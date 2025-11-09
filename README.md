# README

This folder contains a series of *.Rmd files that generate the figures associated with the draft paper: 

High fuel demands and overheating risk challenge mesothermic fishes in warming oceans. Nicholas L. Payne*, Edward P. Snelling, Ignacio Peralta-Maraver, Dave E. Cade, Taylor K. Chapple,  Alex G. McInturf, Yuuki Y. Watanabe, David W. Sims, Nuno Queiroz, Ivo da Costa, Lara L. Sousa, Jeremy A. Goldbogen, Haley R. Dolton & Andrew L. Jackson

The data files are:

+ `RMR_data_final.csv` which contains the routine metabolic data alongside body temperature (where available), mass and temperature at which it was observed for a range of species. 
+ `RMR_data_fina_core.csv` is a version of the dataset that has body temperatures corrected to represent core body temperature. [**AJ - check this is accurate description**]
+ `fish_shark_combined.tre` is a phylogenetic tree of the species in the RMR dataset used to run random effects regressions.
+ `kpars.rda`, `mod.rda` and `pars.rda` are R object data files containing objects of the same name which are used as global parameters by the main *.Rmd files in this project. The file `Fit-RMR-regression.Rmd` creates and/or defines these objects. 

The R code files are provided as Rnotebook *.Rmd files. They do not need to be run in order, and are stand-alone.

Note that when the figures are created, they are created directly into pdf containers using the function `pdf()` which is closed at at the end using `dev.off()` in order to allow the file to be completed and opened. This is instead of using `quartz()` or similar. 

+ `Fit-RMR-regression.Rmd` is not required to be run since its outputs are saved as the R objects `kpars.rda`, `mod.rda` and `pars.rda`. These output objects are required by the Figure generating files. This file loads both the raw RMR data and the phylogenetic tree data, processes them and fits a Bayesian phylogenetic regression of RMR by water temperature, body mass and ectotherm/mesotherm trait. The model is fit using STAN which must be correctly installed on the local computer to run. It is also worth noting that on older computers, this might take some time to run. 
+ `Figure-1-generation.Rmd` creates Figure 1 from the draft paper which is a radial phylogenetic tree alongside a regression of $\Ln(RMR)$ by $\Ln{mass}$. It outputs the figure as `Figure-1.pdf`.
+ `Figure-2-generation.Rmd` creates the multipanel Figure 2 from the draft paper. The four panels are: RMR by body mass for a range of body temperature $20 <= T_m <= 25$, Temperature elevation over a range of body masses for a fish at $T_m = 20$, and then one panel each for an ectotherm and a mesotherm showing $T_a$ values that can be heat balanced for fish over a range of body mass at different body temperatures $T_m$. It outputs the figure as `Figure-2.pdf`.
+ `Figure-3-generation.Rmd` creates the multipanel map plot showing how ectotherm and mesotherm ranges and RMR estimates vary by season and under future climate projections. It outputs the figure as `Figure-3.pdf`. This file introduces two helper functions. One loops over the a raster matrix of values and calculates $T_m$ from $T_a$ using the Lambert function method described in the paper. The other function creates a map with given inputs of fish trait values and a map of water temperatures.
+ `Supplementary-figure-generation.Rmd` creates a multipanel RMR map for a range of mesotherms of different sizes by summer and winter. It outputs the figures as `SM-maps.pdf`. This file also defines the same two helper functions that appear in `Figure-3-generation.Rmd`. Note that compared with Nacho's original files, I have changed the size of the plot to avoid stretching the maps, and also I have added a blank column of plots in the first column to leave space for the silhouettes to be added. As a consequence, the way in which the axes titles have been located has changed somewhat from the original version: they are now adjusted to different lines and locations to render them in the centre of the maps. 

