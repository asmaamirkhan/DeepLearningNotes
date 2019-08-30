# Pyhton Code Snippets on The Basics of Neural Networks


<details>
<summary>Sigmoid Function</summary>

**Formula:**

<img src="../res/Sigmoid.png" height="45"  />

```python
def sigmoid(x):
    """
    Arguments:
    x -- A scalar, an array or a matrix

    Return:
    result -- sigmoid(x)
    """
    
    result = 1 /( 1 + np.exp(-x) )
    
    return result
```
</details>

[//]: ------------------------------------------------------------------------------

<details>
<summary>Sigmoid Gradient</summary>

**Description:** A function that computes gradients to optimize loss functions using backpropagation

**Formula:**

<img src="../res/SigmoidGradient.png" height="30"  />

```python
    def sigmoid_derivative(x):
    """
    Computes the gradient (also called the slope or derivative) of the sigmoid function with respect to its input x.
    
    Arguments:
    x -- A scalar or numpy array

    Return:
    ds -- Your computed gradient.
    """
    
    s = 1 / (1 + np.exp(-x))
    ds = s * (1 - s)
    
    return ds
```
</details>

[//]: ------------------------------------------------------------------------------

<details>
<summary>Reshaping Arrays (or images)</summary>


```python
    def arr2vec(arr, target):
     """
    Argument:
    image -- a numpy array of shape (length, height, depth)
    
    Returns:
    v -- a vector of shape (length*height*depth, 1)
    """
    
    v = image.reshape(image.shape[0] * image.shape[1] * image.shape[2], 1)
    
    return v
```
</details>

[//]: ------------------------------------------------------------------------------

<details>
<summary>Normalizing Rows</summary>

**Description:** Dividing each row vector of x by its norm.

**Formula:**


<img src="../res/Normalization.png" height="40"  />


```python
 
def normalizeRows(x):
    """
    Argument:
    x -- A numpy matrix of shape (n, m)
    
    Returns:
    x -- The normalized (by row) numpy matrix.
    """
    
    # Finding norms
    x_norm = np.linalg.norm(x, axis=1, keepdims=True)
    
    # Dividing x by its norm
    x = x / x_norm
    
    return x
```
</details>

[//]: ------------------------------------------------------------------------------

<details>
<summary>Softmax Function</summary>

**Description:**  A normalizing function used when the algorithm needs to classify two or more classes

**Formula:**


<img src="../res/Softmax.png" height="45"  />


```python
 def softmax(x):
    """Calculates the softmax for each row of the input x.

    Argument:
    x -- A numpy matrix of shape (n,m)

    Returns:
    s -- A numpy matrix equal to the softmax of x, of shape (n,m)
    """
    
    # Applying exp() element-wise to x
    x_exp = np.exp(x)

    # Creating a vector x_sum that sums each row of x_exp
    x_sum = np.sum(x_exp, axis=1, keepdims=True)
    
    # Computing softmax(x) by dividing x_exp by x_sum.
    # numpy broadcasting will be used automatically.
    s = x_exp / x_sum

    return s
```
</details>

[//]: ------------------------------------------------------------------------------

<details>
<summary>L1 Loss Function</summary>

**Description:**  The loss is used to evaluate the performance of the model. The bigger the loss is, the more different that predictions ( ŷ ) are from the true values ( y ). In deep learning, we use optimization algorithms like Gradient Descent to train the model and to minimize the cost.

**Formula:**


<img src="../res/L1Function.png" height="50"  />


```python
def L1(yhat, y):
    """
    Arguments:
    yhat -- vector of size m (predicted labels)
    y -- vector of size m (true labels)
    
    Returns:
    loss -- the value of the L1 loss function defined above
    """
    
    loss = np.sum(np.abs(y - yhat))
    
    return loss
```
</details>


[//]: ------------------------------------------------------------------------------

<details>
<summary>L2 Loss Function</summary>

**Description:**  The loss is used to evaluate the performance of the model. The bigger the loss is, the more different that predictions ( ŷ ) are from the true values ( y ). In deep learning, we use optimization algorithms like Gradient Descent to train the model and to minimize the cost.

**Formula:**


<img src="../res/L2Function.png" height="50"  />


```python
def L2(yhat, y):
    """
    Arguments:
    yhat -- vector of size m (predicted labels)
    y -- vector of size m (true labels)
    
    Returns:
    loss -- the value of the L2 loss function defined above
    """
    
    loss = np.sum((y - yhat) ** 2)
    
    return loss
```
</details>

[//]: ------------------------------------------------------------------------------

<details>
<summary>Propagation Function</summary>

**Description:**  Doing the "forward" and "backward" propagation steps for learning the parameters

**Formula:**

<img src="../res/GradW.png" height="50"  />
<br/>
<img src="../res/GradB.png" height="50"  />


```python
def propagate(w, b, X, Y):
    """
    Implementation of the cost function and its gradient for the propagation

    Arguments:
    w -- weights, a numpy array of size (num_px * num_px * 3, 1)
    b -- bias, a scalar
    X -- data of size (num_px * num_px * 3, number of examples)
    Y -- true "label" vector (containing 0 if non-cat, 1 if cat) of size (1, number of examples)

    Return:
    cost -- negative log-likelihood cost for logistic regression
    dw -- gradient of the loss with respect to w, thus same shape as w
    db -- gradient of the loss with respect to b, thus same shape as b
    
    """
    
    m = X.shape[1]
    
    # FORWARD PROPAGATION (FROM X TO COST)
    
    # computing activation
    A = sigmoid( np.dot(w.T, X) + b ) 
    
    # computing cost
    cost = - np.sum( Y * np.log(A) + (1-Y) * np.log(1 - A) ) / m 
    
    # BACKWARD PROPAGATION (TO FIND GRAD)
    
    dw = (np.dot(X,(A-Y).T))/m
    db = np.sum(A-Y)/m
    
    grads = {"dw": dw,
             "db": db}
    
    return grads, cost
```
</details>


[//]: ------------------------------------------------------------------------------

<details>
<summary>Gradient Descent (Optimization)</summary>

**Description:**  The goal is to learn _ω_ and _b_ by minimizing the cost function _J_. For a parameter _ω_

**Formula:**

<img src="../res/OptimizationFunction.png" height="30"  />


Where *α* is the learning rate

```python
def optimize(w, b, X, Y, num_iterations, learning_rate, print_cost = False):
    """
    This function optimizes w and b by running a gradient descent algorithm
    
    Arguments:
    w -- weights, a numpy array of size (num_px * num_px * 3, 1)
    b -- bias, a scalar
    X -- data of shape (num_px * num_px * 3, number of examples)
    Y -- true "label" vector (containing 0 if non-cat, 1 if cat), of shape (1, number of examples)
    num_iterations -- number of iterations of the optimization loop
    learning_rate -- learning rate of the gradient descent update rule
    print_cost -- True to print the loss every 100 steps
    
    Returns:
    params -- dictionary containing the weights w and bias b
    grads -- dictionary containing the gradients of the weights and bias with respect to the cost function
    costs -- list of all the costs computed during the optimization, this will be used to plot the learning curve.
    """
    
    costs = []
    
    for i in range(num_iterations):
        
        
        # Cost and gradient calculation
        grads, cost = propagate(w, b, X, Y)
        
        # Retrieve derivatives from grads
        dw = grads["dw"]
        db = grads["db"]
        
        # update rule
        w = w - learning_rate*dw
        b = b - learning_rate*db
        
        # Record the costs
        if i % 100 == 0:
            costs.append(cost)
        
        # Print the cost every 100 training iterations (optional)
        if print_cost and i % 100 == 0:
            print ("Cost after iteration %i: %f" %(i, cost))
    
    params = {"w": w,
              "b": b}
    
    grads = {"dw": dw,
             "db": db}
    
    return params, grads, costs
```
</details>