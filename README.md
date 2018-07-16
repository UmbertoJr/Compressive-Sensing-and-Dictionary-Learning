---


---

<h1 id="simple-introduction-to-compressive-sensing-and-dictionary-learning-on-python">Simple Introduction to Compressive Sensing and Dictionary Learning on Python</h1>
<p>An interesting Theory that recently I got to study is Compressive Sensing and Dictionary Learning, and here I will try to share some intuition that I had during my studies trying to keep thinghs easy and practical.</p>
<h2 id="what-is-compressive-sensing">What is Compressive Sensing?</h2>
<p>Compressive Sensing is a new Theory that after the First paper  <a href="http://statweb.stanford.edu/~candes/papers/ExactRecovery.pdf">Robust Uncertainty Principles: Exact Signal Reconstruction from Highly Incomplete Frequency Information</a> (June 2004) written by the noted <strong>Emmanuel Candes</strong>, <strong>Justin Romberg</strong> and <strong>Terence Tao</strong>, where they gived the proof that is possible to exactly recover an object from an incoplete frequency samples, by a convex optimization problem.</p>
<p>While the Second paper of Compressive Sensing history is <a href="http://statweb.stanford.edu/~donoho/Reports/2004/l1l0approx.pdf">For Most Large Underdetermined Systems of Equations, the Minimal ` 1 -norm Near-Solution Approximates the Sparsest Near-Solution</a> (August 2004) written by David L. Donoho; here we have the most famous approach to the problem, that is the one that use the inexact linear equation <a href="https://www.codecogs.com/eqnedit.php?latex=y&amp;space;\approx&amp;space;\Phi&amp;space;\cdot&amp;space;\alpha" target="_blank"><img src="https://latex.codecogs.com/gif.latex?y&amp;space;\approx&amp;space;\Phi&amp;space;\cdot&amp;space;\alpha" title="y \approx \Phi \cdot \alpha"></a>,<br>
where <a href="https://www.codecogs.com/eqnedit.php?latex=\Phi" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\Phi" title="\Phi"></a> is a given n by m matrix  and <a href="https://www.codecogs.com/eqnedit.php?latex=\alpha" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\alpha" title="\alpha"></a> is a sparse vector.<br>
In general this problem requires combinatorial optimization and so is considered intractable. But his convex-relaxation using  <a href="https://www.codecogs.com/eqnedit.php?latex=l_1" target="_blank"><img src="https://latex.codecogs.com/gif.latex?l_1" title="l_1"></a>-minimization is convex, and is totally tractable.</p>
<p><img src="image/obj_fun.png?raw=true" alt=""></p>
<p>If you want more go <a href="https://www.quora.com/What-are-the-seminal-papers-on-compressed-sensing">here </a></p>
<h2 id="lets-have-some-intuition-of-what-is-going-on....">Let’s have some intuition of what is going on…</h2>
<p>Let’s start to think what it means that <a href="https://www.codecogs.com/eqnedit.php?latex=y&amp;space;=&amp;space;\Phi&amp;space;\cdot&amp;space;\alpha" target="_blank"><img src="https://latex.codecogs.com/gif.latex?y&amp;space;=&amp;space;\Phi&amp;space;\cdot&amp;space;\alpha" title="y = \Phi \cdot \alpha"></a>,<br>
if <a href="https://www.codecogs.com/eqnedit.php?latex=\Phi" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\Phi" title="\Phi"></a> is n by n matrix is means that we have n hyper-planes of dimension n each one that, if they are linearly indipendent, they will end to identify a single point.<br>
Then if we have that <a href="https://www.codecogs.com/eqnedit.php?latex=\Phi" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\Phi" title="\Phi"></a> is (n-1) by n this system of equation will end on a line, and so on…<br>
More dimentions we remove from the row then more dimentions we give to the hiper-plane that is solution of the equations!!!<br>
So we could think that it seems that there is no single solution… but we should not forget that we want the solution to be the most sparse possible, and for this reason the solution exist and is only one.</p>
<p><img src="image/spaziosparso.png" alt="Sparse space"></p>
<p>At least since 0-norm is a NP-problem we transform the problem to convex using 1-norm</p>
<p><img src="image/normaP.png" alt="Norm p with p < 1"></p>
<h3 id="but-under-wich-conditions-is-it-possible-the-unique-and-complete-recovery">But under wich conditions is it possible the unique and complete recovery?</h3>
<blockquote>
<p>Theorem:<br>
Given <a href="https://www.codecogs.com/eqnedit.php?latex=A&amp;space;\in&amp;space;\mathbb{C}^{m&amp;space;\times&amp;space;N}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?A&amp;space;\in&amp;space;\mathbb{C}^{m&amp;space;\times&amp;space;N}" title="A \in \mathbb{C}^{m \times N}"></a>, the following properties are equivalent:<br>
a) If <a href="https://www.codecogs.com/eqnedit.php?latex=A&amp;space;\cdot&amp;space;x&amp;space;=&amp;space;A&amp;space;\cdot&amp;space;z" target="_blank"><img src="https://latex.codecogs.com/gif.latex?A&amp;space;\cdot&amp;space;x&amp;space;=&amp;space;A&amp;space;\cdot&amp;space;z" title="A \cdot x = A \cdot z"></a> and both are s-sparse, then <a href="https://www.codecogs.com/eqnedit.php?latex=x&amp;space;=&amp;space;z" target="_blank"><img src="https://latex.codecogs.com/gif.latex?x&amp;space;=&amp;space;z" title="x = z"></a>.<br>
b) The null-space of <a href="https://www.codecogs.com/eqnedit.php?latex=A" target="_blank"><img src="https://latex.codecogs.com/gif.latex?A" title="A"></a> does not contain any 2s-sparse vector other than the 0 vector<br>
c) Every set of 2s columns of <a href="https://www.codecogs.com/eqnedit.php?latex=A" target="_blank"><img src="https://latex.codecogs.com/gif.latex?A" title="A"></a> is linearly independent</p>
</blockquote>
<h2 id="recovery-algorithms">Recovery algorithms</h2>
<p>So up to now we talk about some theory, let’s start talk coding…</p>
<center><b>Basis Pursuit</b> </center>
<p>Consist in solve this simple convex problem:</p>
<p>&nbsp;</p>
<center>
<a href="https://www.codecogs.com/eqnedit.php?latex=\underset{x}{\text{minimize}}&amp;space;\quad&amp;space;||x||_1&amp;space;\\&amp;space;\text{subject&amp;space;to}&amp;space;\quad&amp;space;y&amp;space;=&amp;space;A&amp;space;\cdot&amp;space;x" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\underset{x}{\text{minimize}}&amp;space;\quad&amp;space;||x||_1&amp;space;\\&amp;space;\text{subject&amp;space;to}&amp;space;\quad&amp;space;y&amp;space;=&amp;space;A&amp;space;\cdot&amp;space;x" title="\underset{x}{\text{minimize}} \quad ||x||_1 \\ \text{subject to} \quad y = A \cdot x"></a>
</center>
<p>&nbsp;</p>
<center><b>Lasso</b> </center>
<p>Is the famous convex problem:</p>
<center>
<a href="https://www.codecogs.com/eqnedit.php?latex=\underset{x}{\text{minimize}}&amp;space;\quad&amp;space;||y&amp;space;-&amp;space;A&amp;space;\cdot&amp;space;x||_2&amp;space;\\&amp;space;\text{subject&amp;space;to}&amp;space;\quad&amp;space;||x||_1&amp;space;\leq&amp;space;\tau" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\underset{x}{\text{minimize}}&amp;space;\quad&amp;space;||y&amp;space;-&amp;space;A&amp;space;\cdot&amp;space;x||_2&amp;space;\\&amp;space;\text{subject&amp;space;to}&amp;space;\quad&amp;space;||x||_1&amp;space;\leq&amp;space;\tau" title="\underset{x}{\text{minimize}} \quad ||y - A \cdot x||_2 \\ \text{subject to} \quad ||x||_1 \leq \tau"></a></center>
<p>&nbsp;</p>
<center><b>Orthogonal Matching Pursuit</b> </center>
<p>It’s a greedy method that do the follow steps:</p>
<ul>
<li>
<p>Initialization:  <a href="https://www.codecogs.com/eqnedit.php?latex=S^0&amp;space;=&amp;space;\emptyset,&amp;space;\quad&amp;space;x^0&amp;space;=&amp;space;0" target="_blank"><img src="https://latex.codecogs.com/gif.latex?S^0&amp;space;=&amp;space;\emptyset,&amp;space;\quad&amp;space;x^0&amp;space;=&amp;space;0" title="S^0 = \emptyset, \quad x^0 = 0"></a></p>
</li>
<li>
<p>Repeat until a stopping criterion is met:</p>
</li>
</ul>
<center>
<a href="https://www.codecogs.com/eqnedit.php?latex=S^{n+1}&amp;space;=&amp;space;S^n&amp;space;\cup&amp;space;\{&amp;space;j_{n+1}\},&amp;space;\quad&amp;space;j_{n+1}=&amp;space;argmax\{|A^H(y-&amp;space;A\cdot&amp;space;x^n)|\}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?S^{n+1}&amp;space;=&amp;space;S^n&amp;space;\cup&amp;space;\{&amp;space;j_{n+1}\},&amp;space;\quad&amp;space;j_{n+1}=&amp;space;argmax\{|A^H(y-&amp;space;A\cdot&amp;space;x^n)|\}" title="S^{n+1} = S^n \cup \{ j_{n+1}\}, \quad j_{n+1}= argmax\{|A^H(y- A\cdot x^n)|\}"></a>
</center>
<center>
<a href="https://www.codecogs.com/eqnedit.php?latex=x^{n+1}&amp;space;=&amp;space;argmin_z\{|y&amp;space;-&amp;space;A&amp;space;\cdot&amp;space;z|_2&amp;space;,&amp;space;supp(z)&amp;space;\subset&amp;space;S^{n+1}\}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?x^{n+1}&amp;space;=&amp;space;argmin_z\{|y&amp;space;-&amp;space;A&amp;space;\cdot&amp;space;z|_2&amp;space;,&amp;space;supp(z)&amp;space;\subset&amp;space;S^{n+1}\}" title="x^{n+1} = argmin_z\{|y - A \cdot z|_2 , supp(z) \subset S^{n+1}\}"></a>
</center>
<ul>
<li>Output <a href="https://www.codecogs.com/eqnedit.php?latex=x^*&amp;space;=&amp;space;x^{n+1}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?x^*&amp;space;=&amp;space;x^{n+1}" title="x^* = x^{n+1}"></a></li>
</ul>

