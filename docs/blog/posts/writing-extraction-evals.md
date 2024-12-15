---
title: Converting Subjective Evals to Binary Metrics
date: 2024-12-15
description: How to write simpler evaluations for subjective tasks
categories:
  - LLMs
authors:
  - ivanleomk
---

# Converting Subjective Evals to Binary Metrics

Although many tasks require subjective evaluations, I've found that starting with simple binary metrics can get you surprisingly far. In this article, I'll share a recent case study of extracting questions from transcripts.

We'll do so in 3 steps

1. First, we'll see how synthetic data can be a good starting point to iterate quickly
2. Then we'll see an example of how to convert a subjective evaluation to a binary metric
3. Lastly, we'll walk through how we used this approach to iteratively improve our prompts and evals

By the end of this article, you'll have a good starting point for writing better evals for your next project.

<!-- more -->

## The Initial Challenge

I recently faced what seemed like a straightforward task: extract question-answer pairs from office hours transcripts. The actual implementation, however, revealed 3 main challenges

1. The transcripts were long and took a long time to process
2. It was difficult to measure the quality of the extracted questions
3. It was difficult to iterate on the prompts and evals ( as a result of 1 and 2 )

Each time I made a call to Claude, I had to wait 2-3 minutes for the transcript to be processed. After 15 minutes of this, I knew I needed a different approach. Additionally, since I was manually reviewing each extracted question, it was difficult to know if I was making progress.

## Moving to Binary Metrics with Synthetic Data

When building LLM applications that seem to require subjective evaluation, consider:

1. Starting with synthetic data. Create small, focused examples that capture the key aspects of your problem. This enables rapid iteration and testing of different approaches.
2. Looking for binary components. While the overall task might be subjective, there are often objective pieces you can measure. Finding the right parts of a document, matching known patterns, or identifying specific features can all be evaluated binarily.
3. Building up gradually. Start with simple metrics on synthetic data, then add complexity as you confirm basic functionality. This methodical approach helps ensure you're building on a solid foundation.

Let's see how this worked out in this specific example.

### Starting with Synthetic Data

Rather than continue struggling with full transcripts, I took a step back and created synthetic data. Since the original transcripts were about fine-tuning models, I generated several smaller conversations about the same topic by manually prompting Claude with the prompt of

> Hey here's a transcript I'm working with. I'd like you to generate sample conversations that follow the same format and talk about <topic>. Specifically let's introduce some back and forth, useless information and have people hesitate on questions in a natural way. Vary the conversations and how people ask questions in a natural way

Here's an example:

```python
{"id": 4, "text": "Thanks Alex. I'm working with a client who wants to implement LLMs for their customer service, but they have this massive legacy system that's basically held together with duct tape. How do you handle situations where the underlying infrastructure is a mess?", "speaker": "James Wilson"}
{"id": 5, "text": "Oh man, legacy systems - the eternal challenge. Hold on, my cat just knocked over my coffee... again. Give me two seconds.", "speaker": "Dr. Alex Liu"}
{"id": 6, "text": "While Alex cleans up, maybe we can share our worst legacy system horror stories? I once found COBOL code from the 70s still running in production.", "speaker": "\u26a1 Mark Chen (TA)"}
{"id": 7, "text": "I'll do you one better - I found a crucial Python script with comments in Latin. Actual Latin.", "speaker": "Sarah Martinez"}
{"id": 8, "text": "Okay, I'm back - thankfully missed my keyboard this time. So James, about legacy systems - this is actually a perfect example of where understanding business value comes in.  Instead of trying to bolt AI onto a fragile system, I usually start by mapping out the actual business processes. What are they trying to achieve? Often, you can start with a smaller, isolated pilot that proves value without touching the core system.  The key is to quantify the potential impact. If automating customer service could save them $2M annually, suddenly that $500K infrastructure upgrade doesn't seem so expensive.", "speaker": "Dr. Alex Liu"}
{"id": 9, "text": "That makes sense. How do you handle the stakeholder management though? Usually there's someone who's been maintaining that legacy system for 20 years and sees any change as a threat.", "speaker": "James Wilson"}
{"id": 10, "text": "Great point. This is where the soft skills really matter. I always try to make that person a key ally. They know where all the bodies are buried, so to speak.  Oh, speaking of bodies - did anyone watch the new True Detective episode? No spoilers, but wow.", "speaker": "Dr. Alex Liu"}
```

