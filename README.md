
<!-- README.md is generated from README.Rmd. Please edit that file -->
ramlegacy
=========

[![Travis Build Status](https://travis-ci.com/kshtzgupta1/ramlegacy.svg?branch=master)](https://travis-ci.com/kshtzgupta1/ramlegacy) [![AppVeyor Build Status](https://ci.appveyor.com/api/projects/status/github/kshtzgupta1/ramlegacy?branch=master&svg=true)](https://ci.appveyor.com/project/kshtzgupta1/ramlegacy) [![Coverage status](https://codecov.io/gh/kshtzgupta1/ramlegacy/branch/master/graph/badge.svg)](https://codecov.io/github/kshtzgupta1/ramlegacy?branch=master) [![Project Status: WIP – Initial development is in progress, but there has not yet been a stable, usable release suitable for the public.](https://www.repostatus.org/badges/latest/wip.svg)](https://www.repostatus.org/#wip) [![](https://badges.ropensci.org/264_status.svg)](https://github.com/ropensci/software-review/issues/264)

-   **Authors**: Kshitiz Gupta, [Carl Boettiger](http://www.carlboettiger.info/)
-   **License**: [MIT](http://opensource.org/licenses/MIT)
-   [Package source code on Github](https://github.com/kshtzgupta1/ramlegacy)
-   [**Submit Bugs and feature requests**](https://github.com/kshtzgupta1/ramlegacy/issues)

`ramlegacy` is an R package that supports caching and reading in different versions (including older ones) of the RAM Legacy Stock Assessment Data Base, an online compilation of stock assessment results for commercially exploited marine populations from around the world. More information about the database can be found [here.](http://ramlegacy.org)

What does `ramlegacy` do?
-------------------------

-   Provides a function `download_ramlegacy()`, to download all the available
    versions of the RAM Legacy Stock Assessment Excel Database as RDS objects. This way once a version has been downloaded it doesn't need to be re-downloaded for subsequent analysis.
-   Supports reading in specified dataframes from any particular cached version of the database through a function called `load_ramlegacy()`
-   Provides a function `ram_dir()` to view the path where the downloaded database is saved.

Installation
------------

You can install the development version from [GitHub](https://github.com/kshtzgupta1/ramlegacy) with:

``` r
install.packages("devtools")
library(devtools)
install_github("kshtzgupta1/ramlegacy")
```

To ensure that the vignette is installed along with the package make sure to remove `--no-build-vignettes` from the `build_opts` in `install_github`

Usage
-----

Please see the ramlegacy [vignette](https://kshtzgupta1.github.io/ramlegacy/articles/ramlegacy.html) for more detailed examples and additional package functionality.

Start by loading the package using `library`.

``` r
library(ramlegacy)
```

### download\_ramlegacy

`download_ramlegacy()` downloads the specified version of **RAM Legacy Stock Assessment Excel Database** and then saves it as an RDS object in user’s application data directory as detected by the [rappdirs](https://cran.r-project.org/web/packages/rappdirs/index.html) package. This location is also where `load_ramlegacy()` will look for the downloaded database.

``` r
# downloads version 3.0
download_ramlegacy(version = "3.0")
```

If version is not specified then `download_ramlegacy` defaults to downloading the latest version :

``` r
# downloads current latest version 4.44
download_ramlegacy()
```


### load\_ramlegacy

After the specified version of the database has been downloaded through `download_ramlegacy`, `load_ramlegacy` can be used to return a list of particular dataframes within the database. To get a list of all the dataframes within a specific version of the database set `tables` = NULL.  If If version is not specified then `load_ramlegacy` defaults to the latest version (currently 4.44)  :

```{r, load_ramlegacy_example1, echo = T, eval = F}
# returns a list containing area and bioparams tables from version 4.44 database
load_ramlegacy(version = "4.44", tables = c("area", "bioparams"))

# the latest version (currently 4.44)
load_ramlegacy()
```

### ram\_dir

To view the exact local path where a certain version of the database was downloaded and cached by `download_ramlegacy` you can run `ram_dir(vers = 'version')`, specifying the version number inside the function call:

``` r
# downloads version 4.44
download_ramlegacy(version = "4.44")

# view the location where version 4.44 of the database was downloaded and cached
ram_dir(vers = "4.44")
```

Similar Projects
----------------

1.  [`ramlegacy`](https://github.com/seananderson/ramlegacy) Sean Anderson has a namesake package that appears to be a stalled project on GitHub (last updated 9 months ago). However, unlike this package which supports downloading and reading in the Excel version of the database, Sean Anderson's project downloads the Microsoft Access version and converts it to a local sqlite3 database.

2.  [`RAMlegacyr`](https://github.com/ashander/RAMlegacyr) `RAMlegacyr` is an older package last updated in 2015. Similar to Sean Anderson's project, the package seems to be an R interface for the Microsoft Access version of the RAM Legacy Stock Assessment Database and provides a set of functions using RPostgreSQL to connect to the database.

Citation
--------

Use of the RAM Legacy Stock Assessment Database is subject to a [Fair Use Policy.](http://ramlegacy.marinebiodiversity.ca/ram-legacy-stock-assessment-database/ram-legacy-stock-assessment-database-fair-use-policy)

Please cite the paper associated with RAM Legacy Stock Assessment Database as follows:

Ricard, D., Minto, C., Jensen, O.P. and Baum, J.K. (2013) Evaluating the knowledge base and status of commercially exploited marine species with the RAM Legacy Stock Assessment Database. Fish and Fisheries 13 (4) 380-398. DOI: 10.1111/j.1467-2979.2011.00435.x

If you are using any of the older versions(1.0, 2.0, 2.5, 3.0, 4.3) then please cite the paper.

If you are using any of the latest versions(4.40¸ 4.41, 4.44) then please cite the paper and see the zenodo doi for instructions to add the relevant citation for the latest versions.
