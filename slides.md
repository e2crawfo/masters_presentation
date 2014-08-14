
<div class="fragment">
$\newcommand{\id}[1]{\mathbf{#1_{id}}}$
</div>

<div class="fragment">
$\newcommand{\hrr}[1]{\mathbf{#1_{sp}}}$
</div>

<div class="fragment">
$\newcommand{\cc}[]{\circledast}$
</div>

<div class="fragment">
$\newcommand{\vc}[1]{\mathbf{#1}}$
</div>

<div class="fragment">
$\newcommand{\inverseop}[1]{\overline{\mathbf{#1}}}$
</div>

<div class="fragment">
$\newcommand{\pair}[2]{\langle#1,#2\rangle}$
</div>

<div class="fragment">
$\newcommand{\hili}[1]{\color{blue}{\mathbf{#1}}}$
</div>

---Right---
### Biologically Plausible, <br>Human-scale Knowledge Representation

### Master's Thesis Presentation
### Aug 14, 2014

Eric Crawford <br>
Centre for Theoretical Neuroscience<br>
University of Waterloo

---Right---
##<font color="blue">Outline</font>
<ol>
<li>Introduction</li>
<li>Past Approaches</li>
<li>Semantic Pointers</li>
<li>Neural Implementation</li>
<li>Results</li>
<li>Conclusion</li>
</ol>

---Right---
##1. Introduction

---Right---

Interested in how the brain represents knowledge. Specifically,
##Structured Representations
<br>
<div style="width: 100%;">
  <div style="width: 50%; float: left;" class="fragment">
    <center>Natural Language</center>
    <img src="img/natlang.jpg" width="300">
  </div>

  <div style="margin-left: 50%;" class="fragment">
    <center>Recipes</center>
    <img src="img/recipe.png" width="200px">
  </div>
</div>

<div style="width: 100%; overflow: hidden;">
  <div style="width: 50%; float: left;" class="fragment">
    <br>
    <center>Programming languages</center>
     <pre><code data-trim>
def fib(n):
   if n==1 or n==2:
      return 1

   return fib(n-1) + fib(n-2)

print fib(5)
     </code></pre>
  </div>

  <div style="margin-left: 50%;" class="fragment">
    <br>
    <center>Mathematics</center>
    <br>
    $i \hbar \frac{ \partial f}  {\partial t} = - \frac{\hbar ^2}{2m}\nabla ^2f + U(x) f$
  </div>

</div>

---Right---
##Two criteria:
For a connectionist account of structured representations.

<ol>
<li> Human-scale.</li>
<li> Biologically plausible.</li>
</ol>

---Right---
###Human-scale?
"In the Hitchhiker's Guide to the Galaxy, a fearsome intergalactic battle fleet is accidentally eaten by a small dog due to a terrible miscalculation of scale. I think that a similar fate awaits most of the models proposed by Cognitive Scientists"

-----

<small>Geoff Hinton. Where do features come from? In *Outstanding questions in cognitive science: A
symposium honoring ten years of the David E. Rumelhart prize in cognitive science*. Cognitive Science Society, 2010.

---Right---
Cognitive scientists like to focus on toy problems. But humans deal with
extremely large structured representations, and our models must be able to
account for that.

<div class="fragment">
  <img src="img/clifford_dictionary.svg" width="600">
</div>

E.g., the size of adult human vocabulary estimated to be 60,000 words.

---------

<small>David Crystal. *Cambridge encyclopedia of the english language.* Cambridge University Press. Cambridge, UK. 2003.</small>

---Right---

###Biologically plausible?
Achieve this under the constraints that the *adult human* brain operates under.
<br>
<div style="width: 100%;">
  <div style="width: 50%; float: left;" class="fragment">
    <center>Spiking neurons</center>
    <img src="img/neurons.jpg" width="400px">
  </div>

  <div style="margin-left: 50%;" class="fragment">
    <center>Not too many of them</center>
    <img src="img/bigbrain.jpg" width="400px">
  </div>
</div>
<br>
<div class="fragment">
</div>

---Right---
##2. Past approaches
No existing approach is capable of encoding a human-scale knowledge structure in spiking neurons without making implausible neural resource assumptions. We demonstrate this for 3 of the most successful approaches.

---Right---
###Synchrony
<div style="width: 100%;">
<img src="img/synchrony.png" width="700">
</div>

---Right---
##Requires more neurons than there are in the human brain
####Because each fact/proposition requires a devoted node

Assume vocabulary with $\hili{1500~nouns}$, $\hili{500~verbs}$, and $\hili{100~neurons~per~node}$.
Neurons required to represent all relations of the form $\hili{verb(noun,~noun)}$:

<br>
$1500 \times 1500 \times 500 \times 100 = \hili{1.1\times10^{11}~neurons}$

$>$ than the $\hili{50\times10{}^{9}~neurons}$ in cortex$^1$.
<br>

-----

<small>1. Alan Peters and Edward Jones. *Cerebral Cortex*. Plenum Press.
New York, NY. 1984.</small>

---Right---
###Neural Blackboard Architecture

<div style="width: 100%;">
<img src="img/nba3.png" width="700">
</div>

---Right---
##Requires more cortical area allotted to all known-language areas

Conservatively assume:<br>
60,000 words<br>
2 roles<br>
100 assemblies/role<br>
800 neurons/mesh element<br>

$60,000$ words $\times 200$ assemblies $\times 800$ neurons/mesh element<br>
=<font color="blue">$96 \times 10^8$ neurons.</font><br>

Works out to roughly $480~cm^2$ of cortical area.

All language areas comprise only about $250~cm^2$*.

----

<small>*Chris Eliasmith. *How to Build a Brain.* Oxford University Press. New York, NY.
2013.</small>

---Right---
###Tensor Product
<div style="width: 100%;">
<img src="img/tensor.png" width="700">
</div>

---Right---
##Scales poorly with the depth of the encoded structure
####Because the size of the representation expands for each added level

Assume representations of nouns requires 512 dimensions.
Representing <font color="blue">Bill believes that Max is larger than Eve</font> requires:<br>
$512 \times 512 \times 512 = 12.5 \times 10^7$ dimensions.

Assuming $50$ neurons per dimension gives <font color="blue">$6.25 \times 10^9$ neurons</font>.<br>
Works out to roughly $312~cm^2$ of cortical area, still larger than all language
areas.

---Down---
Short-term vs long-term storage of bindings.
Localist vs distributed.
Classical vs non-classical

---Right---

###So
###<font color="blue">Biologically Plausible, Human-scale Knowledge Representation</font>
###is still an open problem

---Right---
##3. Semantic Pointers

---Right---
###Our Goal:
###<font color="blue">Encode human-scale knowledge base in a reasonable number of spiking neurons</font>
<div style="width: 100%;">
<img src="img/sn_to_nn.svg" width="1000">
</div>

---Right---

###Our Approach:
#<font color="blue">Semantic Pointers</font>

###Neurally realized, compressed representations of high-dimensional data.
<ul>
<li>Can be manipulated more easily than high-dimensional representation</li>
<li>Bear systematic relationship to the data they are generated from</li>
<li>Can be decompressed to recover approximation of pre-compressed data</li>
</ul>

----

<small>Chris Eliasmith. *How to Build a Brain.* Oxford University Press. New York, NY.
2013.</small>

---Right---
##Example: Visual Semantic Pointers
###Generative Statistical Models

<div style="width: 100%;">
  <div style="width: 50%; float: left;" class="fragment">
    <center><font color="blue">Compression</font></center>
    <img src="img/visual_compression.png" width="700">
  </div>
  <div style="margin-left: 50%;" class="fragment">
    <center><font color="blue">Decompression</font></center>
    <img src="img/visual_decompression.png" width="700">
  </div>
</div>

---Right---
##<font color="blue">Holographic Reduced Representations</font>
###Semantic Pointers for Structured Representations
A Vector Symbolic Architecture, like tensor products. But with better scaling properties.

---Right---
##HRR Operations
$\mathbf{x}$ and $\mathbf{y}$ are $D$-dimensional vectors.

-----

<div style="width: 100%;">
  <div style="width: 50%; float: left;" class="fragment">
    <center><font color="blue">Circular Convolution</font></center>
    $\mathbf{x} \circledast \mathbf{y}$<br>
    $(\mathbf{x} \circledast \mathbf{y})\_{(j)} = \sum\_{k = 0}^{D-1} \mathbf{x}\_{(k)} \mathbf{y}\_{(k - j)}$<br>
    $\mathbf{x} \circledast \mathbf{y}$ <i>dissimilar</i> to $\mathbf{x}$ and $\mathbf{y}$
  </div>
  <div style="margin-left: 50%;" class="fragment">
    <center><font color="blue">Vector Addition</font></center>
    $\mathbf{x} + \mathbf{y}$<br>
    $(\mathbf{x} + \mathbf{y})\_{(j)} = \mathbf{x}\_{(j)} + \mathbf{y}\_{(j)}$
    <br>
    $\mathbf{x} + \mathbf{y}$ <i>similar</i> to $\mathbf{x}$ and $\mathbf{y}$
  </div>
</div>
<br>
<div style="width: 100%;" class="fragment">
  <center><font color="blue">Involution</font></center>
  $\inverseop{x}$<br>
  $\overline{\mathbf{x}}\_{(j)} = \mathbf{x}\_{(-j)}$<br>
  Approximate inverse wrt $\circledast$:
  <br>
  $\mathbf{x} \circledast \mathbf{y} \circledast \inverseop{y} \approx \mathbf{x}$
</div>
<br>
(All indices taken modulo $D$)

---Right---
##Compression
Can use $\circledast$ and $+$ to create semantic pointers storing structured representations. E.g., role-filler structures:<br><br>
$\vc{S} = \vc{R\_1} \circledast \vc{F\_1} + \vc{R\_2} \circledast \vc{F\_2} + \vc{R\_3} \circledast \vc{F\_3} $<br><br>
where $\vc{S}$, $\vc{R_i}$ and $\vc{F_i}$ are all $D$-dimensional vectors.

---Right---
##Decompression
Can approximately extract constituents of the structure using $\circledast$ and $\inverseop{(\cdot)}$.<br>
E.g., can reconstruct the vector filling role 1 by computing:<br><br>

<div style="margin-left: 5%;">
\begin{align}
&\vc{S} \circledast \inverseop{R\_1}&\\\\

&=(\vc{R\_1} \circledast \vc{F\_1}  + \vc{R\_2} \circledast \vc{F\_2} + \vc{R\_3} \circledast \vc{F\_3} ) \circledast  \inverseop{R\_1}&\\\\

&=\vc{R\_1} \circledast \vc{F\_1} \circledast \inverseop{R\_1} + \vc{R\_2} \circledast \vc{F\_2} \circledast  \inverseop{R\_1} + \vc{R\_3} \circledast \vc{F\_3} \circledast \inverseop{R\_1}  &\color{blue}{\text{(Distributive)}}\\\\

&=\vc{F\_1} \circledast \vc{R\_1} \circledast \inverseop{R\_1} + \vc{R\_2} \circledast \vc{F\_2} \circledast  \inverseop{R\_1} + \vc{R\_3} \circledast \vc{F\_3} \circledast \inverseop{R\_1}  &\color{blue}{\text{(Commutative)}}\\\\

&\approx \color{blue}{\underbrace{\color{white}{\vc{F\_1} + \vc{R\_2} \circledast \vc{F\_2} \circledast  \inverseop{R\_1} + \vc{R\_3} \circledast \vc{F\_3} \circledast \inverseop{R\_1}  }}\_{\text{Similar to}~\vc{F\_1}}}&
\end{align}
</div>

---Right---
#WordNet
###A human-scale knowledge base.

###117,659 concepts.

Concepts are nodes, relations are directed, labelled edges between nodes.

5 types of relations:<br>
$\mathbf{class, instance, substance, member, part}$

---Right---
<div style="width: 100%;">
<img src="img/wordnet_dog.png" width="800">
</div>

---Right---
##Encode WordNet in semantic pointers.
<br>
###All vectors have dimensionality $D = 512$ <br><br>

####Relation-type vectors
Assign random $D$-dimensional vector to each relation-type.<br><br>

####ID-vectors
Assign each concept a randomly chosen $D$-dimensional unit vector.<br><br>

####Semantic Pointers
Assign each concept another $D$ dimensional role-filler semantic pointer storing the structural relations.

---Right---
Part of the relational structure of *dog* is:<br><br>
*dog = class(canine) and member(pack)*<br><br>

-----

Semantic pointer *dog* for would be:<br><br>
$\hrr{dog} = \vc{class} \circledast \id{canine} + \vc{member} \circledast \id{pack}$

---Right---
Now we can use decompression ($\circledast$ and $\inverseop{(\cdot)}$) to *traverse* an edge in WordNet.

<div class="fragment">
\begin{align}
&\hrr{dog} \circledast \inverseop{class}&\\\\
&=(\vc{class} \circledast \id{canine} + \vc{member} \circledast \id{pack}) \circledast  \inverseop{class}&\\\\
&=\vc{class} \circledast \id{canine} \circledast \inverseop{class} + \vc{member} \circledast \id{pack} \circledast  \inverseop{class}&\color{blue}{\text{(Distributive)}}\\\\
&=\id{canine} \circledast \vc{class} \circledast \inverseop{class} + \vc{member} \circledast \id{pack} \circledast  \inverseop{class}&\color{blue}{\text{(Commutative)}}\\\\
&\approx \color{blue}{\underbrace{\color{white}{\id{canine} + \vc{member} \circledast \id{pack} \circledast  \inverseop{class}}}\_{\text{Similar to}~\id{canine}}}&
%&\approx \underbrace{\id{canine} + \vc{member} \circledast \id{pack} \circledast  \inverseop{class}}\_{\text{Similar to}~\id{canine}}&
\end{align}
</div>

---Right---
##Semantic Pointers for Sentences
<br>
<font color=blue>dogs chase cats</font> encoded as:<br>
<div class="fragment">
<br>
$\hrr{sentence} = \vc{subject} \circledast \id{dog} + \vc{verb} \circledast \id{chase} + \vc{object} \circledast \id{cat}$
</div>
<br>
<div class="fragment">
Extract constituents:<br><br>
$\hrr{sentence} \circledast \inverseop{verb}$ similar to $\id{chase}$
</div>

---Right---
##Semantic Pointers for Deep Sentences
<br>
<font color="blue">mice believe that dogs chase cats</font> encoded as:
<div class="fragment">
<br>
\begin{align}
\hrr{deep~sentence} =~\vc{subject} \circledast \id{mouse} + \vc{verb} \circledast \id{believe}~+\\\\
\vc{object} \circledast  (\vc{subject} \circledast \id{dog} + \vc{verb} \circledast \id{chase} + \vc{object} \circledast \id{cat})
\end{align}
</div>
<br>
<div class="fragment">
Extract constituents:<br><br>
$\hrr{deep~sentence} \circledast \inverseop{(\vc{object} \circledast \vc{subject})}$ similar to $\id{dog}$
</div>

---Right---
##Two Problems
<div style="width: 100%;">
  <div style="width: 50%; float: left;" class="fragment">
    <center>1. Result of Decompression is Noisy</center>
    <br>
    $\hrr{dog} \cc{} \inverseop{class} \neq \id{canine}$
    $\hrr{sentence} \cc{} \inverseop{verb} \neq \id{chase}$
  </div>

  <div style="margin-left: 50%;" class="fragment">
    <center>2. Prefer SP's over ID-vectors </center>
    <br>
    $\hrr{dog} > \id{dog}$
  </div>
</div>

---Right---
##Associative Memory

Associate pairs of vectors $\pair{\xi_k}{\eta_k}$ for $k = 1 \dots N$.

$\xi_k$ are the address vectors, $\eta_k$ are stored vectors.
Given noisy version of an $\xi$, output corresponding $\eta$.

<div style="width: 100%;">
<img src="img/association_algorithm.png" width="500">
</div>

Let $\xi$'s be ID-vectors, $\eta$'s be semantic pointers.

---Down---
###Why ID-vectors?

---Down---
###Decompression statistics

---Right---
##Associative Memory

<div style="width: 100%;">
<img src="img/association_schematic.png" width="800">
</div>

---Right---
##Extraction Algorithm
####Putting it all together
<div style="width: 100%;">
<img src="img/extraction.png" width="800">
</div>

---Right---
##4. Neural Implementation

---Right---
#Neural Engineering Framework
####Activity of populations of neurons represent vectors, connection weight matrices perform transformations on those vectors

---Right---
<div style="width: 100%;">
  <div style="width: 50%; float: left;" class="fragment">
    <center><font color="blue">Neural Encoding</font></center><br><br>
    \begin{align}
      a\_{i}(\mathbf{x})=G\_{i}( \mathbf{e}\_i \mathbf{x} )
    \end{align}
  </div>
  <div style="margin-left: 50%;" class="fragment">
    <center><font color="blue">Neural Decoding</font></center><br><br>
    \begin{align}
    \widehat{f(\mathbf{x})}=\sum\_{i}a\_{i}\mathbf{(x)}\mathbf{d}^f\_{i}
    \end{align}
  </div>
</div>
<br>
<div style="width: 100%;">
  <div style="width: 50%; float: left;" class="fragment">
    <center><font color="blue">Finding Decoding Vectors</font></center>
    Minimize:<br><br>
    \begin{align}
      Error=&\ \frac{1}{2}\int(f(\mathbf{x})-\widehat{f(\mathbf{x})})^2d\mathbf{x}\\\\
      =&\ \frac{1}{2}\int(f(\mathbf{x})-\sum\_{i}a\_{i}(\mathbf{x)}\mathbf{d}\_{i}^{f})^{2}d\mathbf{x}
    \end{align}
  </div>

  <div style="margin-left: 50%;" class="fragment">
    <center><font color="blue">Derive connection weights</font></center>
    Implement non-linear function $f$ and linear transformlation $L$.<br><br>
    \begin{align}
        \omega\_{ij}=\mathbf{e}\_{j} \mathbf{L} \mathbf{d}\_{i}^f
    \end{align}
  </div>
</div>

---Down---
Populations of neurons represent vectors.

Populations have encoding vectors, and respond in proportion to the similarity
of the input vector to their encoding vector.

Populations have decoding vectors which allow us to reconstruct the vector
driving the population, or a function thereof.

Can construct weight matrix between two neural populations in terms of decoding
vectors of pre-synaptic population and encoding vectors of post-synaptic
population.

---Right---
<div style="position:relative; height:540px;">
  <img src="img/input.gif" width="400" height="400"
      style="position:absolute; top:58px; left:280px;">
  <img src="img/neuron1.gif" class="fragment" data-fragment-index="2"
      style="position:absolute; top:0; left:355px;">
  <img src="img/neuron2.gif" class="fragment" data-fragment-index="2"
      style="position:absolute; top:64px; left:580px;">
  <img src="img/neuron3.gif" class="fragment" data-fragment-index="2"
      style="position:absolute; top:244px; left:710px;">
  <img src="img/neuron4.gif" class="fragment" data-fragment-index="2"
      style="position:absolute; top:427px; left:580px;">
  <img src="img/neuron5.gif" class="fragment" data-fragment-index="2"
      style="position:absolute; top:490px; left:355px;">
  <img src="img/neuron6.gif" class="fragment" data-fragment-index="2"
      style="position:absolute; top:427px; left:130px;">
  <img src="img/neuron7.gif" class="fragment" data-fragment-index="2"
      style="position:absolute; top:244px; left:0px;">
  <img src="img/neuron8.gif" class="fragment" data-fragment-index="2"
      style="position:absolute; top:64px; left:130px;">
  <div id="neuron1" class="fragment" data-fragment-index="1"
      style="position:absolute; top:38px; left:470px;"></div>
  <div id="neuron2" class="fragment" data-fragment-index="1"
      style="position:absolute; top:100px; left:620px;"></div>
  <div id="neuron3" class="fragment" data-fragment-index="1"
      style="position:absolute; top:251px; left:685px;"></div>
  <div id="neuron4" class="fragment" data-fragment-index="1"
      style="position:absolute; top:403px; left:620px;"></div>
  <div id="neuron5" class="fragment" data-fragment-index="1"
      style="position:absolute; top:465px; left:470px;"></div>
  <div id="neuron6" class="fragment" data-fragment-index="1"
      style="position:absolute; top:403px; left:320px;"></div>
  <div id="neuron7" class="fragment" data-fragment-index="1"
      style="position:absolute; top:251px; left:256px;"></div>
  <div id="neuron8" class="fragment" data-fragment-index="1"
      style="position:absolute; top:100px; left:320px;"></div>
  <div class="fragment fade-in" data-fragment-index="1" id="encoders"
      style="position:absolute; top:74px; left:280px;"></div>
</div>

Input: $\mathbf{x}$,<br>

<span class="fragment" data-fragment-index="1">
Encoding vectors: $\mathbf{e_i}$,</span><br>

<span class="fragment" data-fragment-index="2">
Neural activity: $a\_{i}(\mathbf{x})=G\_{i}( \mathbf{e}\_i \mathbf{x} )$</span>


---Right---

<div style="display:inline-block;width:255px;">
  <img src="img/neuron1.gif">
  <img src="img/neuron2.gif">
  <img src="img/neuron3.gif">
  <img src="img/neuron4.gif">
  <img src="img/neuron5.gif">
  <img src="img/neuron6.gif">
  <img src="img/neuron7.gif">
  <img src="img/neuron8.gif">
</div>
<div class="fragment" style="display:inline-block;width:165px;" id="decoders" data-fragment-index="1"></div>
<div class="fragment" style="display:inline-block;position:relative;top:-36px;" data-fragment-index="1">
  <img src="img/estimate.gif" width="250">
  <p class="fragment">$$\hat{\mathbf{x}} = \sum_i d_i^I a_i$$</p>
</div>


---Right---

<div style="display:inline-block;width:255px;">
  <img src="img/neuron1.gif">
  <img src="img/neuron2.gif">
  <img src="img/neuron3.gif">
  <img src="img/neuron4.gif">
  <img src="img/neuron5.gif">
  <img src="img/neuron6.gif">
  <img src="img/neuron7.gif">
  <img src="img/neuron8.gif">
</div>
<div style="display:inline-block;width:165px;" id="decoders-2"></div>
<div style="display:inline-block;position:relative;top:-36px;">
  <img src="img/func.gif" width="250">
  $$\widehat{f(\mathbf{x})} = \sum_i d_i^f a_i$$
</div>



---Right---
##Circular Convolution
Can be written as element-wise multiplication ($\diamond$) in the Fourier space.
$\mathbf{x} \circledast \mathbf{y} = \mathbf{F}^{-1}( \mathbf{Fx} \diamond \mathbf{Fy} )$
<img src="img/convolution.png" width="80%">

---Right---
##Involution
A permutation, so is a linear operator, and a corresponding matrix $V$. Make
the convolution network compute $\mathbf{x} \cc{} \inverseop{y}$ instead of
$\mathbf{x} \cc{} \mathbf{y}$ with a small adjustment.
<img src="img/involution.png" width="80%">

---Right---
##Neural Associative Memory
Neural implementation of associative memory algorithm we saw earlier.
A small population is assigned to each pair $\pair{\xi_k}{\eta_k}$. Each population then has 3 jobs:

<ol>
<li>Compare input to $\xi_k$.</li>
<li>Threshold result.</li>
<li>Multiply $\eta_k$ by result.</li>
</ol>

Output should then be the summation of each of these populations.

---Right---
##Neural Associative Memory
<img src="img/neural_associative_memory.png" width="70%">

---Right---
##Complete Model
<img src="img/schematic.png" width="100%">
Neural populations labeled with values they represent when
$\hrr{H} = \vc{Q} \cc{} \id{T} + \vc{R} \cc{} \id{U}$ and $\vc{Q}$
given as input.

---Right---
##Neuron Count
<img src="img/schematic.png" width="40%">

50 neurons per dimension, 20 neurons per association population.<br>

Dark gray populations (512-D): $4 \times 512 \times 50$<br>
Light gray population (1028-D): $1 \times 1028 \times 50$<br>
Association populations: $117,659 \times 20$<br>

Total neurons: $2,506,980$<br>
Cortical area: $2,506,980~neurons / 170,000 \frac{neurons}{mm^2}^{\*}$<br>
$= 14.7 mm^2$<br>
$= 0.147 cm^2$ $<<$ previous approaches

-----

<small>$^{\*}$Chris Eliasmith. *How to Build a Brain.* Oxford University Press. New York, NY.
2013.</small>

---Right---
##5. Results

---Right---

<img src="img/prgraph.svg" width="80%">

---Right---
##6. Conclusion

1. First biologically plausible neural implementation of a human-scale knowledge-base.
2. Ability to scale can be a useful way to select theories.
3. Encourage theoretical debates to be replaced by concrete, large-scale implementations.

---Right---
##Acknowledgements
Thanks to my readers, members of the CNRGlab, NSERC, AFO.

Visualization of Past Approaches made by Terry Stewart.
NEF visualizations made by Trevor Bekolay and Xuan Choo.


