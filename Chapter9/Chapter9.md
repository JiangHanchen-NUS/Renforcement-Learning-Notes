#### Chapter 9 Policy Gradient Methods

Policy Gradient, Monte Carlo Policy Gradient

**Policy Gradient**

1. What is the idea about Policy Gradient Methods?
2. Explain different forms and distributions of average state value metric and average reward. What is the relationship between these two metrics?

3. Explain the form of derivatives of metrics.

**Monte Carlo Policy Gradient (REINFORCE)**

4. Explain the process of MCPG. Why is it also called REINFORCE?

5. Why Policy Gradient can keep a balance between exploiation and exploration?
6. Explain the process of MCPG.



1. Policy is used to be represented in tabular form. Policy gradient methods represent policy in function form and use scalar metrics to evaluate and update the policy to find optimal policies. Policy gradient methods are policy-based, instead of value-based in the previous chapters. It is more efficient to handle large state/action space and has stronger generalization ability to make it more efficient in data utilization. The basic method is using the gradient-ascent method to optimize the metric J(θ) to find optimal policy: 

<img src="assets/image-20241001144624576.png" alt="image-20241001144624576" style="zoom:50%;" />

​	where J(θ) is the metric, α is the optimizing rate.

2. 

​	**Average state value:**	

​	The basic form is:

<img src="assets/image-20241001144935876.png" alt="image-20241001144935876" style="zoom:50%;" />

​	Also can be written as:

<img src="assets/image-20241001145006512.png" alt="image-20241001145006512" style="zoom:50%;" />

​	Also:

<img src="assets/image-20241001145110492.png" alt="image-20241001145110492" style="zoom:50%;" />

​	Also:

<img src="assets/image-20241001145049283.png" alt="image-20241001145049283" style="zoom:50%;" />

​	where {R} is gained by the agent following policy π(θ) with suffient episodes and length.

​	For the last form, we can prove it is equal to other forms: 

<img src="assets/image-20241001151337579.png" alt="image-20241001151337579" style="zoom:50%;" />

​	Usually use <img src="assets/image-20241002092411153.png" alt="image-20241002092411153" style="zoom: 50%;" /> to refer to stationary distribution and use <img src="assets/image-20241002092454624.png" alt="image-20241002092454624" style="zoom:50%;" /> to refer to the case where d(s) is independent of the policy.

​	**Average reward:**

​	basic form:

<img src="assets/image-20241002091451890.png" alt="image-20241002091451890" style="zoom:50%;" />

​	where r<sub>π</sub>(s) is E[r(s, A)|s] = Σπ(a|s, θ) · r(a,s), where r(a,s) = E[R|s,a] = Σ<sub>r</sub>rp(r|s,a).s

​	Also:

<img src="assets/image-20241002092046512.png" alt="image-20241002092046512" style="zoom:50%;" />

​	Also:

<img src="assets/image-20241002092025268.png" alt="image-20241002092025268" style="zoom:50%;" />

​	**Relationship:**

<img src="assets/image-20241002092729030.png" alt="image-20241002092729030" style="zoom:50%;" />

3. 

<img src="assets/image-20241002094139913.png" alt="image-20241002094139913" style="zoom:50%;" />

​	Also:

<img src="assets/image-20241002094158774.png" alt="image-20241002094158774" style="zoom:50%;" />

​	To satisfy π(A|S,θ) > 0, we use softmax function:

<img src="assets/image-20241002094354225.png" alt="image-20241002094354225" style="zoom:50%;" />

​	which can ensure π(a|s,θ) > 0 and the total is 1. This policy can be realized by neural network.

4. Use gradient-ascent method to maximize J(θ):

<img src="assets/image-20241002100653003.png" alt="image-20241002100653003" style="zoom:50%;" />

​	we use samples to approximate the expectation. To be noted, q<sub>π</sub>(s<sub>t</sub>,a<sub>t</sub>) is unknown and we use q<sub>t</sub>(s<sub>t</sub>,a<sub>t</sub>) to approximate it. If q<sub>t</sub>(s<sub>t</sub>,a<sub>t</sub>) is obtained from Monte Carlo Estimation, then the method is called REINFORCE or Monte Carlo Policy Gradient. Transform the derivative in the equation:

<img src="assets/image-20241002101303026.png" alt="image-20241002101303026" style="zoom:50%;" />

<img src="assets/image-20241002101321370.png" alt="image-20241002101321370" style="zoom:50%;" />

5. Firstly, if β >= 0, the probability of choosing current (s<sub>t</sub>,a<sub>t</sub>) increases. The greater β is, the stronger the increase is.

<img src="assets/image-20241002110305265.png" alt="image-20241002110305265" style="zoom:50%;" />

​	Similarly, if β < 0, the probability of choosing current (s<sub>t</sub>,a<sub>t</sub>) decreases.

<img src="assets/image-20241002110441646.png" alt="image-20241002110441646" style="zoom:50%;" />

​	Then, if q<sub>t</sub> is large, then β is large, then the probability increases. This increases the exploitation. Similarly, if π<sub>t</sub> is small, then β is large when q<sub>t </sub>> 0, then the probability increases. This increases the exploration.

6. 

<img src="assets/image-20241002111205553.png" alt="image-20241002111205553" style="zoom:50%;" />
