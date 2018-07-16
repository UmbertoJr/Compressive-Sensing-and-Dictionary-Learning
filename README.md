---


---

<h1 id="simple-introduction-to-compressive-sensing-and-dictionary-learning-on-python">Simple Introduction to Compressive Sensing and Dictionary Learning on Python</h1>
<p>An interesting Theory that recently I got to study is Compressive Sensing and Dictionary Learning, and here I will try to share some intuition that I had during my studies trying to keep thinghs easy and practical.</p>
<h2 id="what-is-compressive-sensing">What is Compressive Sensing?</h2>
<p>Compressive Sensing is a new Theory that after the First paper  <a href="http://statweb.stanford.edu/~candes/papers/ExactRecovery.pdf">Robust Uncertainty Principles: Exact Signal Reconstruction from Highly Incomplete Frequency Information</a> (June 2004) written by the noted <strong>Emmanuel Candes</strong>, <strong>Justin Romberg</strong> and <strong>Terence Tao</strong>, where they gived the proof that is possible to exactly recover an object from an incoplete frequency samples, by a convex optimization problem.</p>
<p>While the Second paper of Compressive Sensing history is <a href="http://statweb.stanford.edu/~donoho/Reports/2004/l1l0approx.pdf">For Most Large Underdetermined Systems of Equations, the Minimal ` 1 -norm Near-Solution Approximates the Sparsest Near-Solution</a> (August 2004) written by David L. Donoho; here we have the most famous approach to the problem, that is the one that use the inexact linear equation <a href="https://www.codecogs.com/eqnedit.php?latex=y&amp;space;\approx&amp;space;\Phi&amp;space;\cdot&amp;space;\alpha" target="_blank"><img src="https://latex.codecogs.com/gif.latex?y&amp;space;\approx&amp;space;\Phi&amp;space;\cdot&amp;space;\alpha" title="y \approx \Phi \cdot \alpha"></a>,<br>
where <a href="https://www.codecogs.com/eqnedit.php?latex=\Phi" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\Phi" title="\Phi"></a> is a given n by m  and <a href="https://www.codecogs.com/eqnedit.php?latex=\alpha" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\alpha" title="\alpha"></a> is a sparse vector.<br>
In general this problem requires combinatorial optimization and so is considered intractable. But his convex-relaxation using  <a href="https://www.codecogs.com/eqnedit.php?latex=l_1" target="_blank"><img src="https://latex.codecogs.com/gif.latex?l_1" title="l_1"></a>-minimization is convex, and is totally tractable.</p>
<p><img src="image/obj_fun.png?raw=true" alt=""></p>
<p>If you want more go <a href="https://www.quora.com/What-are-the-seminal-papers-on-compressed-sensing">here </a></p>
<h2 id="lets-have-some-intuition-of-what-is-going-on....">Let’s have some intuition of what is going on…</h2>
<p>Let’s start to think what it means that y = Phi * alpha,<br>
if <a href="https://www.codecogs.com/eqnedit.php?latex=\Phi" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\Phi" title="\Phi"></a> is n by n matrix is means that we have n hyper-planes of dimension n each one that, if they are linearly indipendent, they will end to identify a single point.<br>
Then if we have that Phi is (n-1) by n this system of equation will end on a line, and so on…<br>
More dimentions we remove from the row then more dimentions we give to the hiper-plane that is solution of the equations!!!<br>
So we could think that it seems that there is no single solution… but we should not forget that we want the solution to be the most sparse possible, and for this reason the solution exist and is only one.</p>
<p><img src="image/spaziosparso.png" alt="Sparse space"></p>
<p>At least since 0-norm is a NP-problem we transform the problem to convex using 1-norm</p>
<p><img src="image/normaP.png" alt="Norm p with p < 1"></p>

