# Convex Optimization

# Part 1: Warm-up, minimization problem and gradient descent
The first part is about using the Gradient descent method to solve a minimization problem

We find the optimal step (leading to the fewest iterations) for which the method converges


![alt text](https://github.com/kderkba/ConvexOptimization/blob/main/iterations_vs_stepsize.png)

When the step size is too small the algorithm needs more iterations to converge.
When it is too large the algorithm does not converge

![alt text](https://github.com/kderkba/ConvexOptimization/blob/main/evolution_of_error.png)

The error compared to numpy linalg solve decreases as the number of iteration increases. It increases as the dimension of the problem increases. 

# Part 2: Penalization

In this part we explore two penalization methods. We consider a path between an origin and an endpoint and we try to find the shortest path according to constraints

Let 
<img src="https://render.githubusercontent.com/render/math?math=\gamma"> be the path (collection of points in a square of length 1),<img src="https://render.githubusercontent.com/render/math?math=\mathcal{H}(\gamma) = \frac{1}{2} \int_{0}^{1} [x'(t)^2+ y'(t)^2]dt"> be the function to minimize,<img src="https://render.githubusercontent.com/render/math?math=D = {(x,y) \in \mathbb{R}^{2}, (x-a)^{2} + (y-b)^{2} < r^{2}}"> the constraint.

We define penalization functions such that we avoid the obstacle(s).
We discretize every function and implement them.

## External penalization

The penalization function is <img src="https://render.githubusercontent.com/render/math?math=\mathcal{R}(\gamma) = \frac{1}{2} \int_{0}^{1} max(0,r^{2} -(x-a)^{2} - (y-b)^{2})^2 dt">

The goal is to minimize <img src="https://render.githubusercontent.com/render/math?math=\mathcal{H}_{\epsilon} = \mathcal{H}(\gamma) + \frac{1}{\epsilon}\mathcal{R}(\gamma)">

![alt text](https://github.com/kderkba/ConvexOptimization/blob/main/penalization1.png)

As <img src="https://render.githubusercontent.com/render/math?math=\epsilon"> becomes smaller, the penalization becomes larger and the constraint is respected.

## Internal penalization

The penalization function is <img src="https://render.githubusercontent.com/render/math?math=\mathcal{L}(\gamma) = \frac{1}{2}\int_{0}^{1} log(r^{2} -(x-a)^{2} - (y-b)^{2}) dt ">

The goal is to minimize <img src="https://render.githubusercontent.com/render/math?math=\mathcal{G}_{\alpha} = \mathcal{H}(\gamma) - \alpha\mathcal{L}(\gamma)">

![alt text](https://github.com/kderkba/ConvexOptimization/blob/main/penalization2.png)

The algorithm goes through the obstacle until  <img src="https://render.githubusercontent.com/render/math?math=\apha"> is large enough.

## Comparison

There seems to be a threshold phenomenon with the second penalization method where it will pass through the obstacle until penalization parameter is large enough to respect the constraint

The first penalization method is an external penalization method because the minimiser of <img src="https://render.githubusercontent.com/render/math?math=\mathcal{R}"> does not necessarily verify the constraints, only in an approximate manner. And the penalization fonction is 0 only in the admissible set of points.
Whereas, the second method is an internal penalization method. The minimizer of  <img src="https://render.githubusercontent.com/render/math?math=\mathcal{L}"> verifies the constraints and the penalization works when we approach the constraints, not just when we violate it.

![alt text](https://github.com/kderkba/ConvexOptimization/blob/main/comparison.png)

## Developments

![alt text](https://github.com/kderkba/ConvexOptimization/blob/main/obstacles.png)

We observe the behavior when we add obstacles


