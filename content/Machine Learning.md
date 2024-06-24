# Calculus
**Note:** Superscripts inside of parenthesis are used for indexing purposes, not powers.

Cost function, where $a$ is the activation function of some layer $L$, less the expected output $y$, squared:
$$
C_0(. . .)=(a^{(L)}-y)^2
$$

Activation function for a given neuron, where $w^{(L)}$ is the weight of the neuron in the present layer, $a^{(L-1)}$ is the result of the previous layer's neuron activation function, and $b^{(L)}$ is the bias of the current layer's neuron:
$$
a^{(L)}=w^{(L)}a^{(L-1)}+b^{(L)}
$$

It is often easier to write the above expression as, where $\sigma$ is some non-linear function (like sigmoid or RELU):
$$
a^{(L)} = \sigma(z^{(L)})
$$

The following equivalency demonstrates how the weight $\partial w^{(L)}$ influences the cost $\partial w^{(L)}$ of a given neuron:
$$
{{\partial C_0}\over{\partial w^{(L)}}} = {{\partial z^{(L)}}\over {\partial w^{(L)}}}{{\partial a^{(L)} \over {\partial z^{(L)}}}{{\partial C_0}\over {\partial a^{(L)}}}} = a^{(L-1)}\sigma '(z^{(L)})2(a^{(L)}-y)
$$

To average the ratio of the weight to the cost of all neurons, take the product of the sum of all partial derivatives and $1 \over n$, where $n$ is the number of neurons:
$$
{{\partial C}\over {\partial w^{(L)}}} = {1 \over n}{\sum^{n-1}_{k=0}} {{\partial C_k}\over {\partial w^{(L)}}}
$$

We can apply the same formula to find the sensitivity of the cost $C_0$ to the bias $b^{(L)}$:
$$
{{\partial C_0}\over{\partial b^{(L)}}} = {{\partial z^{(L)}}\over {\partial b^{(L)}}}{{\partial a^{(L)} \over {\partial z^{(L)}}}{{\partial C_0}\over {\partial a^{(L)}}}} = 1\sigma '(z^{(L)})2(a^{(L)}-y)
$$
And for the previous activation function:
$$
{{\partial C_0}\over{\partial a^{(L-1)}}} = {{\partial z^{(L)}}\over {\partial a^{(L-1)}}}{{\partial a^{(L)} \over {\partial z^{(L)}}}{{\partial C_0}\over {\partial a^{(L)}}}} = w^{(L)}\sigma '(z^{(L)})2(a^{(L)}-y)
$$


8:02
# Data Sources
- https://physionet.org/about/database/
- https://archive.ics.uci.edu/dataset/336/chronic+kidney+disease
- https://futurebloodtesting.org/open-datasets/
- https://github.com/irinagain/Awesome-CGM?tab=readme-ov-file
- https://catalog.data.gov/dataset?q=&sort=views_recent+desc
- https://libguides.brown.edu/c.php?g=545426&p=3741199

# Resources
- https://mathoverflow.net/questions/25983/intuitive-crutches-for-higher-dimensional-thinking
- http://neuralnetworksanddeeplearning.com/chap1.html
- https://towardsdatascience.com/introduction-to-neural-networks-advantages-and-applications-96851bd1a207
- https://developers.google.com/machine-learning/crash-course
- https://rickwierenga.com/blog/ml-fundamentals
- https://www.kaggle.com/code/onurderya/time-series-forecasting-with-ann-lstm
- https://youtube.com/playlist?list=PLZHQObOWTQDNU6R1_67000Dx_ZCJB-3pi&si=y-O2YSLIXRSt6Emj