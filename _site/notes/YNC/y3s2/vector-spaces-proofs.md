# Vector Spaces Proofs

## Vector Subspace Proofs

### Proof 1 : Spans are a subspace

We can represent all vectors within the span of a list of t we vectors as a linear combination of these vectors. This means that vectors within the span take the form of

$$
\alpha_1 v_1 + \alpha_2 v_2 + \dots + \alpha_n v_n
$$

Where $\alpha_1,\alpha_2,\dots,\alpha_n$ represent values from the set of scalars.

We can show the existence of the zero vector by simply substituiting $\alpha_1 , \alpha_2 , \dots , \alpha_n$ as $0$. As such we have shown the existence of the zero vector in the span.

Next, we move on to show that the span is closed under scalar multiplication. We observe that we can represent a scalar multiplication of an arbitary vector $V$ within our span with a scalar $\beta$ as

$$
 \beta V  = \beta (\alpha_1 v_1 + \alpha_2 v_2 + \dots + \alpha_n v_n) \\
$$

which itself can be rewritten as

$$
\beta V  = \beta\alpha_1 v_1 + \beta\alpha_2 v_2 + \dots + \beta\alpha_n v_n \\
$$

Since we observe that $\beta \alpha_1, \beta \alpha_2,\dots,\alpha_n v_n$ are all simply scalars, we can conclude that $\beta V$ is simply another linear combination of our list of vectors and must therefore exist within our span.

Lastly, we can prove that the span is closed under vector addition using two arbitary vectors $v_1,v_2$ from the span of our list of linearly independent vectors.

Since $v_1$ and $v_2$ are vectors within the span of our list of $n$ linearly independent vectors, we can express them as

$$
v_1 = \alpha_{11} v_1 + \alpha_{12} v_2 + \dots + \alpha_{1n} v_n\\
v_2 = \alpha_{21} v_1 + \alpha_{22} v_2 + \dots + \alpha_{2n} v_n
$$

Adding up these two vectors gives us the new vector of

$$
v_1 + v_2 = \alpha_{11} v_1 + \alpha_{21} v_1 + \alpha_{12} v_2 + \alpha_{22} v_2 + \dots + \alpha_{1n} v_n + \alpha_{2n} v_n\\
$$

Which correpsonds to another linear combination of our list of $n$ vectors that exist within our subspace. This shos that our vectors are closed under addition too.

<!--
To prove that a set is a subspace, we need to show three things

1. The zero vector exists
2. The subspace is closed under scalar multiplication
3. The subspace is closed under vector addition



for a list of $n$ vectors in a $n$ dimensional vector space.

We can construct the zero vector by  -->
