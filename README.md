# README #

This repository contains an R package template supporting the use of the Rcpp and/or RcppArmadillo packages. The package template has been configured as an RStudio project, and the following instructions assume you have [RStudio](https://www.rstudio.com/) installed. To make full use of RStudio, the [devtools](https://cran.r-project.org/web/packages/devtools/index.html) R package should also be installed. The package template includes both `R` and `C++` code, so a [suitable](https://cran.r-project.org/doc/manuals/r-release/R-admin.html) `C++` compiler must be available to build the package from source.

1. [Configuring RStudio for Git via SSH](#configuring-rstudio-for-git-via-ssh)
2. [Registering your SSH public key with GitHub](#registering-your-ssh-public-key-with-github)
3. [Cloning the project repository with RStudio](#cloning-the-project-repository-with-rstudio)
4. [Building and running the package template project with RStudio](#building-and-running-the-package-template-project-with-rstudio)

### Configuring RStudio for Git via SSH

The package source code is stored in a Git repository, which is accessible using the SSH (**S**ecure **SH**ell) protocol. Connecting to a remote Git repository requires a Git client be installed on your system. To establish if RStudio has recognized your Git installation, click on the __Tools__ menu and select __Global Options...__ (this dialog may load slowly the first time it is opened). Click on __Git/SVN__ in the left panel, and make sure the checkbox __Enable version control interface for RStudio projects__ has been selected (RStudio may need to be restarted after turning this feature on or off).

![RStudio global options](./readme/SSHKey.png)

If the __Git executable__ is __(Not Found)__, you probably need to install a Git client; for instructions click [here](https://www.atlassian.com/git/tutorials/install-git) (or just google it).

Once RStudio has recognized your Git installation, check to see if it has found a __SSH RSA Key:__ 

1. If the __SSH RSA Key__ is __(None)__, make one by clicking the __Create RSA Key...__ button. Using a passphrase is more secure, albeit less convenient.  
![Create RSA Key](./readme/CreateRSAKey.png)

2. If the __SSH RSA Key__ is the one you want to use, nothing needs to be done.
    
3. If the __SSH RSA Key__ is not the one you want to use, complain to RStudio, because as far as I can tell it cannot be changed by the user. In Linux a workaround is to set the environment variable `GIT_SSH_COMMAND='ssh -i /path/to/alternate/key/id_rsa'` before running RStudio, overriding the default key selection.

The RSA public key will be used to identify and authenticate you when connecting to the Git host via SSH. In cases 1 and 2 above, you can access this file by clicking __View public key__. This key must be registered with the Git host, so you may want to copy and paste it into a temporary text file.

![RSA public key](./readme/PublicKey.png)

In case 3 above, it is assumed that anyone using something other than the default knows how to find the appropriate public key.

### Registering your SSH public key with GitHub

To register your public key, log in to GitHub and click on your avatar, which is located in the top right of the page and defaults to the image ![Avatar](./readme/GitHubAvatar.png). From there, select __Settings__, and then click on __SSH and GPG keys__ in the left panel.

Next, click on __New SSH key__, and paste the public key from before into the text box. A title is optional but recommended, particularly with multiple keys. Press the __Add SSH key__ button when finished.

![GitHub add key](./readme/GitHubAddKey.png)

### Cloning the project repository with RStudio

With RStudio configured for Git, and your SSH key registered with the Git host, you are ready to clone the package template project repository. From the __File__ menu select __New Project...__, then click on __Version Control__ followed by __Git__. Enter *git@github&#46;com:patrickmuchmore/RPackageTemplate.git* for the __Repository URL__, and leave the __Project directory name__ at its default value. When the repository is cloned, a new directory named *RPackageTemplate* will be created. 

![Cloning a repository with Git and RStudio](./readme/CloneGitRepo.png)

The field __Create project as subdirectory of__ indicates where the *RPackageTemplate* directory will be created. To specify an alternate location, click __Browse...__ and navigate to the desired file system path. If __Open in new session__ is checked, once the clone operation is complete RStudio will automatically open the project. After setting the appropriate option values, click the __Create Project__ button to clone the repository using Git. 

The first time you connect to a remote host (such as github.com), you may receive an SSH security message asking you to confirm before continuing. You must type __yes__ to continue, simply hitting __OK__ will terminate the connection.

![SSH Host Auth](./readme/HostAuth.png)

### Building and running the package template project with RStudio

To build and run the project, it must be open in RStudio (this should already be the case if __Open in new session__ was selected). If the project is not open, click on __File__ and select __Open Project...__, then navigate to the newly created *RPackageTemplate* folder and open the *RPackageTemplate.Rproj* file (the *.Rproj* extension denotes a configuration file for an RStudio project). When the project is open, one of the panes in the RStudio window should have a series of tabs including __Environemnt__, __History__, __Build__, and __Git__ (the RStudio interface can be customized by selecting __Pane Layout__ from the left panel of the __Global Options__ dialog). Click on the tab labeled __Build__.

![Cloning a repository with Git and RStudio](./readme/BuildTab.png)

Clicking the __Build & Reload__ button causes R to compile and load the contents of the project directory. Because the project contains `C++` code, you should see some lines of compiler output. The package is then installed, and as with any R package, if this completes successfully the last few lines of output will look like:

    ** testing if installed package can be loaded
    * DONE (RPackageTemplate)

Assuming the package has been built successfully, it is automatically (re)loaded by calling `library(RPackageTemplate)`. To verify the package installation, you can run the included "hello world" function `rcpparma_hello_world`, which should return a 3x3 matrix that has seven on the diagonal and zero elsewhere.

    >rcpparma_hello_world()
         [,1] [,2] [,3]
    [1,]    7    0    0
    [2,]    0    7    0
    [3,]    0    0    7
