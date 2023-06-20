# Myosin-cluster-simulation
This repo contains the Jupyter Notebook to implement a simple toy model that quantitatively describes myosin cluster growth, as described in [Chou et al. (2023)](https://www.biorxiv.org/content/10.1101/2023.06.07.544121v1). In this paper, we described how myosin cluster sizes are controlled in the contractile cell cytoskeleton. We found that myosin clusters grow via the association of free myosin in the cytoplasm to existing myosin clusters on stress fibers. This toy model aims to quantitatively capture myosin cluster growth.

## Toy model setup
We model myosin cluster growth as the binding of a fixed pool of free myosin ($N_{myo}$) to a 1D grid. To capture the statistics of myosin cluster sizes, we model myosin cluster growth as a Monte Carlo process, where the simulation iterates through the random binding of a pool free myosin. In each iteration, myosin randomly chooses a grid point to bind. The probability of binding to a given grid point ($P_i$) is $P_i=\frac{1+\alpha M_i}{\sum_i P_i}$, where $M_i$ is the myosin cluster size at that grid point, and $\alpha$ is an affinity parameter that captures the scenario where myosin preferentially binds to existing clusters [[1](https://doi.org/10.1101/2023.04.26.538303)].


<figure>
  <img src="https://github.com/WHChou/Myosin-cluster-simulation/blob/14f5d9c97e4eb9b79712b0e015138c29814316df/FigSIM_A.png" width="800" alt="">
  <em>Fig. 1 Simulation setup.</em>
</figure>


## Results
### Myosin cluster growth without myosin motor activity
First, we use our toy model to simulate myosin cluster growth without myosin motor activity, specifically when Y-27 is washed out in cells treated with both Y-27 and blebbistatin. To make a meaningful comparison between the simulation and experiments, we initialized the simulation such that the size of myosin clusters on each grid matches the size distribution in cells treated with both Y-27 and blebbistatin (Fig. 2, i, Y+B+). As a result, the initial total cluster size in the simulation adds up to about 47000. Since our experimental results showed that ROCK-dependent myosin cluster growth increases assembled myosin by about 42%, the simulation iterates through the binding of about 20000 additional myosin filaments. If we assume that myosin filaments can bind to each grid point with equal probability ($\alpha$ = 0), corresponding to uniform growth rates across the cell, the myosin cluster sizes at the end of the simulation exhibit a Gaussian-like distribution (Fig. 2, ii). However, this result contradicts the experimentally observed lognormal distribution when we selectively wash out Y-27 (Fig. 2, i, Y-B+). When the affinity parameter is non-zero ($\alpha$ > 0), the simulated cluster sizes start to qualitatively recapitulate the lognormal distribution of myosin cluster sizes in the absence of myosin motor activity (Fig. 2, iii). We quantified the error between simulated and experimental cluster sizes by calculating the average distance between the cumulative distributions of experimental-measured and simulated myosin cluster sizes. While the simulated results are insensitive to changes in $\alpha$, presumably due to the finite size of our simulation setup, the simulated results depend heavily on the number of myosin iterated through the simulation. When we scan through a range of $N_{myo}$, the simulation error is the lowest when $N_{myo}$ is 20000, which coincides with experimentally quantified results (Fig. 2, iv)! This suggests that the limiting pool of available myosin is important for setting myosin cluster sizes.

<figure>
  <img src="https://github.com/WHChou/Myosin-cluster-simulation/blob/90e1f1d9bd0327ad7ab71e7dc6f453cc304d0980/FigSIM_B.png" width=800>
  <em>Fig. 2 Simulation of myosin cluster growth without myosin motor activity. (i) Experimentally observed myosin cluster size distribution in cells before (Y+B+) and after (Y-B+) washing out Y-27 in cells that are treated with both Y-27 and blebbistatin. (ii) Simulation when myosin binding probability is uniform across all grid points (α=0). Inset shows the cumulative distribution of the experimental and simulated results. (iii) Simulation when myosin has an affinity toward existing myosin clusters (α=10). Inset shows the cumulative distribution of the experimental and simulated results. (iv) Average distance between cumulative distributions of the experimental and simulated cluster sizes across different α and Nmyo values. Stars show the Nmyo determined by experimental quantifications. </em>
 </figure>
 
### Myosin cluster growth with myosin motor activity
We next explored if the same simulation framework and parameters can capture myosin cluster growth under myosin motor activity, specifically when blebbistatin is washed out from cells. To make a meaningful comparison with experiments, we initialized the simulation such that myosin cluster size on each grid matches the myosin cluster size distribution in blebbistatin-treated cells (Fig. 3, i). Using the same assumption as before, the initial total cluster size in the simulation adds up to about 81000. Since untreated cells show 54% more assembled myosin than blebbistatin-treated cells in our experimental quantification, the simulation iterates through the binding of about 44000 additional myosin filaments. As in the case of myosin cluster growth without motor activity, uniform myosin binding probability ($\alpha$ = 0) fails to capture the lognormal distribution of myosin cluster sizes in control cells (Fig. 3, ii). When the affinity parameter is non-zero ($\alpha$ > 0), the simulated result once again qualitatively recapitulated the experimental cluster sizes in control cells (Fig. 3). The error between simulated and experimental results decreased with increasing α but again converged around α=10 (Supp. Fig. 5). The optimal Nmyo that produces the least error between simulated and experimental results is around 37500, which is about 15% less than the experimentally measured Nmyo (Fig. 3, iv). This is likely due to the F-actin-dependent myosin cluster regulation not captured in this toy model. Taken together, our results suggest that myosin cluster sizes on stress fibers are set by a limiting pool of myosin available for cluster growth with myosin self-affinity.

<figure>
  <img src="https://github.com/WHChou/Myosin-cluster-simulation/blob/53ca7a44496a23317fbc383689ce218441734939/FigSIM_C.png" width=800>
  <em>Fig. 3 Simulation of myosin cluster growth with myosin motor activity. (i) Experimentally observed myosin cluster size distribution in cells treated with blebbistatin or control cells. (ii) Simulation when myosin binding probability is uniform across all grid points (α=0). Inset shows the cumulative distribution of the experimental and simulated results. (iii) Simulation when myosin has an affinity toward existing myosin clusters (α=10). Inset shows the cumulative distribution of the experimental and simulated results. (iv) Average distance between cumulative distributions of the experimental and simulated cluster sizes across different α and Nmyo values. Stars show the Nmyo determined by experimental quantifications.</em>
</figure>
