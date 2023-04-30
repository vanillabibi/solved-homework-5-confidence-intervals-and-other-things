Download Link: https://assignmentchef.com/product/solved-homework-5-confidence-intervals-and-other-things
<br>
5/5 - (4 votes)




Your solutions to theoretical questions should be done in Markdown/MathJax directly below the associated question. Your solutions to computational questions should include any specified Python code and results as well as written commentary on your conclusions. Remember that you are encouraged to discuss the problems with your instructors and classmates, but <strong>you must write all code and solutions on your own</strong>.

<strong>NOTES</strong>:

<ul>

 <li>Do <strong>NOT</strong> load or use any Python packages that are not available in Anaconda 3.6.</li>

 <li>Some problems with code may be autograded. If we provide a function API <strong>do not</strong> change it. If we do not provide a function API then you’re free to structure your code however you like.</li>

 <li>Because you can technically evaluate notebook cells is a non-linear order, it’s a good idea to do Cell <img decoding="async" class="math math-inline" src="https://render.githubusercontent.com/render/math?math=%5Crightarrow&amp;mode=inline" alt="$rightarrow$"> Run All as a check before submitting your solutions. That way if we need to run your code you will know that it will work as expected.</li>

 <li>Submit only this Jupyter notebook to Moodle. Do not compress it using tar, rar, zip, etc.</li>

 <li>This should go without saying, but… For any question that asks you to calculate something, you <strong>must show all work to receive credit</strong>. Sparse or nonexistent work will receive sparse or nonexistent credit.</li>

</ul>

<hr>

<strong>Shortcuts:</strong> <a href="https://render.githubusercontent.com/view/ipynb?commit=463e2f80e1978d1ed5c55c0225f63c6dcc626b21&amp;enc_url=68747470733a2f2f7261772e67697468756275736572636f6e74656e742e636f6d2f64626c617272656d6f72652f63736369333032322f343633653266383065313937386431656435633535633032323566363363366463633632366232312f686f6d65776f726b2f686f6d65776f726b352f686d776b30355f4c6173744e616d655f46697273744e616d652e6970796e62&amp;nwo=dblarremore%2Fcsci3022&amp;path=homework%2Fhomework5%2Fhmwk05_LastName_FirstName.ipynb&amp;repository_id=145737840&amp;repository_type=Repository#p1">Problem 1</a> | <a href="https://render.githubusercontent.com/view/ipynb?commit=463e2f80e1978d1ed5c55c0225f63c6dcc626b21&amp;enc_url=68747470733a2f2f7261772e67697468756275736572636f6e74656e742e636f6d2f64626c617272656d6f72652f63736369333032322f343633653266383065313937386431656435633535633032323566363363366463633632366232312f686f6d65776f726b2f686f6d65776f726b352f686d776b30355f4c6173744e616d655f46697273744e616d652e6970796e62&amp;nwo=dblarremore%2Fcsci3022&amp;path=homework%2Fhomework5%2Fhmwk05_LastName_FirstName.ipynb&amp;repository_id=145737840&amp;repository_type=Repository#p2">Problem 2</a> | <a href="https://render.githubusercontent.com/view/ipynb?commit=463e2f80e1978d1ed5c55c0225f63c6dcc626b21&amp;enc_url=68747470733a2f2f7261772e67697468756275736572636f6e74656e742e636f6d2f64626c617272656d6f72652f63736369333032322f343633653266383065313937386431656435633535633032323566363363366463633632366232312f686f6d65776f726b2f686f6d65776f726b352f686d776b30355f4c6173744e616d655f46697273744e616d652e6970796e62&amp;nwo=dblarremore%2Fcsci3022&amp;path=homework%2Fhomework5%2Fhmwk05_LastName_FirstName.ipynb&amp;repository_id=145737840&amp;repository_type=Repository#p3">Problem 3</a> | <a href="https://render.githubusercontent.com/view/ipynb?commit=463e2f80e1978d1ed5c55c0225f63c6dcc626b21&amp;enc_url=68747470733a2f2f7261772e67697468756275736572636f6e74656e742e636f6d2f64626c617272656d6f72652f63736369333032322f343633653266383065313937386431656435633535633032323566363363366463633632366232312f686f6d65776f726b2f686f6d65776f726b352f686d776b30355f4c6173744e616d655f46697273744e616d652e6970796e62&amp;nwo=dblarremore%2Fcsci3022&amp;path=homework%2Fhomework5%2Fhmwk05_LastName_FirstName.ipynb&amp;repository_id=145737840&amp;repository_type=Repository#p4">Problem 4</a>

