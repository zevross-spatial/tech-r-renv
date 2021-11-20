### Initialize renv only once

```r
renv::init()
install.packages("remotes")
renv::snapshot() # already up to date because remotes is dev dependency
```


### Example, install old dplyr

This gets installed in, sort of, a personal library separate from your main system library. So although you're installing "0.8.4", this is just the version in this project and if you close and open another project, it still uses the version associated with your system.

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

### Push to github and importantly note that renv.lock is in github but not the renv folder


### Pull from github to a new project as if you're a different person

You'll see that it gives a warning that "The project library is out of sync with the lockfile". It knows you're using `renv` and it sees the lock file. But if you type `packageVersion("dplyr")` you'll see that there is no package `dplyr`

### Restore the renv environment

This will install all the dependencies.

```r
renv::restore()
```

### If you update your dplyr and look at status

You will see that `dplyr` is "out of sync". And, in this case, it appears that the newer version of `dplyr` removed four dependencies. 


```r
install.packages("dplyr")
renv::status()
```

### You can abandon the update with `renv::restore()` or you can update with `renv::snapshot()`

If you use `restore` then it will undo the update and if you use `snapshot` it will save the update.

In this case I'll update and then push and then pull from the other account.

```r
renv::snapshot()
```
