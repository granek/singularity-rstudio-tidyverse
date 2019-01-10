BootStrap: shub
From: nickjer/singularity-rstudio

%labels
  Maintainer Josh Granek
#  RStudio_Version 1.1.463

%help
  This will run RStudio Server with tidyverse and support for knitting

%apprun rserver
  exec rserver "${@}"

%runscript
  exec rserver "${@}"

%environment
  export PATH=/usr/lib/rstudio-server/bin:${PATH}

%post
  # Install tidyverse and packages necessary for knitting to HTML 
   Rscript -e "install.packages(pkgs = c('tidyverse','caTools','rprojroot'), \
     repos='https://cran.revolutionanalytics.com/', \
     dependencies=TRUE, \
     clean = TRUE)"
