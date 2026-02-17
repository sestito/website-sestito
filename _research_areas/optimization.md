---
title: optimization
nochild: 
order: 0
---
## Optimization
{: class="section-heading"}

Optimization is the method of optimizing a set of parameters, or input variables, such that a set of objectives, or output variables, are minimized (or maximized). In its simplest form, single objective optimization with one parameter can be represented as $$\min_{x} f(x)$$. Our goal is then to find the value of $$x$$ which minimizes $$f(x)$$. If instead we wish to maximize $$f(x)$$, we can just minimize $$-f(x)$$. This is rather trivial to accomplish but becomes much more difficult as the number of parameters and objectives increase. 

{% include research_image.html url="/assets/images/research/pareto_front.png" width="30%" minwidth="15rem" align="left" class="image-center" %}

Multi-objective optimization is when the number of objectives is greater than one. For a set of parameters $$\boldsymbol{x} = (x_1, x_2, ... , x_m),$$ the optimization problem can be represented as

<div>$$ 
    \min_{\boldsymbol{x}} ( f_1(\boldsymbol{x} ), f_2(\boldsymbol{x}), ... , f_n(\boldsymbol{x}) ),
$$</div>

where the goal is to minimize all of the objectives by modifying the parameters. In a theoretical sense, the ideal soltuion would be an $$\boldsymbol{x}$$ which represents the absolute minimum for all objectives simultaneously. However, in a more traditional sense, selecting an $$\boldsymbol{x}$$ which minimizes one objective does not minimize the other objectives. However, there are a set of solutions such that it is impossible to decrease the value of one objective by changing the value of $$\boldsymbol{x}$$ without increasing the value of the other objectives. This set of solutions results in what is known as the Pareto front, which is a set of non-dominated solutions that for the minimum front of the objective space. This Pareto front holds the ideal solutions to the optimization problem in which a set of design variables should be selected for the desired minimum objectives.

Now, how does this relate to engineering? When desiging parts your always trying to minimze and maximize attributes. Maybe you wish to minimize manufacturing costs and time while keeping with the original design of your product; you then can adjust the geometric design to minimize these two competing objectives. These optimization problems are all around us!

Our goal is to find efficient and effective methods to calculate the pareto front for a large number of parameters and objectives. We also wish to explore optimization engineering problems and apply optimization methods to solve these engineering problems.
