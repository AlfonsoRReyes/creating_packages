# README


1. Install these packages: `devtools`, `roxygen2`, 


2. Inside RStudio or R, load the package `devtools` first and run:

```
# no spaces, no underscores, no dashes
create("C:/Users/ptech/git.projects/CreatingPackages")   
```


Quit RStudio or R and from the command line, create a git repository with:

```
cd CreatingPackages
git init
```



Open RStudio and push the original structure just created.

Modify the file `DESCRIPTION` and add this line at the end:

```
VignetteBuilder: knitr
```



Add these folders: `data`, `inst`, `inst/extdata` to the project root.

Copy these raw data files to `inst/extdata`:

We will use these files for processing later. All processed data will go to `./data`



Under `Roxygen Options` check `Vignettes` and `Build & Reload`



Run for the first time from `Build` with `Build and Reload`. There should be no errors. Take a look at the output:

```
==> devtools::document(roclets=c('rd', 'collate', 'namespace', 'vignette'))

Updating CreatingPackages documentation
Loading CreatingPackages
Updating roxygen version in  C:\Users\ptech\git.projects\CreatingPackages/DESCRIPTION 
Writing NAMESPACE
Updating vignettes
Documentation completed

==> Rcmd.exe INSTALL --no-multiarch --with-keep.source CreatingPackages

* installing to library 'C:/Users/ptech/Documents/R/win-library/3.3'
* installing *source* package 'CreatingPackages' ...
** inst
No man pages found in package  'CreatingPackages' 
** help
*** installing help indices
** building package indices
** installing vignettes
** testing if installed package can be loaded
* DONE (CreatingPackages)
```

The `man` folder is created during this process. 

* Commit and push these changes.

Main folder structure:

```

-<>-|---- data
	|---- inst
			|---- extdata
	|---- R
	|---- src
	|---- vignettes


```



* Copy these two files `ismbTweetAnalysis-package.r` and `ismb_analysis.Rmd` to the `R` and `vignettes` folders respectively. These files are almost ready to work. We will make couple of changes. Commit and push these two files.

* We will run another `BaR` (build and reload) to check all is working ok. There shouldn't be any errors. Take a look at the output:

```
  ==> devtools::document(roclets=c('rd', 'collate', 'namespace', 'vignette'))

  Updating CreatingPackages documentation
  Loading CreatingPackages
  Writing ismbTweetAnalysis.Rd
  Writing ismb2012.Rd
  Writing readTweetData.Rd
  Writing ismb2014.Rd
  Writing tweetCounts.Rd
  Writing retweetCount.Rd
  Writing tweetRank.Rd
  Writing totalRT.Rd
  Writing NAMESPACE
  Updating vignettes
  Documentation completed

  ==> Rcmd.exe INSTALL --no-multiarch --with-keep.source CreatingPackages

  * installing to library 'C:/Users/ptech/Documents/R/win-library/3.3'
  * installing *source* package 'CreatingPackages' ...
  ** R
  ** inst
  ** preparing package for lazy loading
  ** help
  *** installing help indices
  ** building package indices
  ** installing vignettes
  ** testing if installed package can be loaded
  * DONE (CreatingPackages)
```

  Notice that the functions are now documented as `Rd` files under the `man` folder.

  

* We will chose to ignore the files under `man` until the end since this process will happen many time automatically. The same we will do with NAMESPACE. Otherwise, we will require to commit these files after `BaR`. Do this from the `Git` tab panel.

* Commit the `.gitignore` and `NAMESPACE`.

* Run `Build and Reload` and since there is no change in the sources there shouldn't be any notifications ion the `Git` tab panel.

## Check if the notebook is running

We will modify the notebook a little bit. Staring with the objects `baseLoc` and `extPath`. Modify the first chunk into this:


<pre><code>```{r datamunging}
baseLoc <- system.file(package="ismbTweetAnalysis")
extPath <- file.path(baseLoc, "extdata")
baseLoc
extPath
```</code></pre>


Run the chunk. Your output would look to something like this:

```
[1] "C:/Users/ptech/Documents/R/win-library/3.3/CreatingPackages"
[1] "C:/Users/ptech/Documents/R/win-library/3.3/CreatingPackages/extdata"
```

This is important because we will use this technique to get the relative paths to our files under `data` and under `inst/data`



Notes

The folder doesn't need to be created; it is created by `devtools`.