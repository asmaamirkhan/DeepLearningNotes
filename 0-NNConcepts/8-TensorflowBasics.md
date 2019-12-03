# 🏃‍♀️ Brief Introduction to Tensorflow

## 🚩 Main flow of programs in Tensorflow
1. Create Tensors (variables) that are not yet executed/evaluated.
1. Write operations between those Tensors.
1. Initialize your Tensors.
1. Create a Session.
1. Run the Session. This will run the operations you'd written above.

> To summarize, remember to initialize your variables, create a session and run the operations inside the session. 👩‍🏫

## 👩‍💻 Code Example
To calculate the following formula:

$$loss=L(\hat{y},y)=(\hat{y}^{(i)}-y^{(i)})^2$$

```python
# Creating tensors and writing operations between them 
y_hat = tf.constant(36, name='y_hat')
y = tf.constant(39, name='y')
loss = tf.Variable((y - y_hat)**2, name='loss')

# Initializing tensors
init = tf.global_variables_initializer()

# Creating session
with tf.Session() as session: 
    # Running the operations
    session.run(init) 

    # printing results
    print(session.run(loss)) 
```

> When we created a variable for the loss, we simply defined the loss as a function of other quantities, but did not evaluate its value. To evaluate it, we had to use the initializer.

## ❗ Değişken Başlatma _(initalization)_ Hakkında Not

For the following code:

```python
a = tf.constant(2)
b = tf.constant(10)
c = tf.multiply(a,b)
print(c)
```

🤸‍♀️ The output is

```
Tensor("Mul:0", shape=(), dtype=int32)
```

As expected, we will not see 20 🤓! We got a tensor saying that the result is a tensor that does not have the shape attribute, and is of type "int32". All we did was put in the **'computation graph'**, but we have not run this computation yet.



## 📦 Placeholders in TF
- A placeholder is an object whose value you can specify **only later**. To specify values for a placeholder, we can pass in values by using a `feed dictionary`. 
- Below, a placeholder has been created for x. This allows us to pass in a number later when we run the session.

```python
x = tf.placeholder(tf.int64, name = 'x')
print(sess.run(2 * x, feed_dict = {x: 3}))
sess.close()
```

## 🎀 More examples
Computing sigmoid function with TF

```python
def sigmoid(z):
    """
    Computes the sigmoid of z
    
    Arguments:
    z -- input value, scalar or vector
    
    Returns: 
    results -- the sigmoid of z
    """
    
    # Creating a placeholder for x. Naming it 'x'.
    x =  tf.placeholder(tf.float32, name = 'x')

    # computing sigmoid(x)
    sigmoid = tf.sigmoid(x)

    # Creating a session, and running it.
    with tf.Session() as sess:
        # Running session and call the output "result"
        result = sess.run(sigmoid, feed_dict = {x: z})
        
    return result
```

Computing cost function with TF

```python
def cost(logits, labels):
    """
    Computes the cost using the sigmoid cross entropy
    
    Arguments:
    logits -- vector containing z, output of the last linear unit (before the final sigmoid activation)
    labels -- vector of labels y (1 or 0) 
    
    Returns:
    cost -- runs the session of the cost function
    """
    
    # Creating the placeholders for "logits" (z) and "labels" (y)
    z = tf.placeholder(tf.float32, name = 'z')
    y = tf.placeholder(tf.float32, name = 'y')
    
    # Using the loss function
    cost = tf.nn.sigmoid_cross_entropy_with_logits(logits = z,  labels = y)
    
    # Creating a session
    sess = tf.Session()
    
    # Running the session 
    cost = sess.run(cost, feed_dict = {z: logits, y: labels})
    
    # Closing the session
    sess.close()
        
    return cost
```