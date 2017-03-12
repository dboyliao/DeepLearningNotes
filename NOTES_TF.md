## Notes for Tensorflow

- Basic setup
```python
import tensorflow as tf

graph = tf.Graph()

# use context manager to set up default
# working graph
with graph.as_default():
    # now all operations will happend in graph.
    # do work here....
```
- Running graph with session
```python
with tf.Session(graph=graph) as session:
   # you first initialize all variables in the graph
   tf.global_variables_initializer().run()
   # do work afterward...
   # things_you_want is a list of tensors you
   # want the session to return its value
   session.run(things_you_want)
```
- When creating tensor with `tensorflow` api, it is recommanded to specify the dimension with a list, not tuple.
- `tf.constant`: create a constant tensor
- `tf.Variable`: create a variable tensor. This means that it will be updated during training.
- `tf.matmul`: multiply two matrices (2D array or array with rank > 2 which represents a batch of matrices). The rank should be compatible.
- `tf.reduce_mean`: conceptually the same as `numpy.mean`
- `tf.nn` is the module where you can find ops for constructing a neural network including:
  - activation functions
  - convolution operators
  - pooling
  - morphological filtering
  - normalizing
  - loss functions
  - RNN
  - and more....
- `tf.nn.softmax_cross_entropy_with_logits`: softmax cross entropy.
- `tf.Tensor.eval(self, feed_dict=None, session=None)`: evaluate a tensor. If `feed_dict` is not given, it will return the current value in the graph.
  - It can be used only within a `session`.

## Snippets

- reformatting
```python
# data: `N` by `m` by `k` numpy array
data = data.reshape((-1, m*k)) 
```
- one-hot encoding
```python
# labels: 1D numpy array with length `N` each element
#   is a label of original data. `k` kinds of labels.
labels = (np.arange(k) == labels[:,None])
```