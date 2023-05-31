# Myosin-cluster-simulation
This repo contains the code to implement a simple toy model that quantitatively describes myosin cluster growth. In my paper (in preparation), I described how myosin cluster sizes on stress fibers are controlled in cells. We found that myosin clusters grow via the association of free myosin in the cytoplasm to existing myosin clusters on stress fibers. This toy model aims to quantitatively capture myosin cluster growth.

To this end, we model myosin cluster growth as the binding of free myosin to a 1D grid. To capture the statistics of myosin cluster sizes, we model myosin cluster growth as a Monte Carlo process, where the simulation iterates through the random binding of free myosin. In each iteration, myosin randomly chooses a grid point to bind. The probability of binding to a given grid point ($P_i$) is $P_i=\frac{1+\alpha M_i}{\sum_i P_i}$, where $M_i$ is the myosin cluster size at that grid point, and $\alpha$ is an affinity parameter that captures the scenario where myosin preferentially binds to existing clusters [[1](https://doi.org/10.1101/2023.04.26.538303)].




<img src="https://github.com/WHChou/Myosin-cluster-simulation/blob/242db198332cec142b1811208f8b91ad5cf7c301/FigSIM_v3.png" width="750">
