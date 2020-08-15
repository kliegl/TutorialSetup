

# Background

A course on MixedModels in the Julia Programming Language will be held September 7-11, 2020 as one of four streams of the *Fourth Summer School for Statistical Methods for Linguistics and Psychology* [(SMLP2020)](https://vasishth.github.io/smlp2020/). SMLP2020 has been organized by [Shravan Vasishth](https://vasishth.github.io) at the University of Potsdam, Germany, since 2017, as part of a [methods project](https://www.uni-potsdam.de/en/sfb1287/projects/infrastructure-service-training-and-central-projects/project-q.html) funded within the Collaborative Research Project *Limits of Variability in Language* [(SFB 1287)](https://www.uni-potsdam.de/en/sfb1287/index). This year this stream will be taught virtually using Zoom for daily real-time meetings.

Applicants must have experience with linear mixed models and be interested in learning how to carry out such analyses with the Julia-based MixedModels package) (i.e., the analogue of the R-based lme4 package). Julia MixedModels has some significant advantages. Some of them are: (a) new and more efficient computational implementation, (b) speed — needed for, e.g., complex designs and the computation of statistical power, (c) more flexibility for selection of parsimonious mixed models, and (d) more flexibility in taking into account autocorrelations or other dependencies — typical EEG-, fMRI-based time series (under development). We do not expect profound knowledge of Julia from participants; the necessary subset of knowledge will be taught on the first two days of the course. 

We do expect a readiness to install Julia and the confidence that with some basic instruction participants will be able to adapt prepared Julia scripts for their own data or to adapt some of their own lmer()-commands to the equivalent MixedModels()-commands. The course will be taught in a hybrid IDE. There is already the option to execute R chunks from within Julia, meaning one needs Julia primarily for execution of MixedModels command as replacement of lmer(). There is also an option to call Julia MixedModels from within R and process the resulting object like an lme4-object. Thus, much of pre- and postprocessing (e.g., data simulation for complex experimental designs; visualization of partial-effect interactions or shrinkage effects) can be carried out in the RStudio / R environment. 

# Instructions for setup

We assume that those participating in the tutorial are somewhat familiar with [`R`](https://R-project.org) and the [`RStudio`](https://rstudio.com/products/rstudio) IDE (integrated development environment).

## Installing Julia

The [Julia download site](https://julialang.org/downloads/) provides binary downloads for most common operating systems. Ensure that the version you install is v1.5.0. 

## The Julia REPL

By itself the Julia binary provides a basic REPL (read-eval-print-loop), which is quite adequate for installing packages. (Installing and using IDE's for Julia is discussed below.) When you start Julia you are in julia mode, as indicated by the `julia> ` prompt.

Typing certain characters as the first in an input line will change the mode of the REPL.

| Character | Prompt | Context |
| --------- | ------ | --------------- |
| `?` | `help?> ` | Help mode - print help messages on functions, types, etc. |
| `]` | `(v1.3) pkg> ` | Pkg mode - install, list, remove, etc. packages |
| `;` | `shell> ` | Shell mode - execute a single shell command |
| `$` | `R> ` | R mode - requires `RCall` package installed and active |
| `<backspace>` | `julia> ` | return to Julia mode |

## Julia packages

### The Standard Library

A binary installation of Julia includes several packages in the standard library. They are listed and documented as part of the general documentation at https://docs.julialang.org. Most of the time a user does not need to be conscious of these packages but occasionally we will attach one explicitly.

For example
~~~~{.julia}
julia> using InteractiveUtils, Random, Statistics

julia> varinfo(Random)   # list exported functions and types
  name                   size summary                   
  ––––––––––––––– ––––––––––– ––––––––––––––––––––––––––
  AbstractRNG       168 bytes DataType                  
  MersenneTwister   224 bytes DataType                  
  Random          380.452 KiB Module                    
  RandomDevice      184 bytes DataType                  
  bitrand             0 bytes typeof(Random.bitrand)    
  rand!               0 bytes typeof(Random.rand!)      
  randcycle           0 bytes typeof(Random.randcycle)  
  randcycle!          0 bytes typeof(Random.randcycle!) 
  randexp             0 bytes typeof(Random.randexp)    
  randexp!            0 bytes typeof(Random.randexp!)   
  randn!              0 bytes typeof(Random.randn!)     
  randperm            0 bytes typeof(Random.randperm)   
  randperm!           0 bytes typeof(Random.randperm!)  
  randstring          0 bytes typeof(Random.randstring) 
  randsubseq          0 bytes typeof(Random.randsubseq) 
  randsubseq!         0 bytes typeof(Random.randsubseq!)
  shuffle             0 bytes typeof(Random.shuffle)    
  shuffle!            0 bytes typeof(Random.shuffle!)   

julia> varinfo(Statistics)
  name              size summary                     
  –––––––––– ––––––––––– ––––––––––––––––––––––––––––
  Statistics 220.695 KiB Module                      
  cor            0 bytes typeof(Statistics.cor)      
  cov            0 bytes typeof(Statistics.cov)      
  mean           0 bytes typeof(Statistics.mean)     
  mean!          0 bytes typeof(Statistics.mean!)    
  median         0 bytes typeof(Statistics.median)   
  median!        0 bytes typeof(Statistics.median!)  
  middle         0 bytes typeof(Statistics.middle)   
  quantile       0 bytes typeof(Statistics.quantile) 
  quantile!      0 bytes typeof(Statistics.quantile!)
  std            0 bytes typeof(Statistics.std)      
  stdm           0 bytes typeof(Statistics.stdm)     
  var            0 bytes typeof(Statistics.var)      
  varm           0 bytes typeof(Statistics.varm)     

~~~~~~~~~~~~~





### User-contributed Packages

A listing of registered Julia packages is available at https://pkg.julialang.org/.  Note the panel on the left where you can search by name or filter by tags on the packages.  Packages we will use include

| Name | Purpose |
| ---- | ----------- |
| CSV | read and write comma-separated-value files |
| CategoricalArrays | `factor`-like objects |
| DataFrames | data tables with properties and capabilities like R's `data.frame` |
| DataFramesMeta | database-like operations on data tables |
| MixedModels | fit and examine mixed-effects models |
| PooledArrays | light-weight version of categorical arrays |
| RCall | call R from Julia, including data transfers |
| RData | read data tables stored in `.rda` or `.rds` format |
| Tables | general data table structures - either row- or column-oriented |
| Weave | similar to the `knitr` package for R |

These packages must be added (similar to `package.install` in R) before they can be attached with `using` (similar to `library` or `require` in R).  In the package REPL (accessed by typing `]` as the first character of a line) just type `add Tables`, for example.  Note that you must have R installed on your computer to be able to successfully install the `RCall` package in Julia.

This document was created from the file `README.jmd` in this repository using `Weave` as
~~~~{.julia}

using Weave
weave("README.jmd", doctype="pandoc")
~~~~~~~~~~~~~




## Integrated Development Environments

Editing and running Julia code is supported [VS Code](https://code.visualstudio.com) and 
documented at https://www.julia-vscode.org