These synthetic transcripts took only 30 seconds to process instead of several minutes. This faster iteration cycle proved crucial for improving the system. While synthetic data isn't perfect, it let me rapidly test different approaches without getting bogged down in processing time.

### Using Citations

My first attempt at making evaluation more concrete was simple counting. I knew how many questions should be in each synthetic transcript, so I added basic assertions:

```python
class Questions(BaseModel):
    questions: List[Question]

def test_extraction():
    questions = extract_questions(synthetic_transcript)
    assert len(questions.questions) == 4  # We expect 4 Q&A pairs
```

This was better than pure subjective review, but it had a major flaw: just because we extracted the right number of questions doesn't mean they were the right questions. The model might find four questions, but were they the important ones we wanted?

This led to the key insight: we needed to know if the model was looking at the right parts of the transcript. I modified the question model to include source citations. These were the chunk ids that were provided by the synthetic transcripts that we had above.

```python
class Question(BaseModel):
    relevant_chunk_ids: list[int]  # Which transcript chunks contain this Q&A
    question: str
    answer: str
```

Now instead of just counting questions, we could verify if the model identified the correct transcript segments. This transformed our evaluation from "are these good questions?" to "did we find the right chunks that we can identify for downstream processing".

### Why Binary Metrics work

With citation checking in place, evaluation became straightforward recall calculation: out of all the question-answer segments we know exist and their relevant chunks, what percentage did the model find? This simple metric proved remarkably powerful.

The code to evaluate these metrics is also relatively simple.

```python


async def run_test(test_case):
    path = test_case["path"]
    expected_ids = test_case["expected_ids"]

    with open(path, "r") as f:
        content = f.read()
        questions = await extract_questions(content)

        # Count exact matches between expected and found question IDs
        matches = 0
        for expected_id_group in expected_ids:
            for question in questions.questions:
                if question.relevant_chunk_ids == expected_id_group:
                    matches += 1
                    break

        recall = matches / len(expected_ids)

        return {
            "path": path,
            "recall": recall,
            "questions": questions.questions,
            "question_count": f"{len(questions.questions)}/{len(expected_ids)}",
            "missing_questions": [
                expected_id_group
                for expected_id_group in expected_ids
                if not any(
                    q.relevant_chunk_ids == expected_id_group
                    for q in questions.questions
                )
            ],
        }
```

We're literally just counting the number of matches and dividing by the total number of expected ids. This is a simple metric that can be calculated quickly. More importantly, with about 30 minutes of this new metric, I had significantly improved the model's ability to identify relevant transcript segments.

This transferred effectively to real-world data. When I finally tested the improved system on real transcripts, it was able to identify relevant chunks that I agreed with.

## Conclusion

Ideally, you should start with simple metrics that can be calculated quickly. While in this example we've seen that binary metrics are easy to calculate, their benefits extend far beyond just measurement efficiency.

Firstly, they reduce the cognitive load making it easy for other members of the team to evaluate the results. They don't need to wrestle with complex scoring rubrics or subjective scales.

Secondly, they lower the barrier to team participation. With more nuanced evaluation systems, like 1-5 scales or detailed rubrics, you often need extensive domain knowledge and training to evaluate consistently.

Lastly, they make it easy to get started. Often times when evaluations are more complex and subjective, it's hard to find common ground. Binary metrics on the other hand, make it easy to secure quick early wins and get started.

Eventually you'd want to move to more complex metrics but starting with binary metrics is a good way to get started. Converting subjective evaluation into binary metrics isn't always obvious, but it's often more possible than it first appears. By combining synthetic data with simple, measurable objectives, you can create a development process that enables rapid iteration while maintaining clear quality standards.

Remember: the goal isn't to eliminate subjective evaluation entirely, but to establish a solid foundation of measurable metrics first. This makes it much easier to systematically improve your system and know when you're making real progress.
