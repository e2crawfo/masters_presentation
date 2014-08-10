### Biologically Plausible, Human-scale<br> Knowledge Representation

### Master's Thesis Presentation
### Aug 14, 2014

Eric Crawford <br>
Centre for Theoretical Neuroscience<br>
University of Waterloo

---Right---

Our formalization of knowledge:
###Semantic Networks

Graph-like stucture.
Node are concepts, edges are relations between concepts.

Edges are labelled with type of relation:<br>
E.g. is a kind of, is an instance of, is a part of, is a member of,
is a substance of

---Right---

Goal: encode an arbitrary semantic network in a network of spiking neurons.

Getting more specific:

<ol>
<li>Establish a vector encoding of the semantic network. Assignment of vectors to each concept and each relation type.</li>
<li>Create a neural network that can "traverse" the semantic network.</li>
<li>Handle large (human-scale) semantic networks without 
</ol>

---Right---

In other words, we want to fill in the blanks in the following network:
<!--<object type="image/svg+xml" data="img/initial_network_opt.svg" width="700"></object>-->

---Right---
###Encoding relational structure.

Edge-list representation of a graph. Can store this using role-filler
construction we have seen before with semantic pointers.

Assuming we have vectors $\mathbf{isA}, \mathbf{partOf}, \mathbf{canine},$ and $\mathbf{pack}$.

<div class="fragment">
<br>
  $\mathbf{dog} = \mathbf{isA} \circledast \mathbf{canine} + \mathbf{partOf} \circledast \mathbf{pack}$
</div>

---Right---
###Extracting relational structure
If we use this method to assign vectors to concepts, then we can use circular convolution $\circledast$ and involution ($\cdot$)$^{-1}$
to extract the target of the relation.

<div class="fragment">
$\newcommand{\inverseop}[1]{\mathbf{#1^{-1}}}$
<!--$\newcommand{\inverseop}[1]{\overline{\mathbf{#1}}}$-->
\begin{align}
&\mathbf{dog} \circledast \inverseop{isA}&\\\\
&=(\mathbf{isA} \circledast \mathbf{canine} + \mathbf{partOf} \circledast \mathbf{pack}) \circledast  \inverseop{isA}&\\\\
&=\mathbf{isA} \circledast \mathbf{canine} \circledast \inverseop{isA} + \mathbf{partOf} \circledast \mathbf{pack} \circledast  \inverseop{isA}&\color{blue}{\text{(Distributive)}}\\\\
&=\mathbf{canine} \circledast \mathbf{isA} \circledast \inverseop{isA} + \mathbf{partOf} \circledast \mathbf{pack} \circledast  \inverseop{isA}&\color{blue}{\text{(Commutative)}}\\\\
&\underbrace{\approx \mathbf{canine} + \mathbf{partOf} \circledast \mathbf{pack} \circledast  \inverseop{isA}}\_{\text{Similar to canine}}&
\end{align}
</div>

---Right---

Lets try this out in code.

---Right---
Adding in the SPA network to perform this operation that we have seen
previously, our network now looks like:

---Right---
###Noise to be removed
The circular convolution/involution operation doesn't get us the whole way.
How can we fix this?

By exploiting the similarity properties of the deconvolution operation.

Need to design a neural network so solve the following problem:

Given a vocabulary of vectors, and a vector that is similar to exactly one of
those vectors, return the vector it is similar to. This is essentially the
problem of **auto-association**.

---Right---
###Auto-association
Extremely well studied problem, many good solutions exist.

**Hopfield nets?**
Too slow, require a settling time.

**Multilayer perceptron, linear associator, straightforward NEF function decoding?**
Don't scale well to large numbers of stored vectors.

---Right---

###Cleanup Memories with the NEF

Abstract algorithm in ipython notebook.

---Right---
Any ideas how we might implement this in Nengo using the NEF?

Hint - the architecture looks like:
---Right---
<ol>
<li>Parallelize - one population per loop iteration</li>
<li>Set encoders equal to vocabulary vectors</li>
<li>Use neurons with high-thresholds</li>
<li>Decode a thresholding function.
$f(x) = 1~\text{if}~x > 0.3~\text{else}~0$</li>
<li>Set output transformation matrix equal to vocabulary vectors.</li>
</ol>

---Right---

Lets try this out in code.

---Right---
What if we want to be able to handle graphs with directed cycles?
Another set of vectors, ID-vectors, chosen from unit hypersphere.
<br>
$\mathbf{dog\_{SP}} = \mathbf{isA} \circledast \mathbf{canine\_{ID}} + \mathbf{partOf} \circledast \mathbf{pack\_{ID}}$

---Right---
Have to make our cleanup memory an associative cleanup memory.

But this is trivial since the inputs and outputs are decoupled.

---Right---

What dimension to use?

Show distributions using I-python notebook.

---Right---
###Extracting from sentences

* Present network with concepts (sentences) it has never seen before, should
  perform well.

* 'dog chase cats' encoded as:<br>
<div class="fragment">
<br>
$\mathbf{sentence} = \mathbf{subject} \circledast \mathbf{dog\_{ID}} + \mathbf{verb} \circledast \mathbf{chase\_{ID}} + \mathbf{object} \circledast \mathbf{cat\_{ID}}$
</div>
<br>

* Can do deep sentences as well. 'mice believe that dogs chase cats' encoded as:

<div class="fragment">
<br>
\begin{align}
\mathbf{deep~sentence} =~\mathbf{subject} \circledast \mathbf{mouse\_{ID}} + \mathbf{verb} \circledast \mathbf{believe\_{ID}}~+\\\\
\mathbf{object} \circledast  (\mathbf{subject} \circledast \mathbf{dog\_{ID}} + \mathbf{verb} \circledast \mathbf{chase\_{ID}} + \mathbf{object} \circledast \mathbf{cat\_{ID}})
\end{align}
<br>
</div>

---Right---
Bonus: WordNet with nltk and networkx.
