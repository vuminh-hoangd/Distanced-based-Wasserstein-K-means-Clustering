# Distance-based Wasserstein $K$-means Clustering

## Background and Definitions

Let $(\mathcal{X}, ||\cdot||_2)$ be $\mathbb{R}^d$ equipped with the Euclidean norm, and let $\mu, \nu \in \mathcal{P}_2(\mathbb{R}^d)$, i.e. the space of all probability measures on $\mathbb{R}^d$ with finite second moments. The squared Wasserstein 2-distance between $\mu$ and $\nu$ is defined as

$$
W_2^2(\mu, \nu) = \inf_{\gamma \in \Gamma(\mu,\nu)} \int_{\mathbb{R}^d \times \mathbb{R}^d} \|x - y\|_2^2 \, d\gamma(x,y),
$$

where $\Gamma(\mu, \nu)$ denotes the set of all couplings of $\mu$ and $\nu$, i.e., the collection of all Borel probability measures $\gamma$ on $\mathbb{R}^d \times \mathbb{R}^d$ whose marginals are $\mu$ and $\nu$ respectively. Formally, $\gamma \in \Gamma(\mu, \nu)$ if and only if
$$
\gamma(A \times \mathbb{R}^d) = \mu(A) \quad \text{and} \quad \gamma(\mathbb{R}^d \times A) = \nu(A)
$$
for all Borel measurable sets $A \subseteq \mathbb{R}^d$.

### Distance-based Wasserstein $K$-means (D-WKM)

In Wasserstein space, the data points are probability distributions $\mu_i$. The objective function looks similar to Distance-based Euclidean $K$-means but behaves differently.

$$
\sum_{k=1}^{K} \frac{1}{|G_k|} \sum_{i,j \in G_k} W_2^2(\mu_i, \mu_j)
$$

Correspondingly, we can analogously design an algorithm for the update rule. Given an initial cluster estimate $G_1^{(0)}, \dots, G_K^{(0)}$, one assigns each probability measure $\mu_1, \dots, \mu_n$ based on minimizing the averaged squared $W_2$ distances to all current members in every cluster, leading to an updated cluster rule as

$$
G_k^{(t+1)} = \{ i \in [n] : \frac{1}{|G_k^{(t)}|} \sum_{s \in G_k^{(t)}} W_2^2(\mu_i, \mu_s) \leq \frac{1}{|G_j^{(t)}|} \sum_{s \in G_j^{(t)}} W_2^2(\mu_i, \mu_s), \quad \forall j \in [K] \} \tag{1}
$$

## Comparing Clustering Performance Across Fashion-MNIST Class Pairs using D-WKM, K-means and GMM

- **Well-Separated Distributions.** D-WKM achieves optimal clustering performance when class distributions are well-separated in Wasserstein space. For visually distinct pairs such as *T-shirt vs. Sandal* and *Trouser vs. Sneaker*, D-WKM with K-means++ initialization attains perfect or near-perfect clustering scores (Accuracy ≈ 1.0, NMI ≈ 1.0, ARI ≈ 1.0). In these cases, K-means++ initialization consistently outperforms random initialization.

- **Moderately Separated Distributions.** When class distributions have greater visual similarity, D-WKM performance degrades. For *Shirt vs. Dress*, D-WKM maintains superior clustering quality compared to baseline methods, though performance gaps narrow. However, this is the only case where K-means++ initialization underperforms relative to random initialization. For *T-shirt vs. Pullover*, D-WKM yields comparable results to standard K-means and GMM.

- **Poorly Separated Distributions**. The most challenging scenario *Sandal vs. Sneaker*. In this case, D-WKM performs significantly worse than both K-means and GMM.