<hr>

In [ ]:

<pre><span class="kn">import</span> <span class="nn">numpy</span> <span class="k">as</span> <span class="nn">np</span><span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="k">as</span> <span class="nn">plt</span><span class="kn">import</span> <span class="nn">pandas</span> <span class="k">as</span> <span class="nn">pd</span><span class="kn">import</span> <span class="nn">scipy.stats</span> <span class="k">as</span> <span class="nn">stats</span><span class="o">%</span><span class="n">matplotlib</span> <span class="n">inline</span></pre>

<hr>

<a href="https://render.githubusercontent.com/view/ipynb?commit=463e2f80e1978d1ed5c55c0225f63c6dcc626b21&amp;enc_url=68747470733a2f2f7261772e67697468756275736572636f6e74656e742e636f6d2f64626c617272656d6f72652f63736369333032322f343633653266383065313937386431656435633535633032323566363363366463633632366232312f686f6d65776f726b2f686f6d65776f726b352f686d776b30355f4c6173744e616d655f46697273744e616d652e6970796e62&amp;nwo=dblarremore%2Fcsci3022&amp;path=homework%2Fhomework5%2Fhmwk05_LastName_FirstName.ipynb&amp;repository_id=145737840&amp;repository_type=Repository#top">Back to top</a>

<h3>[30 points] Problem 1 – Sea-level rise, schmee-level rise!</h3>

You have been contacted by the local government of Key West, Florida, to assess whether there is statistical evidence for sea-level rise in the area. You obtain from the University of Hawaii Sea Level Center’s <a href="https://uhslc.soest.hawaii.edu/data/?rq">gigantic repository of sea-level data</a> the daily mean sea levels file <a href="https://piazza.com/class_profile/get_resource/jhaqogsdelf76h/jixzm0rl5dp6y4">linked here</a> and below.

In this problem, you will:

<ol>

 <li>practice calculating confidence intervals,</li>

 <li>practice wrangling a real-life data set into a form where you can actually compute these confidence intervals, because life will rarely be so kind as to simply hand you a nicely packaged and cleaned set of data, and</li>

 <li>save Key West from a watery fate?</li>

</ol>

In [ ]:

<pre><span class="c1"># Local and web paths to the data; pick which works for you.</span><span class="n">local_path</span> <span class="o">=</span> <span class="s2">"data/sealevel_keywest.csv"</span><span class="n">web_path</span>   <span class="o">=</span> <span class="s2">"https://raw.githubusercontent.com/dblarremore/csci3022/master/homework/homework5/data/sealevel_keywest.csv"</span><span class="n">file_path</span>  <span class="o">=</span> <span class="n">local_path</span><span class="n">dfSL</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="n">file_path</span><span class="p">,</span> <span class="n">header</span><span class="o">=</span><span class="kc">None</span><span class="p">)</span><span class="n">dfSL</span><span class="o">.</span><span class="n">rename</span><span class="p">(</span><span class="n">columns</span><span class="o">=</span><span class="p">{</span><span class="mi">0</span> <span class="p">:</span> <span class="s1">'Year'</span><span class="p">,</span> <span class="mi">1</span> <span class="p">:</span> <span class="s1">'Month'</span><span class="p">,</span> <span class="mi">2</span> <span class="p">:</span> <span class="s1">'Day'</span><span class="p">,</span> <span class="mi">3</span> <span class="p">:</span> <span class="s1">'SL'</span><span class="p">},</span> <span class="n">inplace</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span><span class="n">dfSL</span><span class="o">.</span><span class="n">head</span><span class="p">()</span></pre>

