# Distanced-based Wasserstein $K$-means Clustering 


**Comparing Clustering Performance Across Fashion-MNIST Class Pairs using D-WKM, K-means and GMM**

- **Well-Separated Distributions.** D-WKM achieves optimal clustering performance when class distributions are well-separated in Wasserstein space. For visually distinct pairs such as *T-shirt vs. Sandal* and *Trouser vs. Sneaker*, D-WKM with K-means++ initialization attains perfect or near-perfect clustering scores (Accuracy ≈ 1.0, NMI ≈ 1.0, ARI ≈ 1.0). In these cases, K-means++ initialization consistently outperforms random initialization.


- **Moderately Separated Distributions.** When class distributions have greater visual similarity, D-WKM performance degrades. For *Shirt vs. Dress*, D-WKM maintains superior clustering quality compared to baseline methods, though performance gaps narrow. However, this is the only case where K-means++ initialization underperforms relative to random initialization. For *T-shirt vs. Pullover*, D-WKM yields comparable results to standard K-means and GMM.

- **Poorly Separated Distributions**. The most challenging scenario *Sandal vs. Sneaker*. In this case, D-WKM performs significantly worse than both K-means and GMM.
