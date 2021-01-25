# Optimization Problems

# Optimization Problems

We can define an optimization problem in terms of three requirements

## Objective Function

This is a function we wish to maximize of minimize. We call it the objective function because it provides an objective way to compare different possible choices within the feasible region ( if any ) .

## Decision Variables

These represent the variables whose values are under our control that influence the performance of the system.

## Constraints

Constraints are the restrictions we place on the values of our decision variables.

These three prerequisites must be defined in order to have an optimization problem on hand. Our goal is then to first apply our constraints on our decision variables to obtain a feasible region. This represents the specification of the decision variables which satisfy all of the model's constraints.

We then use our objective function to compare different choices within this feasible region that optimizes the objective function. Optimization can come in many forms (Eg. Maximization, Minimization )

# Types Of Optimization Problem

When considering what type of optimization problem we are looking at, we can consider three main categories

1. Discrete vs Continous : Decision variables are either discrete or continous, leading to us having a corresponding discrete or continous optimization problem

```
Sample Discrete Problem: We can buy eggs and brownies. Eggs cost $1 and give us 100 calories while brownies cost $1.50 and give us 200 calories. How many of each should we buy to maximise the number of calories we obtain. (The number of brownies/eggs takes on a discrete integer value. We cannot have for instance 3.14 eggs, we can only have 3 in this case.)

Sample continous problem : We have 20 metres of fence. We want to maximise the area that we fence off and we want to use a rectangular shape. How can we optimize the area we fence off? (Length is a continous variable and can take on any real value)
```

2. Deterministic vs Stochastic : Sometimes, we are unsure about the value of our decision variables and are only aware of the range that we expect to get them in.

```
Sample Stochastic problem : We expect to sell 8-12 donuts a day. Each donut costs us $1 and we sell them for $1.10 each. How many donuts should we purchase each day to maximise our profit

Sample Deterministic problem: We can buy eggs and brownies. Eggs cost $1 and give us 100 calories while brownies cost $1.50 and give us 200 calories. How many of each should we buy to maximise the number of calories we obtain
```

3. Prescriptive, Optimization and Descriptive :

- Prescriptive models aim to prescribe behaviours for an organization to meet its goals.
- Optimization models seek to find values of the decision variables that optimize an objective function among the set of all values for the decision variables that satisfy the given constraints
- Descriptive models aim to describe the behaviour of a outcome as a function of various factors.

4. Static and Dynamic Models:

- Static Models : Decision variables do not involves sequences of decisions over multiple periods
- Dynamic models : Decision variables do involve sequences of decisions over multiple periods

```
In a static model we solve a “one-shot” problem whose solutions prescribe optimal values of decision variables at all points in time. A dynamic model on the other hand involves decisions made over multiple periods (eg. over the next four quarters) with unique optimal values of decision variables at each point.
```