<strong>Part A:</strong> Write a function <code>clean_data</code> to:

<ol>

 <li>take in a single argument of a raw sea level data frame (e.g., <code>dfSL</code> above),</li>

 <li>compute the fill-value used to replace missing sea level (SL) data (<strong>not</strong> hard-coded!),</li>

 <li>use the Pandas <code>DataFrame.dropna</code> method to remove all missing rows of data,</li>

 <li>select only the data point on the second day of each month, and</li>

 <li>return a cleaned Pandas data frame.</li>

</ol>

Use your shiny new function to clean the <code>dfSL</code> data frame and save the results in a new data frame.

There is a very specific reason to sample only one daily data point per month. We will talk about it later.

In [ ]:

<pre><span class="k">def</span> <span class="nf">clean_data</span><span class="p">(</span><span class="n">df</span><span class="p">):</span>        <span class="c1"># your code goes here!</span>    <span class="n">dfClean</span> <span class="o">=</span> <span class="n">df</span>        <span class="k">return</span> <span class="n">dfClean</span><span class="n">dfClean</span> <span class="o">=</span> <span class="n">clean_data</span><span class="p">(</span><span class="n">dfSL</span><span class="p">)</span><span class="n">dfClean</span><span class="o">.</span><span class="n">head</span><span class="p">()</span></pre>

<strong>Part B:</strong> Plot the cleaned time series of sea levels. Be sure to label your axes, including units. The UHSLC data portal includes a link to the metadata accompanying our data set; if you are not sure about units, that would be a good place to start looking. For the <img decoding="async" class="math math-inline" src="https://render.githubusercontent.com/render/math?math=x&amp;mode=inline" alt="$x$">-axis, place the <img decoding="async" class="math math-inline" src="https://render.githubusercontent.com/render/math?math=x&amp;mode=inline" alt="$x$"> tick marks on January 2 of each year that is divisible by 10 (i.e., 1920, 1930, …), and label with that year. You may need to do additional processing in order to grab these indices.

<strong>Bonus challenge (0 points):</strong> Why do we choose to work with the second day of each month instead of the first? You may need to look at the original data set to answer this.

In [ ]:

<pre></pre>

<strong>Part C:</strong> Use your cleaned sea levels data frame to create two new Pandas data frames or series:

<ol>

 <li>one object to contain the sea levels between (and including) the years 1986 and 1995, and</li>

 <li>another object to contain the sea levels between (and including) the years 2006 and 2015.</li>

</ol>

Then, create a single-panel figure that includes density histograms of each decade of sea levels. Be sure to label everything appropriately.

Finally, based on the data in front of you, formulate and state a hypothesis about how the mean sea level in the decade 2006-2015 compares to the mean sea level in the decade 1986-1995.

In [ ]:

<pre></pre>

<strong>Part D:</strong> Compute a 99.9% confidence interval for each of (1) the mean sea level in the 1986-1995 decade (<img decoding="async" class="math math-inline" src="https://render.githubusercontent.com/render/math?math=%5Cmu_%7B1986-1995%7D&amp;mode=inline" alt="$mu_{1986-1995}$">) and (2) the mean sea level in the 2006-2015 decade (<img decoding="async" class="math math-inline" src="https://render.githubusercontent.com/render/math?math=%5Cmu_%7B2006-2015%7D&amp;mode=inline" alt="$mu_{2006-2015}$">). You may use Python for arithmetic operations and executing the calculations, but the relevant steps/set-up should be displayed in Markdown/MathJax.

Based on these two confidence intervals, do you think there is sufficient evidence to conclude that there is or is not a significant difference in the mean sea level between 1986-1995 and 2006-2015? Justify your answer.

In [ ]:

<pre></pre>

