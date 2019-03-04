# Writing down qubit states

As we've seen, there are multiple ways to extract an output from a qubit. The two methods we've use so far are the z and x measurements.

```text
// z measurement of qubit 0
measure q[0] -> c[0];

// x measurement of qubit 0
h q[0];
measure q[0] -> c[0];
```

There are many possible states that our qubits can be in. For some, they might give certain outputs with certainty. For others, the output might be random. To continue learning about qubits, we need a way to write down these states and figure out what outputs they'll give. For this we need some notation, and we need some math.

### The z basis

If you do nothing in a circuit but a  measurement, you are certain to get the outcome `0`. This is because the qubits always start in a particular state, and the defining property of that state is that it is certain to output a `0` for a z measurement.

We need a name for this state. Let's be unimaginative and call it $$0$$ . Similarly, there exists a qubit state that is certain to output a `1`. We'll call this $$1 $$.

These two states are completely mutually exclusive. Either the qubit definitely outputs a `0`, or it definitely outputs a `1`.There is no overlap.

One way to represent this with mathematics is using two orthogonal vectors.

$$
|0\rangle = \begin{pmatrix} 1 \\ 0 \end{pmatrix} ~~~~ |1\rangle =\begin{pmatrix} 0 \\ 1 \end{pmatrix}.
$$

This is a lot of notation to take in all at once. First let's unpack the weird $$|$$ and  $$\rangle$$ . Their job is essentially just to remind us that we are talking about the vectors that represent qubit states labelled $$0$$ and $$1$$. This helps us distinguish them from things like the bit values `0` and `1` or the numbers 0 and 1. It is part of the bra-ket notation, introduced by Dirac.

If you are not familiar with vectors, they are essentially just lists of numbers. If we write them as a vertical list, as we have done above, they are called _column vectors_. In Dirac notation, they are also called _kets_.

 Horizontal lists are called _row vectors_ or _bras_ in Dirac notation. They are represented with a $$\langle$$ and a $$|$$.

$$
\langle 0| = \begin{pmatrix} 1 & 0\end{pmatrix} ~~~~ \langle 1| =\begin{pmatrix} 0 & 1 \end{pmatrix}.
$$

Vectors also come with a set of rules on how to manipulate them. These define what it means to add or multiply with vectors. For example, to add two vectors we need them to be the same type and the same length.Then we add each element in one list to the corresponding element in the other. For a couple of arbitrary vectors that we'll call $$a$$ and $$b$$, this works as follows.

$$
\begin{pmatrix} a_0 \\ a_1 \end{pmatrix} +\begin{pmatrix} b_0 \\ b_1 \end{pmatrix}=\begin{pmatrix} a_0+b_0 \\ b_0+b_1 \end{pmatrix}.
$$

To multiple a vector by a number, we simply multiply every element in the list by that number

$$
x \times\begin{pmatrix} a_0 \\ a_1 \end{pmatrix} = \begin{pmatrix} x \times a_0 \\ x \times a_1 \end{pmatrix}
$$

Multiplying a vector with another vector is a bit more tricky, since there are multiple ways we can do it. For now we just need the so-called 'inner product'. 

$$
\begin{pmatrix} a_0 & a_1 \end{pmatrix} \times \begin{pmatrix} b_0 \\ b_1 \end{pmatrix}= a_0~b_0 + a_0~b_1.
$$

Note that the right hand side of this equation contains only normal numbers being multipled and added in a normal way. The inner product of two vectors therefore yields just a number. As we'll see, we can interpret this as a measure of how similar the vectors are.

The inner product requires the first vector to be a bra and the second to be a ket. In fact, this is where their names come from. Dirac wanted to write the inner product as something like$$\langle a | b \rangle$$, which looks like the names of the vectors enclosed in brackets. Then he worked backwards to split the _bracket_ into a _bra_ and a _ket_.

If you try out the inner product on the vectors we already know, you'll find

$$
\langle 0 | 0\rangle = \langle 1 | 1\rangle = 1,\\
\langle 0 | 1\rangle = \langle 0 | 1\rangle = 0.
$$

Here we are using a concise way of writing the inner products where, for example $$\langle 0 | 1 \rangle = \langle 0 | \times | 1 \rangle$$. The top line shows us that the inner product of a state with itself always gives a 1. When done with two orthogonal states, as on the bottom line, we get the outcome 0. These two properties will come in handy later on.

### The x basis \(part 1\)

So far we've looked at states for which the z measurement has a certain outcome. But there are also states for which the outcome of a z measurement is equally likely to be `0` or `1`. What might these look like in the language of vectors?

