
<!-- README.md is generated from README.Rmd. Please edit that file -->

# WeedEco

<!-- badges: start -->
<!-- badges: end -->

This repository stores the R package WeedEco. This package contains
functions which conduct linear discriminant analysis using one of three
modern models (i.e., sets of discriminated modern arable fields) to
classify archaeobotanical data or other cases the investigator wishes to
classify, such as survey data from other farming regimes, on the basis
of relevant functional ecological traits (or attributes) of weed
species. Other functions include those related to data organisation, as
well as functions for plotting the results of the linear discriminant
analysis in comparison with the selected modern model.

## Referencing

The package draws on data from the functional trait database, as well as
models constructed by [Bogaard et
al. (2016)](https://doi.org/10.1007/s00334-015-0524-0), [Bogaard et
al. (2018)](https://doi.org/10.1080/14614103.2016.1261217) and [Bogaard
et al. (2021)](https://library.oapen.org/handle/20.500.12657/58568).

When publishing results obtained via the use of this package please cite
the package and its version, as well as the functional trait database
and the model used. A best practice example paragraph is provided in
Stroud et al. (2023).

**Package citation**: Stroud, E., (2023) WeedEco: Classification of
unknown cases using linear discriminant analysis to understand farming
regimes. R package version 0.1.0,
\<\[<a href="https://github.com/\\" class="uri">https://github.com/\\</a>\](<a href="https://github.com/\" class="uri">https://github.com/\</a>){.uri}\>.

**Functional trait database**: \<ORA link\>

**Model 1**: Bogaard, A., Hodgson, J., Nitsch, E. *et al.* (2016)
Combining functional weed ecology and crop stable isotope ratios to
identify cultivation intensity: a comparison of cereal production
regimes in Haute Provence, France and Asturias, Spain. *Veget Hist
Archaeobot* **25**, 57–73. [DOI:
10.1007/s00334-015-0524-0](https://doi.org/10.1007/s00334-015-0524-0)

**Model 2**: Bogaard, A., Styring, A., Ater, M., *et al.* (2018) From
Traditional Farming in Morocco to Early Urban Agroecology in Northern
Mesopotamia: Combining Present-day Arable Weed Surveys and Crop Isotope
Analysis to Reconstruct Past Agrosystems in (Semi-)arid
Regions, Environmental
Archaeology, 23:4, 303-322, DOI: [10.1080/14614103.2016.1261217](#0)

**Model 3**: Bogaard, A., Hodgson, J., Kropp, C., *et al.* (2022)
Lessons from Laxton, Highrove and Lorsch: Building arable weed-based
models for the investigation of Early Medieval Agriculture in England in
McKerracher, M., and H. Hamerow (eds) *New Perspectives on the Medieval
‘Agricultural Revolution’: Crop, Stock and Furrow*. Liverpool University
Press. [Online
resource](https://library.oapen.org/handle/20.500.12657/58568)

**Example paper**: Stroud et al. (in prep). Seeing the fields through
the weeds: introducing the WeedEco R package for comparing past and
present arable farming systems using functional weed ecology. Vegetation
History and Archaeobotany

## Installation

You can install the package WeedEco from [GitHub](https://github.com/)
with:

``` r
# install.packages("devtools")
devtools::install_github("elizabethastroud/FIBS-R-Package")
```

## Example

This is a basic example which shows the use of the package with a
simulated data set. Please see Stroud et al. (2023) for a fully worked
example using archaeobotanical data. Please note that each species used
requires its correct four_three code - the unique identifier which links
it with the corresponding species within the functional trait database.
More details can be found here \<insert link\>.

``` r
library(WeedEco)
## Random data created to represent survey data or archaeobotanical counts
species<-c("Chenopodium album" , "Anthemis cotula", "Brassica rapa",
  "Raphanus raphanistrum", "Agrostemma githago" , "Poa annua" )
Four_three_code<-c("chenalb", "anthcot", "brasrap","raphrap","agrogit", "poa_ann")
s.1246<-sample(1:3, 6, replace=T)
s.46178<-sample(1:5, 6, replace=T)
s.1<-sample(0:8, 6, replace=T)
s.23<-sample(0:3, 6, replace=T)
s.987<-sample(3:9, 6, replace=T)
dataset<-data.frame(species,Four_three_code,s.1246,s.46178,s.1,s.23,s.987) # the random dataset
## Creation of random flowering period dataset
# Note that flowering period (max duration) is not provided and must be collected from relevant literature
FLOWPER<-sample(3:9, 6, replace=T)
x<-data.frame(Four_three_code,FLOWPER) 
## Data organisation - function used to organise archaeobotncial or survey data for LDA analysis
results<-wdata_org(dataset, samples=3, codes=2, codename="Four_three_code,", model=1, fl_pr=x)
#>              SLA    ARNODE LOGCANH  LOGCAND  FLOWPER
#> s.1246  23.78448 12008.417    5.50 5.500000 6.500000
#> s.46178 23.78448 12008.417    5.50 5.500000 6.500000
#> s.1     24.64255 13468.402    5.25 5.500000 5.250000
#> s.23    20.59847  8737.949    6.00 5.333333 7.666667
#> s.987   23.78448 12008.417    5.50 5.500000 6.500000
```

``` r
## LDA anaylsis classification using model 1
LDA<-wmodel.LDA(results, model = 1)
#> 
#> Results and linear discriminant scores:
#>         CLASS_std* Prob.1_std* Prob.2_std*   LD1*
#> s.1246           2           0           1 -3.019
#> s.46178          2           0           1 -3.019
#> s.1              2           0           1 -3.991
#> s.23             2           0           1 -3.102
#> s.987            2           0           1 -3.019
#> 
#> Centroids:
#>   Group Centroid1
#> 1     1     2.441
#> 2     2    -2.833
```

``` r
## Visulastion using wplot_basic
wplot_basic(model = 1, LDA$`LD1*`)
```

<img src="man/figures/README-Plot-1.png" width="100%" />

## 
