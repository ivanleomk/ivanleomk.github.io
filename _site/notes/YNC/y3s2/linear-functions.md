# Linear Functions

# What is a Linear Function

A Linear function is one which **applies a scalar multiple to each individual variable within the function** and **passes through the origin at $x=0$ **.

$$
f(x_1,x_2,\dots,x_n) = \alpha_1 x_1 + \alpha_2 x_2 + \dots + \alpha_n x_n
$$

As a result, the following are not linear functions

1. $f(x,y) = xy$
2. $f(x,y) =sin(x)$
3. $f(x) = x^n$
4. $f(x) = 2x+3$

We observe that

(1) is not a linear function because individual variables are multiplied against one another rather than using a scalar multiple (e. 2,3,4)

(2) is not a linear function because a non-linear function is applied against a variable

(3) is not a linear function because a variable is raised to a power $n$ which is not equal to $1$

(4) is not a linear function because it does not pass through the origin at $x=0$. It is instead a [[affine function]]

# Solving Linear Programming Question

Step 1 : Decide on the decision variables

Step 2 : Identify the constraints

Step 3 : Find the feasible area

## Determinine the Feasible Area - Maximisation

I have 200 hectares of Land, $10,000 of upfront investment and 1200 labour man-hours. I incur the following profit and costs when I plant the two respective crops - Wheat and barley

| Crop Name | Cost/Hec | Profit/Hec | Labor/Hec |
| --------- | -------- | ---------- | --------- |
| Wheat     | $100     | $50        | $10       |
| Barley    | $200     | $120       | $30       |

Question : How should I optimize this?

**Step 1** : Decide on our decision variables

We know that we need to vary the amount of hectares of barley and wheat that we plant in terms of hectares. Let us term this $B$ and $W$.

**Step 2** : Decide on our constraints

We have the following constraints

1. We must plant positive amounts of barley and wheat. This can be expressed as $B\geq 0$ and $W \geq 0$.

2. We must also ensure that the total cost incurred for our barley and wheat planting exercise is within our original budget of $10,000$. We also know that the cost per hectare to plant barley and wheat is $100$ and $200$ respectively. We can therefore express this as

3. We must also ensure that the total amount of man-hours we spend to plant all our crops is going to be within the 1200 labor man-hours we have. This means that we have

4. We must ensure that the total amount of barley and wheat we plant does not exceed $200$ hectares. This can be expressed as $B+W\leq200$.

**Step 3** : Find our feasible Region

1. We first begin by defining our decision region. We can do so by applying the following constraints to an infinite plane.

This gives us a feasible region as seen below.

![](../../../assets/images/FeasibleArea.png)

1. We then begin by applying our second constraint, that is that the total amount of barley and wheat does not exceed 200 hectares and that the amount of man hours we spend to plant our crops is within the 1200 labor man hours. These correspond to

We then apply our new constraints and arrive at a new feasible radius of

1. We can conclude that the best amount of barley and wheat to plant should therefore be the at the intersection seen below since we plant the most barley and wheat at that point.

![](../../../assets/images/NewFeasible.png)

# Convex Areas

A convex area is defined as a part of a plane such that any two of its points are entirely contained within that part of the plane. Any connecting part of the boundary of the convex area is called a convex curve.