A good place to start would be something like $$(|0\rangle + |1\rangle)$$ , since this inclues both $$|0\rangle$$and $$|1\rangle$$ with no particular bias towards either. But let's hedge our bets a little and multiply it by some number $$x$$ .

$$
x ~ (|0\rangle + |1\rangle) = \begin{pmatrix} x \\ x \end{pmatrix}
$$

We can choose the value of $$x$$ to make sure that the state plays nicely in our calculations. For example, think about the inner product,

$$
\begin{pmatrix} x & x \end{pmatrix} \times \begin{pmatrix} x \\ x \end{pmatrix}= 2x^2.
$$

We can get any value for the inner product that we want, just by choosing the appropriate value of $$x$$. So let's choose for the inner product to give the value 1. This is what we got for the inner products of $$|0\rangle$$and $$|1\rangle$$with themselves, so let's make it true for this state too.

This condition is known as the normalization condition, and it results in $$x=\frac{1}{\sqrt{2}}$$ . Now we know what our new state is, so here's a few ways of writing it down.

$$
\begin{pmatrix} \frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}} \end{pmatrix} = \frac{1}{\sqrt{2}}\begin{pmatrix} 1 \\ 1 \end{pmatrix} = \frac{ |0\rangle + |1\rangle}{\sqrt{2}}
$$

This state is essentially just $$|0\rangle$$and $$|1\rangle$$added together and then normalized. So we will give it a name to reflect that orgin. We call it $$|+\rangle$$ .

### The Born rule

Now we've got three states that we can write down as vectors. We can also calculate inner products for them. For example, the inner product of each with $$\langle 0 |$$ is

$$
\langle 0 | 0\rangle = 1\\
\langle 0 | 1\rangle = 0\\
~~~~~~\langle 0 | +\rangle = \frac{1}{\sqrt{2}}.
$$

We also know the probabilities of getting various outcomes from a z measurement for these states. For example, let's use  $$p^z_0$$ to denote the probability of the result `0` for a z measurement. The values this has for our three states are,

$$
p_0^z( | 0\rangle) = 1,\\ p_0^z( | 1\rangle) = 0, \\  p_0^z( | +\rangle) = \frac{1}{2}.
$$

As you might have noticed, there's a lot of similarlity between the numbers we get from the inner products and those we get for the probabilities. Specifically, the three probabilities can all be written as the square of the inner products,

$$
p_0^z(|a\rangle) = (~\langle0|a\rangle~)^2.
$$

If we compared the inner products with $$\langle 1 |$$with the probabilities of the `1` outcome, we'd see a similar relation.

$$
\\
p_1^z(|a\rangle) = (~\langle1|a\rangle~)^2.
$$

The same also holds true for other types of measurement. All probabilities in quantum mechanics can be expressed in this way. This is known as the _Born rule_.

### Global and relative phases

States are how we use math to represent what a qubit is doing. With them we can calculate the probabilities of all the possible things that could be measured. These probabilities are essentially all that is physically relevant about a qubit. It is by measuring them that we can determine or verify what state our qubits are in. Anything aspect of the state that doesn't affect the probabilities is therefore just a mathematical curiosity.

Now you'd sat through a paragraph of heavy-handed philoshophy, let's find ourselves a physically irrelevant mathematical curiosity.

Consider a state that looks like this

$$
|\tilde 0\rangle = \begin{pmatrix} -1 \\ 0 \end{pmatrix} = -|0\rangle.
$$

This is is equivalent to multiplying the state $$|0\rangle$$by $$-1$$. It therefore means that every inner product we could calculate with $$|\tilde0\rangle$$ is the same as for $$|0\rangle$$, but multplied by  $$-1$$. 

$$
\langle a|\tilde 0\rangle = -\langle a| 0\rangle
$$

As you probably know, any negative number squares to the same value as its positive counterpart: $$(-x)^2 =x^2$$ .

Since we square inner products to get probabilities, this means that any probability we could ever calculate for $$|\tilde0\rangle$$will give us the same value as for $$|0\rangle$$. Since these, there is no observable different between $$|\tilde0\rangle$$ and $$|0\rangle$$them: they are just different ways of representing the same state.

This is known as the irrelevance of the global phase. Quite simply, this means that multplying the whole of a quantum state by $$-1$$ gives us a state that will look different, but which is actually completely equivalent.

The same is not true if the phase is _relative_ rather than _global_. This would mean multiplying only part of the state by $$-1$$ , for example

$$
\begin{pmatrix} a_0 \\ a_1 \end{pmatrix} \rightarrow \begin{pmatrix} a_0 \\ -a_1 \end{pmatrix}.
$$

