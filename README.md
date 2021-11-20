### Initialize renv only once

```r
renv::init()
install.packages("remotes")
renv::snapshot() # already up to date because remotes is dev dependency
```


### Example, install old dplyr

```r
remotes::install_version("dplyr", "0.8.4")
```


### Confirm package version


```r
packageVersion("dplyr") #0.8.4
```

### `dplyr` not added to lockfile automatically


```r
renv::status() # still says lockfile up to date because dplyr is not being used
```

### Create script that references dplyr

The script will recognize that you're using dplyr if you use `library(dplyr)` or if you use `dplyr::` syntax.

### Check status again


```r
renv::status() # the following package(s) are installed but not recorded in the lockfile:
# list of packages associated with dplyr
```

### Update the lockfile with these packages

```r
renv::snapshot()
```


