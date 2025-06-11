# K- Means Agglomerative Clustering

# Clustering
- An unsupervised learning techniques
- What makes a good cluster ?
    - Inter-cluster distance
    - Intra-cluster distance
- Major types of clustering
    - K-Means
    - Hierarchical Clustering
    - DBSCAN

# K-Means Clustering
- Need to specify the number of clusters
## K-Means Code
```python
from sklearn.cluster import KMeans

wcss = []
for i in range(2,5):
  kmeans = KMeans(n_clusters = i, init = 'k-means++',
                  max_iter=300, n_init=10, random_state=0)
  kmeans.fit(X)
  wcss.append(kmeans.inertia_)

plt.figure(figsize = (10,6))
plt.plot(range(2,5), wcss,marker = 'o')
plt.title('Elbow Method')
plt.xlabel('Number of Clusters')
plt.ylabel('WCSS')
plt.show()

```
# Hierarchical Clustering
## Agglomerative Hierarchical Clustering
- Starts from smallers clusters then they are grouped togother
- Groups points based on similarity in quantitative terms
- Can be visualized as dendograms
    - A tree like diagram that records the sequences of merges or splits

## Agglomerative Code
```python
from sklearn.cluster import AgglomerativeClustering
agg_hc = AgglomerativeClustering(n_clusters = 5,
                             metric = 'euclidean',
                             linkage = 'ward')

y_hc = agg_hc.fit_predict(X)
```
    
## Divisive Hierarchical Clustering
- Starts from one big cluster and then splits


# Silhouette Score
## Silhouette Score Code
```python
from sklearn.metrics import silhouette_score
silhouette_score = silhouette_score(X,y_hc)
```


# DBSCAN: Density Based Spatial Clustering of Applications with Noise
- Able to handle both dense regions and sparse regions

## DBSCAN Code
```python
from sklearn.cluster import DBSCAN
db = DBSCAN(eps=0.3, min_samples=10)
db.fit(X)
labels = db.labels_
```