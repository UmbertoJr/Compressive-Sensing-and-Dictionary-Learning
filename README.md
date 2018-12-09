---


---

<h1 id="simple-introduction-to-compressive-sensing-and-dictionary-learning">Simple Introduction to Compressive Sensing and Dictionary Learning</h1>
<p>An interesting Theory that recently I got to study is Compressive Sensing and Dictionary Learning, and here I will share with you some intuition that I had during my studies trying to keep thighs easy and practical.<br>
I made also a <a href="https://prezi.com/view/ft9eVbTF8aYyHALbDxMX/">Presentation</a> to  Compressive Sensing and Dictionary Learning and here you can also find my <a href="https://github.com/UmbertoJr/Compressive_Sensing_and_Dictionary_Learning/blob/master/CompressiveSensing_and_DictionaryLearning.ipynb">Jupyter Notebook</a> repository on this topic (I suggest you run it on <a href="https://colab.research.google.com/notebooks/welcome.ipynb">colaboratory</a>).</p>
<h2 id="what-is-compressive-sensing-compressive-sensing-is-a-new">What is Compressive Sensing? </h2>
Compressive Sensing is a new <p> Theory that after the First paper <a href="http://statweb.stanford.edu/~candes/papers/ExactRecovery.pdf">Robust Uncertainty Principles: Exact Signal Reconstruction from Highly Incomplete Frequency Information</a> (June 2004) written by the noted <strong>Emmanuel Candes</strong>, <strong>Justin Romberg</strong> and <strong>Terence Tao</strong>, where they gave the proof that is possible to exactly recover an object from an incomplete frequency samples, by a convex optimization problem.<br>
While the Second paper of Compressive Sensing history is <a href="http://statweb.stanford.edu/~donoho/Reports/2004/l1l0approx.pdf">For Most Large Underdetermined Systems of Equations, the Minimal ` 1 -norm Near-Solution Approximates the Sparsest Near-Solution</a> (August 2004) written by David L. Donoho; here we have the most famous approach to the problem, that is the one that use the inexact linear equation <a href="https://www.codecogs.com/eqnedit.php?latex=y&amp;space;\approx&amp;space;\Phi&amp;space;\cdot&amp;space;\alpha" target="_blank"><img src="https://latex.codecogs.com/gif.latex?y&amp;space;\approx&amp;space;\Phi&amp;space;\cdot&amp;space;\alpha" title="y \approx \Phi \cdot \alpha"></a>, where <a href="https://www.codecogs.com/eqnedit.php?latex=\Phi" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\Phi" title="\Phi"></a> is a given n by m matrix and <a href="https://www.codecogs.com/eqnedit.php?latex=\alpha" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\alpha" title="\alpha"></a> is a sparse vector.  In general this problem requires combinatorial optimization and so is considered intractable. But his convex-relaxation using <a href="https://www.codecogs.com/eqnedit.php?latex=l_1" target="_blank"><img src="https://latex.codecogs.com/gif.latex?l_1" title="l_1"></a>-minimization is convex, and is totally tractable.</p>
<p><img src="image/obj_fun.png?raw=true" alt=""><br>
If you want more go <a href="https://www.quora.com/What-are-the-seminal-papers-on-compressed-sensing">here </a></p>
<h2 id="lets-have-some-intuition-of-what-is-going-on...">Let’s have some intuition of what is going on…</h2>
<p>Let’s start to think what it means that <a href="https://www.codecogs.com/eqnedit.php?latex=y&amp;space;=&amp;space;\Phi&amp;space;\cdot&amp;space;\alpha" target="_blank"><img src="https://latex.codecogs.com/gif.latex?y&amp;space;=&amp;space;\Phi&amp;space;\cdot&amp;space;\alpha" title="y = \Phi \cdot \alpha"></a>,  if <a href="https://www.codecogs.com/eqnedit.php?latex=\Phi" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\Phi" title="\Phi"></a> is n by n matrix is means that we have n hyper-planes of dimension n each one that, if they are linearly indipendent, they will end to identify a single point. Then if we have that <a href="https://www.codecogs.com/eqnedit.php?latex=\Phi" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\Phi" title="\Phi"></a> is (n-1) by n this system of equation will end on a line, and so on…<br>
More dimensions we remove from the row then more dimensions we give to the hiper-plane that is the solution of the equations!!!<br>
So we could think that it seems that there is no single solution… but we should not forget that we want the solution to be the most sparse possible, and for this reason, the solution exists and is only one.</p>
<p><img src="image/spaziosparso.png" alt="Sparse space"></p>
<p>At least since 0-norm is an NP-problem we transform the problem to convex using 1-norm<br>
<img src="image/normaP.png" alt="Norm p with p < 1"></p>
<h3 id="but-under-which-conditions-is-it-possible-the-unique-and-complete-recovery">But under which conditions is it possible the unique and complete recovery?</h3>
<blockquote>
<p>Theorem:<br>
Given <a href="https://www.codecogs.com/eqnedit.php?latex=A&amp;space;\in&amp;space;\mathbb{C}^{m&amp;space;\times&amp;space;N}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?A&amp;space;\in&amp;space;\mathbb{C}^{m&amp;space;\times&amp;space;N}" title="A \in \mathbb{C}^{m \times N}"></a>, the following properties are equivalent:</p>
<blockquote>
<p>a) If <a href="https://www.codecogs.com/eqnedit.php?latex=A&amp;space;\cdot&amp;space;x&amp;space;=&amp;space;A&amp;space;\cdot&amp;space;z" target="_blank"><img src="https://latex.codecogs.com/gif.latex?A&amp;space;\cdot&amp;space;x&amp;space;=&amp;space;A&amp;space;\cdot&amp;space;z" title="A \cdot x = A \cdot z"></a> and both are s-sparse, then <a href="https://www.codecogs.com/eqnedit.php?latex=x&amp;space;=&amp;space;z" target="_blank"><img src="https://latex.codecogs.com/gif.latex?x&amp;space;=&amp;space;z" title="x = z"></a>.</p>
</blockquote>
<blockquote>
<p>b) The null-space of <a href="https://www.codecogs.com/eqnedit.php?latex=A" target="_blank"><img src="https://latex.codecogs.com/gif.latex?A" title="A"></a> does not contain any 2s-sparse vector other than the 0 vector</p>
</blockquote>
<blockquote>
<p>c) Every set of 2s columns of <a href="https://www.codecogs.com/eqnedit.php?latex=A" target="_blank"><img src="https://latex.codecogs.com/gif.latex?A" title="A"></a> is linearly independent</p>
</blockquote>
</blockquote>
<h2 id="recovery-algorithms">Recovery algorithms</h2>
<p>So up to now, we talk about some theory, let’s start talk coding…</p>
 <center><b>Basis Pursuit</b> </center> 
  Consist in solve this simple convex problem:  &nbsp;
    <center> <a href="https://www.codecogs.com/eqnedit.php?latex=\underset{x}{\text{minimize}}&amp;space;\quad&amp;space;||x||_1&amp;space;\\&amp;space;\text{subject&amp;space;to}&amp;space;\quad&amp;space;y&amp;space;=&amp;space;A&amp;space;\cdot&amp;space;x" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\underset{x}{\text{minimize}}&amp;space;\quad&amp;space;||x||_1&amp;space;\\&amp;space;\text{subject&amp;space;to}&amp;space;\quad&amp;space;y&amp;space;=&amp;space;A&amp;space;\cdot&amp;space;x" title="\underset{x}{\text{minimize}} \quad ||x||_1 \\ \text{subject to} \quad y = A \cdot x"></a> </center>   &nbsp;  <center><b>Lasso</b> </center>  Is the famous convex problem:  <center> <a href="https://www.codecogs.com/eqnedit.php?latex=\underset{x}{\text{minimize}}&amp;space;\quad&amp;space;||y&amp;space;-&amp;space;A&amp;space;\cdot&amp;space;x||_2&amp;space;\\&amp;space;\text{subject&amp;space;to}&amp;space;\quad&amp;space;||x||_1&amp;space;\leq&amp;space;\tau" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\underset{x}{\text{minimize}}&amp;space;\quad&amp;space;||y&amp;space;-&amp;space;A&amp;space;\cdot&amp;space;x||_2&amp;space;\\&amp;space;\text{subject&amp;space;to}&amp;space;\quad&amp;space;||x||_1&amp;space;\leq&amp;space;\tau" title="\underset{x}{\text{minimize}} \quad ||y - A \cdot x||_2 \\ \text{subject to} \quad ||x||_1 \leq \tau"></a></center>   &nbsp;  <center><b>Orthogonal Matching Pursuit</b> </center> 
     It's a greedy method that do the follow steps: 
<ul>
<li>
<p>Initialization: <a href="https://www.codecogs.com/eqnedit.php?latex=S^0&amp;space;=&amp;space;\emptyset,&amp;space;\quad&amp;space;x^0&amp;space;=&amp;space;0" target="_blank"><img src="https://latex.codecogs.com/gif.latex?S^0&amp;space;=&amp;space;\emptyset,&amp;space;\quad&amp;space;x^0&amp;space;=&amp;space;0" title="S^0 = \emptyset, \quad x^0 = 0"></a></p>
</li>
<li>
<p>Repeat until a stopping criterion is met: </p><center> <a href="https://www.codecogs.com/eqnedit.php?latex=S^{n+1}&amp;space;=&amp;space;S^n&amp;space;\cup&amp;space;\{&amp;space;j_{n+1}\},&amp;space;\quad&amp;space;j_{n+1}=&amp;space;argmax\{|A^H(y-&amp;space;A\cdot&amp;space;x^n)|\}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?S^{n+1}&amp;space;=&amp;space;S^n&amp;space;\cup&amp;space;\{&amp;space;j_{n+1}\},&amp;space;\quad&amp;space;j_{n+1}=&amp;space;argmax\{|A^H(y-&amp;space;A\cdot&amp;space;x^n)|\}" title="S^{n+1} = S^n \cup \{ j_{n+1}\}, \quad j_{n+1}= argmax\{|A^H(y- A\cdot x^n)|\}"></a> </center>  <center> <a href="https://www.codecogs.com/eqnedit.php?latex=x^{n+1}&amp;space;=&amp;space;argmin_z\{|y&amp;space;-&amp;space;A&amp;space;\cdot&amp;space;z|_2&amp;space;,&amp;space;supp(z)&amp;space;\subset&amp;space;S^{n+1}\}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?x^{n+1}&amp;space;=&amp;space;argmin_z\{|y&amp;space;-&amp;space;A&amp;space;\cdot&amp;space;z|_2&amp;space;,&amp;space;supp(z)&amp;space;\subset&amp;space;S^{n+1}\}" title="x^{n+1} = argmin_z\{|y - A \cdot z|_2 , supp(z) \subset S^{n+1}\}"></a> </center><p></p>
</li>
<li>
<p>Output <a href="https://www.codecogs.com/eqnedit.php?latex=x^*&amp;space;=&amp;space;x^{n+1}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?x^*&amp;space;=&amp;space;x^{n+1}" title="x^* = x^{n+1}"></a></p>
<h1 id="dictionary-learning">Dictionary Learning</h1>
</li>
</ul>
<p>It’s a collection of algorithms focused on building, from some training data, a set of atoms/vectors that span a new space with the characteristic that the representation of the signal in such space is given by a sparse vector and each atom don’t need to be orthogonal to the other ones like for example in PCA.</p>
<p>So it’s also a method useful to build the matrix <a href="https://www.codecogs.com/eqnedit.php?latex=\Phi" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\Phi" title="\Phi"></a> that we used previously in the Compressive Sensing Theory .<br>
And to solve this task we need to solve the following optimization problem:</p>
<center>
<a href="https://www.codecogs.com/eqnedit.php?latex=\underset{x,&amp;space;D}{\text{minimize}}&amp;space;\quad&amp;space;\sum_i&amp;space;||&amp;space;y(i)&amp;space;-D&amp;space;\cdot&amp;space;x(i)&amp;space;||_2&amp;space;+&amp;space;\lambda&amp;space;||x(i)||_1&amp;space;\\&amp;space;\text{subject&amp;space;to}&amp;space;\quad&amp;space;\quad&amp;space;\quad&amp;space;||D(j)||_2&amp;space;=&amp;space;1,&amp;space;\quad&amp;space;\forall&amp;space;j" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\underset{x,&amp;space;D}{\text{minimize}}&amp;space;\quad&amp;space;\sum_i&amp;space;||&amp;space;y(i)&amp;space;-D&amp;space;\cdot&amp;space;x(i)&amp;space;||_2&amp;space;+&amp;space;\lambda&amp;space;||x(i)||_1&amp;space;\\&amp;space;\text{subject&amp;space;to}&amp;space;\quad&amp;space;\quad&amp;space;\quad&amp;space;||D(j)||_2&amp;space;=&amp;space;1,&amp;space;\quad&amp;space;\forall&amp;space;j" title="\underset{x, D}{\text{minimize}} \quad \sum_i || y(i) -D \cdot x(i) ||_2 + \lambda ||x(i)||_1 \\ \text{subject to} \quad \quad \quad ||D(j)||_2 = 1, \quad \forall j"></a>
</center>
<p>This is, of course, a non-convex optimization problem since the objective is non-convex.</p>
<h3 id="how-to-solve-this-type-of-non-convex-problem">How to solve this type of non-convex problem?</h3>
<p>In literature there are many different approaches to this problem and we will see just two of them:</p>
<center> <b>Method of Optimal Directions (MOD)</b></center>
<p>It consist simply in solve the sparse coding problem with one of the methods previously seen like <strong>Lasso</strong> and after updating the dictionary by computing the analytical solution of the problem given by <a href="https://www.codecogs.com/eqnedit.php?latex=D=XR^+" target="_blank"><img src="https://latex.codecogs.com/gif.latex?D=XR^+" title="D=XR^+"></a> where the + is for the <strong>Moore-Penrose pseudoinverse</strong>.<br>
After this update D need to be renormalized to fit the constraints and this algorithm is recursive up to convergence.</p>
<center> <b>   Online Dictionary Learning    </b></center>
<p>When the size of the training size is too big or when the input data come in form of a stream, in such cases we are in the field of study of <strong>online learning</strong> which essentially suggests iteratively updating the model upon the new data points x becoming available.</p>
<p>This method allows us to gradually update the dictionary as new data becomes available for sparse representation learning and helps drastically reduce the amount of memory needed to store the dataset (which often has a huge size).<br>
The implementation of this algorithm is taken by the paper <a href="http://www.di.ens.fr/sierra/pdfs/icml09.pdf">Online Dictionary Learning for Sparse Coding</a> by Julien Mairal, Francis Bach, Jean Ponce, Guillermo Sapiro.</p>
<p><img src="image/OnlineAlgo.png" alt="online algorithm"></p>
<p><img src="image/Dictionary_Update.png" alt="Dictionary update"></p>
<p><em><strong>Thank you for reading and I remember you to star my repo and see the <a href="https://github.com/UmbertoJr/Compressive_Sensing_and_Dictionary_Learning/blob/master/CompressiveSensing_and_DictionaryLearning.ipynb">jupyter notebook</a> on colab</strong></em></p>

