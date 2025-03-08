---
title: "MCPs are really LLM microservices"
date: 2025-03-08
description: "How Model Context Protocols enable dynamic tool integration for AI systems"
categories:
  - MCPs
  - LLM
  - Trends
authors:
  - ivanleomk
---

Language Model applications have a fundamental problem: they need better ways to access tools and services. Developers currently spend hours coding custom integrations, maintaining authentication flows, and defining complex schemas for each external service. This creates bottlenecks that limit what AI systems can actually do for users.

Anthropic's Model Context Protocol (MCPs) offers a potential solution by providing a standardized way for LLMs to discover and use tools dynamically. Think of MCPs as an API specification for AI microservices - they define how AI systems can find, call, and combine different tools without requiring developers to hardcode every possible interaction.

In this article, I'll explore what makes MCPs promising, the challenges they solve, and what's still missing for them to move towards become production-ready. This largely serves as some of my own thoughts after chatting with people about them over the past week or so, I'd love to know if you think differently.

<!-- more -->

## The Current State of Tool Integration

Today's language model applications face a fundamental challenge: to be truly useful, they need seamless access to user data and external services. Consider a simple query like "What events do I have tomorrow?"

Currently, developers must:

1. Study API documentation for each service
2. Implement custom integration code with the right authentication flows
3. Defined the function call and keep it updated

While function calling has improved this somewhat, it doesn't solve the core challenge: tools are still statically defined. For models to be able to do more and solve more unique challenges, there needs to be a way for them to discover new tools dynamically and add them to their arsenal or combine existing tools to be executed in a single step.

## Understanding MCPs: More Than Just Another API Spec

MCPs provide a standardized way for models to discover and interact with tools through two simple endpoints: `/tools/list` for discovering available tools, and `/tools/call` for executing them. Each tool is defined with a basic schema:

```json
{
  "name": "string",          // Unique identifier for the tool
  "description": "string",   // Human-readable description
  "inputSchema": {           // JSON Schema for the tool's parameters
    "type": "object",
    "properties": { ... }    // Tool-specific parameters
  }
}
```

While this might seem similar to OpenAPI specifications, MCPs serve a fundamentally different purpose. They're deliberately constrained to support a specific vision: enabling AI systems to dynamically discover and chain multiple tools within a single completion.

This is different from traditional REST APIs where each endpoint typically handles one discrete operation. For example, when a model needs to analyze calendar data and send meeting summaries via email, it can discover and compose these tools on the fly rather than requiring developers to implement these combinations upfront.

Currently, users interact with MCPs through a MCP client. A majority of these clients only support tool calling as seen in [Anthropic's client list](https://modelcontextprotocol.io/clients) - which is why we've chosen to focus on it but the specification does lay the groundwork for more sophisticated forms of interactions.

The simplicity of the tool calling protocol - just two endpoints - makes it easy to implement while still supporting complex tool compositions that would be cumbersome to represent in traditional API specifications.

## The Infrastructure Gap

However, current MCP implementations often exist as proof-of-concept projects - local servers piping commands through standard input/output. While this works for enthusiastic developers experimenting with personal workflows, the path to production-ready systems reveals several crucial infrastructure gaps.

1. **Authentication and Authorization**: Current implementations rely on simple API keys, but production systems need more sophisticated approaches. Consider the difference between "show me today's calendar events" (relatively low risk) versus "cancel my meeting with the CEO" (high risk). We need OAuth-style flows with granular permissions that can distinguish between read operations and potentially destructive actions which can be invoked across multiple services.

2. **Context Management**: As models collaborate across services, they need a way to share this context. This happens because of two main issues - only relevant context should flow across boundaries with appropriate privacy safeguards and we need a way to maintain conversational context of what's happened so far without forcing users to repeat information.

3. **Observability and Debugging**: When combining multiple AI services, tracing the source of errors becomes exponentially more complex. We need standardized logging and monitoring to understand what happened when things go wrong, especially when one model delegates to another.

These challenges highlight why MCPs are currently more "microservices in concept" than "microservices in practice."

While the specification provides a foundation, building truly production-ready systems will require solutions to these infrastructure problems. The community of MCP developers is actively working on these issues, but significant work remains before MCPs can seamlessly power complex production applications.

## Looking Forward: Adaptive AI Microservices

The future we're working toward is one where AI services can dynamically create and compose tools based on usage patterns and needs. Current MCPs focus on single-model interactions with granular tools, but the real potential lies in building networks of specialized AI microservices that communicate through standardized interfaces.

Consider how rapidly the ecosystem is already growing. Some hosted MCP providers are already handling up to 18,000 requests daily, showing clear product-market fit. New marketplaces for MCPs (like Cline's recent launch) are enabling developers to monetize these specialized services. This evolution parallels traditional microservices architecture, but with a crucial difference: the coordination happens through AI reasoning rather than hardcoded logic.

These AI microservices will need to:

- Discover and integrate new tools dynamically
- Execute semantically complex tasks (not just "get my GitHub issues" but "summarize my most urgent pull requests")
- Handle delegated responsibility across multiple models with different specializations
- Maintain context and security boundaries between services
- Scale and adapt based on usage patterns

For example, instead of a model making numerous individual API calls to find products, a future e-commerce MCP might accept queries like "fetch me ten black dresses under $200 in size S available for same-day delivery in Singapore" and handle all the necessary filtering, sorting and availability checks internally. The model doesn't need to understand the implementation - just the capability.

## Conclusion

The true promise of MCPs isn't in their technical specification, but in how they enable a new paradigm for AI services: systems that can dynamically discover, compose, and coordinate tools on behalf of users. While today's implementations are just scratching the surface, the evolution from simple tool calling to truly adaptive AI microservices will require solving complex challenges around authentication, context sharing, security, and observability.

By addressing these challenges systematically, we can move beyond proof-of-concept implementations to production-ready systems that truly enable the next generation of AI applications – ones where the focus shifts to meeting user needs rather than managing technical integrations.