<strong>Part E:</strong> Compute a 99.9% confidence interval for the <strong><em>difference in mean sea level</em></strong> between the 2006-2015 and the 1986-1995 decades (<img decoding="async" class="math math-inline" src="https://render.githubusercontent.com/render/math?math=%5Cmu_%7B2006-2015%7D%20-%20%5Cmu_%7B1986-1995%7D&amp;mode=inline" alt="$mu_{2006-2015} - mu_{1986-1995}$">. Based on this, make a conclusion regarding your hypothesis from <strong>Part C</strong>, and compare to what your results in <strong>Part D</strong> implied. You may use Python for arithmetic operations and executing the calculations, but the relevant steps/set-up should be displayed in Markdown/MathJax.

In [ ]:

<pre></pre>

<strong>Part F:</strong> The confidence intervals from <strong>Parts D</strong> and <strong>E</strong> were derived using the Central Limit Theorem. Which assumption of the Central Limit Theorem would likely be violated if we took more than one measurement per month to form our samples, and why?

<hr>

<a href="https://render.githubusercontent.com/view/ipynb?commit=463e2f80e1978d1ed5c55c0225f63c6dcc626b21&amp;enc_url=68747470733a2f2f7261772e67697468756275736572636f6e74656e742e636f6d2f64626c617272656d6f72652f63736369333032322f343633653266383065313937386431656435633535633032323566363363366463633632366232312f686f6d65776f726b2f686f6d65776f726b352f686d776b30355f4c6173744e616d655f46697273744e616d652e6970796e62&amp;nwo=dblarremore%2Fcsci3022&amp;path=homework%2Fhomework5%2Fhmwk05_LastName_FirstName.ipynb&amp;repository_id=145737840&amp;repository_type=Repository#top">Back to top</a>

<h3>[25 points] Problem 2 – Quality of Red vs White Wine</h3>

<strong>Part A:</strong> Load the data in <a href="https://piazza.com/class_profile/get_resource/jhaqogsdelf76h/jixzm1ebc6q6ye"><code>winequalityred.csv</code></a> and <a href="https://piazza.com/class_profile/get_resource/jhaqogsdelf76h/jixzm17x9pu6y9"><code>winequalitywhite.csv</code></a> into Pandas DataFrames. They are available under Resources on Piazza, and linked here and below. A description of this dataset can be found on <a href="https://archive.ics.uci.edu/ml/datasets/Wine+Quality">UC Irvine’s Machine Learning Repository</a>. The quantity of interest for this problem is the quality of the wine.

Are we justified in using the Central Limit Theorem in our analysis of estimates of the mean and proportions of the data? Justify your response.

In [ ]:

<pre><span class="c1"># read either local or web file version; pick whichever works for you</span><span class="n">local_file_white</span> <span class="o">=</span> <span class="s2">"data/winequality-white.csv"</span><span class="n">local_file_red</span>   <span class="o">=</span> <span class="s2">"data/winequality-red.csv"</span><span class="n">web_file_white</span> <span class="o">=</span> <span class="s2">"https://raw.githubusercontent.com/dblarremore/csci3022/master/homework/homework5/data/winequality-white.csv"</span><span class="n">web_file_red</span>   <span class="o">=</span> <span class="s2">"https://raw.githubusercontent.com/dblarremore/csci3022/master/homework/homework5/data/winequality-red.csv"</span><span class="n">dfRed</span>   <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="n">local_file_red</span><span class="p">,</span> <span class="n">delimiter</span><span class="o">=</span><span class="s1">';'</span><span class="p">)</span><span class="n">dfWhite</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="n">local_file_white</span><span class="p">,</span> <span class="n">delimiter</span><span class="o">=</span><span class="s1">';'</span><span class="p">)</span></pre>

In [ ]:

<pre></pre>

<strong>Part B:</strong> Let <img decoding="async" class="math math-inline" src="https://render.githubusercontent.com/render/math?math=X&amp;mode=inline" alt="$X$"> be a random variable denoting the quality of a bottle of wine, and let <img decoding="async" class="math math-inline" src="https://render.githubusercontent.com/render/math?math=C&amp;mode=inline" alt="$C$"> be a random variable denoting its color (either red (<img decoding="async" class="math math-inline" src="https://render.githubusercontent.com/render/math?math=r&amp;mode=inline" alt="$r$">) or white (<img decoding="async" class="math math-inline" src="https://render.githubusercontent.com/render/math?math=w&amp;mode=inline" alt="$w$">)). For the remainder of this problem, we are concerned with probabilities such as “If I buy a random bottle of red wine, what is the probability that its quality is at least a 7?”. We could write that probability as <img decoding="async" class="math math-inline" src="https://render.githubusercontent.com/render/math?math=P%28X%20%5Cgeq%207%20%5Cmid%20C%3Dr%29&amp;mode=inline" alt="$P(X geq 7 mid C=r)$">, for example, and consider it the <strong><em>proportion</em></strong> of the population of red wines that are at least a 7 in quality. Calculate and report estimates of <img decoding="async" class="math math-inline" src="https://render.githubusercontent.com/render/math?math=P%28X%20%5Cgeq%207%20%5Cmid%20C%3Dr%29&amp;mode=inline" alt="$P(X geq 7 mid C=r)$"> and <img decoding="async" class="math math-inline" src="https://render.githubusercontent.com/render/math?math=P%28X%20%5Cgeq%207%20%5Cmid%20C%3Dw%29&amp;mode=inline" alt="$P(X geq 7 mid C=w)$">.

Obtain 95% confidence intervals for the proportion of red and white wines that are <strong>at least</strong> a 7 in quality (obtain one CI for each color). Based on your results, if you are interested in buying many high quality bottles of wine but are buying totally at random, is one color a better bet than the other? Fully justify your answer.

Calculations may be executed in Python, but you need to set up your work (<em>what</em> it is you are calculating) in Markdown/MathJax.

In [ ]:

<pre></pre>

<strong>Part C:</strong> Now, as college students (and teachers), we might not be super concerned with buying a really high quality bottle of wine. Let’s focus instead on making sure we do <em>not</em> buy a really disgusting bottle of wine. Calculate and report estimates of <img decoding="async" class="math math-inline" src="https://render.githubusercontent.com/render/math?math=P%28X%20%5Cgeq%205%20%5Cmid%20C%3Dr%29&amp;mode=inline" alt="$P(X geq 5 mid C=r)$"> and <img decoding="async" class="math math-inline" src="https://render.githubusercontent.com/render/math?math=P%28X%20%5Cgeq%205%20%5Cmid%20C%3Dw%29&amp;mode=inline" alt="$P(X geq 5 mid C=w)$">.

Obtain 95% confidence intervals for the proportion of red and white wines that are <strong>at least</strong> a 5 in quality, that is, <img decoding="async" class="math math-inline" src="https://render.githubusercontent.com/render/math?math=P%28X%20%5Cgeq%205%20%5Cmid%20C%29&amp;mode=inline" alt="$P(X geq 5 mid C)$">. Based on your results – and what you saw in Problem 1 – if you are interested in buying bottles of wine that are at least a 5 in quality, but are again buying wine totally randomly, can you conclude that you are better off buying one color over the other? Fully justify your answer.

In [ ]:

<pre></pre>

<strong>Part D:</strong> Compute a 95% confidence interval for the difference in proportions of red and white wines that are at least a 5 in quality.

Now, based on your results for this part, can you conclude that you are better off buying one color over the other? Fully justify your answer. How does your work here differ from your work in <strong>Part C</strong>?

In [ ]:

<pre></pre>

<strong>Part E:</strong> Now, we have many more observations of white wines than red. This certainly contributes to the width of the 95% confidence interval for the proportion of red wines that are at least a 5 in quality, which you should have found in <strong>Part C</strong> to be wider than the corresponding confidence interval for white wines.

How large would our sample size of red wines need to be in order to guarantee that this 95% confidence interval width is at most 0.01? Note that we are hypothetically adding more samples, so we do not know the precise value of <img decoding="async" class="math math-inline" src="https://render.githubusercontent.com/render/math?math=%5Chat%7Bp%7D&amp;mode=inline" alt="$hat{p}$">.

In [ ]:

<pre></pre>

<hr>

<a href="https://render.githubusercontent.com/view/ipynb?commit=463e2f80e1978d1ed5c55c0225f63c6dcc626b21&amp;enc_url=68747470733a2f2f7261772e67697468756275736572636f6e74656e742e636f6d2f64626c617272656d6f72652f63736369333032322f343633653266383065313937386431656435633535633032323566363363366463633632366232312f686f6d65776f726b2f686f6d65776f726b352f686d776b30355f4c6173744e616d655f46697273744e616d652e6970796e62&amp;nwo=dblarremore%2Fcsci3022&amp;path=homework%2Fhomework5%2Fhmwk05_LastName_FirstName.ipynb&amp;repository_id=145737840&amp;repository_type=Repository#top">Back to top</a>

<h3>[30 points] Problem 3 – Exploring Confidence Intervals</h3>

The <a href="https://en.wikipedia.org/wiki/Gumbel_distribution">Gumbel</a> distribution is one of several distributions frequently used to model environmental extremes (for example, extreme temperatures and sea levels). It is also fairly asymmetric, and thus interesting for investigating confidence intervals. It is implemented in scipy.stats as <a href="https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.gumbel_r.html">gumbel_r</a>, where the appendix “_r” denotes the right-skewed version of the Gumbel distribution (as opposed to the left-skewed).

<strong>Part A</strong>: Complete the following code cell to plot a histogram of 100 realizations from the Gumbel distribution with parameters <img decoding="async" class="math math-inline" src="https://render.githubusercontent.com/render/math?math=%5Cmu%3D8&amp;mode=inline" alt="$mu=8$">and <img decoding="async" class="math math-inline" src="https://render.githubusercontent.com/render/math?math=%5Cbeta%3D2&amp;mode=inline" alt="$beta=2$">. Be sure to leave this cell executed before turning in your assignment! Make your histogram grey with gold edges.

In [ ]:

<pre><span class="n">mu</span> <span class="o">=</span> <span class="mi">8</span><span class="n">beta</span> <span class="o">=</span> <span class="mi">2</span><span class="n">n_sample</span> <span class="o">=</span> <span class="mi">100</span><span class="c1"># your code here</span></pre>

<strong>Part B:</strong> Look up the analytical mean and variance of the Gumbel distribution with parameters <img decoding="async" class="math math-inline" src="https://render.githubusercontent.com/render/math?math=%5Cmu%3D8&amp;mode=inline" alt="$mu=8$"> and <img decoding="async" class="math math-inline" src="https://render.githubusercontent.com/render/math?math=%5Cbeta%3D2&amp;mode=inline" alt="$beta=2$"> and calculate them here by hand. Note that the Euler–Mascheroni constant can be accessed via <code>np.euler_gamma</code>.

Use the empirical mean from your sample in <strong>Part A</strong>, and the true variance of the Gumbel distribution to compute by hand a 95% confidence interval for the mean.

In [ ]:

<pre></pre>

<strong>Part C: A theoretical interlude.</strong> When Stella O’Flaherty (the famous octopus) ran her solution code for <strong>Part B</strong>, she obtained a 95% confidence interval of <img decoding="async" class="math math-inline" src="https://render.githubusercontent.com/render/math?math=%5B8.81%2C%209.82%5D&amp;mode=inline" alt="$[8.81, 9.82]$"> for the mean of the <img decoding="async" class="math math-inline" src="https://render.githubusercontent.com/render/math?math=Gum%28%5Cmu%3D8%2C%20%5Cbeta%3D2%29&amp;mode=inline" alt="$Gum(mu=8, beta=2)$"> distribution. For each of the following, explain why or why not the situation described is correct, given the technical definition of a 95% confidence interval we went over in class.

<strong>(i)</strong> If you had no other evidence regarding true mean of the <img decoding="async" class="math math-inline" src="https://render.githubusercontent.com/render/math?math=Gum%28%5Cmu%3D8%2C%20%5Cbeta%3D2%29&amp;mode=inline" alt="$Gum(mu=8, beta=2)$"> distribution, you could say there is a 95% chance that its true mean falls between 8.81 and 9.82.

<strong>(ii)</strong> If a class of 100 students all construct 95% confidence intervals for the mean of the <img decoding="async" class="math math-inline" src="https://render.githubusercontent.com/render/math?math=Gum%28%5Cmu%3D8%2C%20%5Cbeta%3D2%29&amp;mode=inline" alt="$Gum(mu=8, beta=2)$"> distribution, then we expect about 95 of their CIs to contain the true mean, and about 5 of them to miss the true mean.

<strong>(iii)</strong> There is a 95% probability that any given random variable sampled from <img decoding="async" class="math math-inline" src="https://render.githubusercontent.com/render/math?math=Gum%28%5Cmu%3D8%2C%20%5Cbeta%3D2%29&amp;mode=inline" alt="$Gum(mu=8, beta=2)$"> will be between 8.81 and 9.82.

<strong>Part D:</strong> In this part you’ll write a function to investigate the <em>coverage properties</em> of a confidence interval for the mean of the Gumbel distribution. Complete the following function to randomly sample <img decoding="async" class="math math-inline" src="https://render.githubusercontent.com/render/math?math=m%3D500&amp;mode=inline" alt="$m=500$"> sample means with sample size <img decoding="async" class="math math-inline" src="https://render.githubusercontent.com/render/math?math=n%3D100&amp;mode=inline" alt="$n=100$"> for the Gumbel distribution with parameters <img decoding="async" class="math math-inline" src="https://render.githubusercontent.com/render/math?math=%5Cmu%3D8&amp;mode=inline" alt="$mu=8$"> and <img decoding="async" class="math math-inline" src="https://render.githubusercontent.com/render/math?math=%5Cbeta%3D2&amp;mode=inline" alt="$beta=2$">. For each random sample, compute the 66% confidence interval for the mean. Note that you actually know that the variance for the true population distribution is, <img decoding="async" class="math math-inline" src="https://render.githubusercontent.com/render/math?math=%5Csigma%5E2&amp;mode=inline" alt="$sigma^2$">. Your function should do two things:

<ol>

 <li>Report the proportion of confidence intervals that successfully cover the true mean of the distribution</li>

 <li>Make a plot of 50 randomly selected confidence intervals. Overlay the intervals on the line <img decoding="async" class="math math-inline" src="https://render.githubusercontent.com/render/math?math=y%3D%5Ctextrm%7BTrue%20mean%7D&amp;mode=inline" alt="$y=textrm{True mean}$"> (from <strong>Part B</strong>). Color confidence intervals black if they cover the true mean, and red if they don’t.</li>

</ol>

Be sure to leave this cell executed before turning in your assignment!

In [ ]:

<pre><span class="k">def</span> <span class="nf">confidence_intervals</span><span class="p">(</span><span class="n">m</span><span class="o">=</span><span class="mi">500</span><span class="p">,</span> <span class="n">n</span><span class="o">=</span><span class="mi">100</span><span class="p">):</span>    <span class="n">mu</span> <span class="o">=</span> <span class="mi">8</span>    <span class="n">beta</span> <span class="o">=</span> <span class="mi">2</span>    <span class="c1"># Your code here</span>    <span class="n">proportion_CIs_covering_mean</span> <span class="o">=</span> <span class="mi">0</span>    <span class="nb">print</span><span class="p">(</span><span class="s2">"proportion covering mean: </span><span class="si">{:.3f}</span><span class="s2">"</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">proportion_CIs_covering_mean</span><span class="p">))</span>        <span class="n">confidence_intervals</span><span class="p">()</span></pre>

<strong>Part E:</strong> Does the proportion of confidence intervals that cover the true mean of the distribution agree with the theory described in class? Justify your conclusion.

<hr>

<a href="https://render.githubusercontent.com/view/ipynb?commit=463e2f80e1978d1ed5c55c0225f63c6dcc626b21&amp;enc_url=68747470733a2f2f7261772e67697468756275736572636f6e74656e742e636f6d2f64626c617272656d6f72652f63736369333032322f343633653266383065313937386431656435633535633032323566363363366463633632366232312f686f6d65776f726b2f686f6d65776f726b352f686d776b30355f4c6173744e616d655f46697273744e616d652e6970796e62&amp;nwo=dblarremore%2Fcsci3022&amp;path=homework%2Fhomework5%2Fhmwk05_LastName_FirstName.ipynb&amp;repository_id=145737840&amp;repository_type=Repository#top">Back to top</a>

<h3>[15 points] Problem 4 – Freethrows</h3>

<hr>

Keep your skills sharp by answering these straightforward questions.

<strong>Part A</strong>:

You have a shuffled deck of cards. It includes the usual 52 cards AND three special additional Octopus cards. You flip over the cards one by one, without replacing them in the deck. You count how many cards you’ll have to flip until you flip over the second Octopus. You repeat this many times. Simulate this process. Plot a histogram with binsize=1 of the outcomes, in lightgrey with white outline. Compute the mean, median, and mode for this dataset, indicate them on the plot too, using linstyles of green dashed, pink dotted, and black solid, respectively. Look up how to do a legend in MatPlotLib, and label your histogram, mean, median.

<hr>

In [ ]:

<pre></pre>

<strong>Part B</strong>:

In general, which is wider: a 95% confidence interval or a 99% confidence interval? How would you explain this to your younger sibling, who is not a statistician?

<hr>

In [ ]:

<pre></pre>

<strong>Part C</strong>:

Luckily, his fingertips also brush against your arm. That’s a foul, and everyone saw it. Back to the line. Back to CSCI3022:&lt;/font&gt;

Let <img decoding="async" class="math math-inline" src="https://render.githubusercontent.com/render/math?math=X&amp;mode=inline" alt="$X$"> be a normally-distributed random variable. You draw from it and get these values, stored in the numpy array <strong>durant</strong>, below. Compute a 95% confidence interval for the <em>standard deviation</em>.

<hr>

In [ ]:

<pre><span class="n">durant</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">array</span><span class="p">([</span><span class="mf">3.7778</span><span class="p">,</span><span class="mf">3.9459</span><span class="p">,</span><span class="mf">3.8248</span><span class="p">,</span><span class="mf">4.1111</span><span class="p">,</span><span class="mf">4.0180</span><span class="p">,</span><span class="mf">4.0898</span><span class="p">,</span><span class="mf">4.0380</span><span class="p">,</span><span class="mf">3.9273</span><span class="p">,</span><span class="mf">3.9614</span><span class="p">,</span><span class="mf">3.8387</span><span class="p">])</span></pre>

In [ ]:

<pre></pre>

<strong>Part D</strong>:

If you’re doing quality control for the average strength of carbon fiber that will be used in airplane construction, and your alternative hypothesis is that the strength of the carbon is below tolerance, and therefore unsafe, would you rather have a low Type I error rate or a low Type II error rate? Explain.

<hr>

<strong>Part E</strong>:

You measure 53 suckers from baby reef octopuses and find that they are, on average, 45.2 mm wide, with a standard devaition of 30.4mm.

Then you measure 41 suckers from from baby dumbo octopuses and find that they are, on average, 52.8 mm wide, with a standard deviation of 22.8 mm.

Is there statistical evidence at the 0.05 significance level that the true mean of baby dumbo octopus sucker width exceeds the true mean of baby reef octopus sucker width by more than 6 mm? Use a test of your choice.

<hr>

In [ ]:

<pre></pre>