Doing this with the $$|+\rangle$$ state gives us a new state. We'll call it $$|-\rangle$$.

$$
|-\rangle =  \frac{1}{\sqrt{2}}\begin{pmatrix} 1 \\ -1 \end{pmatrix} = \frac{ |0\rangle - |1\rangle}{\sqrt{2}}
$$

The values $$p_0^z$$ and $$p_1^z$$ for $$|-\rangle$$ are the same as for $$|+\rangle$$. So these two states are indistinguishable when we make only z measurements. But there are ways to distinguish them. To see how, consider the inner product of $$|+\rangle$$ and  $$|-\rangle$$. 

$$
\langle-|+\rangle = \langle+|-\rangle = 0
$$

The inner product is 0, just as it is for $$|0\rangle$$and $$|1\rangle$$. This means that the $$|+\rangle$$ and  $$|-\rangle$$ states are orthogonal: they represent a pair of mutually exclusive possible ways for a qubit to be a qubit.

### The x basis \(part 2\)

Whenever we find a pair of orthogonal qubit states, we can use it to define a kind of measurement.

First, let's apply this to the case we know well: the z measurement. This asks a qubit whether it is $$|0\rangle$$ or $$|1\rangle$$. If it is $$|0\rangle$$, we get the result `0`. For $$|1\rangle$$we get `1`. Anything else, such as $$|+\rangle$$, is treated as a superposition of the two.

$$
|+\rangle = \frac{|0\rangle+|1\rangle}{\sqrt{2}}.
$$

For a superposition, the qubit needs to randomly choose between the two possibilities according to the Born rule.

We can similarly define a measurement based on $$|+\rangle$$ and  $$|-\rangle$$. This asks a qubit whether it is $$|+\rangle$$ or  $$|-\rangle$$. If it is $$|+\rangle$$, we get the result `0`. For $$|-\rangle$$we get `1`. Anything else is treated as a superposition of the two. This includes the states$$|0\rangle$$and $$|1\rangle$$, which we can write as

$$
|0\rangle = \frac{|+\rangle+|-\rangle}{\sqrt{2}}, ~~~ |1\rangle = \frac{|+\rangle-|-\rangle}{\sqrt{2}}.
$$

For these, and any other superpositions of $$|+\rangle$$ and  $$|-\rangle$$, the qubit chooses it's outcome randomly with probabilities

$$
p_0^x(|a\rangle) = (~\langle+|a\rangle~)^2,\\
p_1^x(|a\rangle) = (~\langle-|a\rangle~)^2.
$$

This is the x measurement.

### The conservation of certainty

Qubits in quantum circuits always start out in the state $$|0\rangle$$. By applying different operations, we can make them explore other states.

Try this out yourself using a single qubit, creating circuits using operations from the following list, and then doing x and z measurements.

```text
h q[0]; \\ the hadamard
x q[0]; \\ x rotation
y q[0]; \\ y rotation
z q[0]; \\ z rotation
\\ for the following, replace theta by any number
u3(theta,-pi/2,pi/2) q[0]; \\ x rotation
u1(theta) q[0]; \\ z rotation
```

You'll find examples where the z measurement gives a certain result, but the x is completely random. You'll also find examples where the opposite is true. Furthermore, there are many examples where both are partially random. With enough experimentation, you might even uncover the rule that underlies this behaviour.

$$
(p^z_0-p^z_1)^2 + (p^x_0-p^x_1)^2 = 1
$$

This is a version of Heisenberg's famous uncertainty principle. The $$(p^z_0-p^z_1)^2$$ term measures how certain the qubit is about the outcome of a z measurement. It is 1 if either outcome is certain, and 0 when both are equally likely. The $$(p^x_0-p^x_1)^2$$ term measures the same for the x measurement. Their sum is the total certainty of the two combinbed. Given that this total certainty always takes the same value, we find that certainty  limited and conserved resource.

The above is not actually entirely true, as you'd soon see by trying any of the operations below

```text
s q[0]; \\ the s gate
sdg q[0]; \\ the inverse of the s gate
u3(theta,0,0) q[0]; \\ y rotation
```

For a circuit with a single `u3(pi/2,0,0)`, for example, we find that $$(p^z_0-p^z_1)^2 + (p^x_0-p^x_1)^2=0$$ . This makes it seem like our certainty has all been removed this operation. But  a circuit where we do `u3(pi/2,0,0)` twice is back to obeying $$(p^z_0-p^z_1)^2 + (p^x_0-p^x_1)^2=1$$. So this operation does not destroy our certainty. It simply moves it back and forwards between and z and x measurements and somewhere else. So let's find out where it goes.

### The y basis


