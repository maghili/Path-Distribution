# Path Lenght Distribution

In this research we statistically investigate the path length distribution of randomly sprinkled points ina two-dimensional Minkowski space. The constant-distance hypersurfaces (in case of two dimensions lines) are not spheres like Riemannian manifold, but they are hyperboloids. Assuming the metric signarure of `(- +) `, we are looking at negative distances corresponding to timelike intervals or causally related regions in physics.
Such interpretation reduces the spacetime from a continuous fabric to a set of points that are causally related and the relations are only one way which makes it a directed graph. Representing this graph as a matrix of zeros and ones, one can obtain the path distribution by looking at the powers of this matrix. Doing so we see the distribution of paths in the figure

![paths](https://github.com/maghili/Path-Distribution/blob/master/50_point.png)

The theoretical calculations proving such average distributions can also be done, and it can be found <a href ="https://arxiv.org/abs/1805.07312">here</a>.

The presented research is part of a bigger research area knwon as Causa Set Theory. In this theory it is proven that with a fixed number of points `N`, as `N` is getting larger, most of the graphs with `N` points will have  the following form known as Kleitman-Rotschild limit. 

![KR](https://github.com/maghili/Path-Distribution/blob/master/3layer_RK.png)

These types of graphs can not represent a physical spacetime, and therefore are not useful. Knowing that in a physical spacetime the distribution of path length are of the form presented in the first figure, we can use the `peak position`, `width at half height`, and `N` to distinguish manifolds.

Another important use of this criterion is that it can be used both to estimate the dimension `d` of spacetime in which the graph is sprinkled in and to classify the spavetimes based on their dimensions.

Here I present one of the simulations. `2-D_Minkowski.npy`, `3-D_Minkowski.npy`, `4-D_Minkowski.npy` are the previously produced data in the form of dictionaries.

```
data1 = np.load('./2-D_Minkowski.npy')
data2 = np.load('./3-D_Minkowski.npy')
data3 = np.load('./4-D_Minkowski.npy')

TwoD = data1.tolist()
ThreeD = data2.tolist()
FourD = data3.tolist()

DataSet1 = pd.DataFrame.from_dict(TwoD)
DataSet2 = pd.DataFrame.from_dict(ThreeD)
DataSet3 = pd.DataFrame.from_dict(FourD)

y = [2]*len(DataSet1)+[3]*len(DataSet2)+[4]*len(DataSet3)
X = DataSet1.append(DataSet2).append(DataSet3)

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size = .2, random_state = 1)

clf = LogisticRegression(multi_class = 'ovr')
clf.fit(X_train, y_train)
print clf.score(X_test, y_test)
```
In which case the accuracy of `100%` is obtained. The more detailed code is presented <a href"https://github.com/maghili/Path-Distribution/blob/master/CausalSets.py.ipynb">here<a>.
