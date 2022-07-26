---
order: 60
label: Package Ecosystems
icon:
---

The Flight Env command provides streamlined installation of many popular software management ecosystems. These can be seen below along with the features they provide.

|     &nbsp;             | Conda              | Easybuild          | Gridware           | Modules            | Singularity        | Spack              |
|------------------------|--------------------|--------------------|--------------------|--------------------|--------------------|--------------------|
| Dependency Management  | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :x:                | :heavy_check_mark: | :heavy_check_mark: |
| Compilation            | :heavy_check_mark: | :heavy_check_mark: | :x:                | :x:                | :x:                | :heavy_check_mark: |
| Preconfigured Binaries | :x:                | :heavy_check_mark: | :heavy_check_mark: | :x:                | :heavy_check_mark: | :small_blue_diamond:  |
| Multiple Versions      | :small_blue_diamond:  | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |


More information on the features:

  - **Dependency Management** - The ecosystem automatically resolves and installs dependencies
  - **Compilation** - The ecosystem builds software from source for optimised functionality on the system (Note: these sorts of installations will take a long time)
  - **Preconfigured Binaries** - The ecosystem provides binaries of the available software for quicker installation to get applications installed quickly
  - **Multiple Versions** - The ecosystem allows for installation of multiple versions of software which can be toggled between

:small_blue_diamond: is for partial support. Technically these features are supported in certain use cases and with additional work. This is not considered full support as multiple versions may require undocumented or uncommon use-cases of the tool. 



+++ [Conda](https://conda.io/)

Conda is an open source package management system and environment management system that runs on Windows, macOS and Linux. Conda quickly installs, runs and updates packages and their dependencies. Conda easily creates, saves, loads and switches between environments on your local computer. It was created for Python programs, but it can package and distribute software for any language.

# Conda Usage Example

## Creating and Using Ecosystem


Flight Env provides quick setup methods to create a conda software ecosystem. 

To install and use conda:

- [Activate the flight system.](/USE/working_with_user_suite/flight_system.md)
- Create the conda installation for the user:

```bash
[flight@gateway1 ~]$ flight env create conda
Creating environment conda@default
   > ✅ Verifying prerequisites
   > ✅ Fetching prerequisite (miniconda)
   > ✅ Creating environment (conda@default)
Environment conda@default has been created
```

- Activate the conda ecosystem:

```bash
[flight@gateway1 ~]$ flight env activate conda
(base) <conda> [flight@gateway1 ~]$
```

- Check that conda can be run:
```bash
(base) <conda> [flight@gateway1 ~]$ conda --version
conda 4.7.10
```

## Installing and Running Perl

An example workflow using perl is demonstrated below.

- View available versions:

```bash
(base) <conda> [flight@gateway1 ~]$ conda search perl
Loading channels: done
# Name                       Version           Build  Channel
perl                          5.26.0      hae598fd_0  pkgs/main
perl                          5.26.2      h14c3975_0  pkgs/main
```

- Install specific version:
```bash
(base) <conda> [flight@gateway1 ~]$ conda install perl=5.26.2
Collecting package metadata (current_repodata.json): done
Solving environment: done

## Package Plan ##

  environment location: /home/flight/.local/share/flight/env/conda+default

  added / updated specs:
    - perl=5.26.2


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    ca-certificates-2019.5.15  |                1         134 KB
    certifi-2019.6.16          |           py37_1         156 KB
    conda-4.7.11               |           py37_0         3.0 MB
    perl-5.26.2                |       h14c3975_0        10.5 MB
    ------------------------------------------------------------
                                           Total:        13.7 MB

The following NEW packages will be INSTALLED:

  perl               pkgs/main/linux-64::perl-5.26.2-h14c3975_0

The following packages will be UPDATED:

  ca-certificates                               2019.5.15-0 --> 2019.5.15-1
  certifi                                  2019.6.16-py37_0 --> 2019.6.16-py37_1
  conda                                       4.7.10-py37_0 --> 4.7.11-py37_0


Proceed ([y]/n)? y


Downloading and Extracting Packages
conda-4.7.11         | 3.0 MB    | ############################################################################################ | 100%
certifi-2019.6.16    | 156 KB    | ############################################################################################ | 100%
perl-5.26.2          | 10.5 MB   | ############################################################################################ | 100%
ca-certificates-2019 | 134 KB    | ############################################################################################ | 100%
Preparing transaction: done
Verifying transaction: done
    Executing transaction: done
```

- Check installation location:
```bash
(base) <conda> [flight@gateway1 ~]$ which perl
~/.local/share/flight/env/conda+default/bin/perl
```

- Install perl library (this may prompt for initial `cpan` configuration, once configuration is complete then the library will be installed):

```bash
    (base) <conda> [flight@gateway1 ~]$ cpan File::Slurp
    Loading internal null logger. Install Log::Log4perl for logging messages
    Reading '/home/flight/.cpan/Metadata'
      Database was generated on Mon, 09 Sep 2019 15:17:03 GMT
    Running install for module 'File::Slurp'
    <-- snip -->
```

- Check installation worked:
```bash

    (base) <conda> [flight@gateway1 ~]$ cpan File::Slurp
    Loading internal null logger. Install Log::Log4perl for logging messages
    Reading '/home/flight/.cpan/Metadata'
      Database was generated on Mon, 09 Sep 2019 15:17:03 GMT
    File::Slurp is up to date (9999.27).
```

+++ [Easybuild](https://easybuilders.github.io/easybuild/)

EasyBuild is a software build and installation framework that allows you to manage (scientific) software on High Performance Computing (HPC) systems in an efficient way.

### Usage Example



# Easybuild: Usage Example


## Creating and Using Ecosystem

Flight Env provides quick setup methods to create an easybuild software ecosystem. 

To install and use easybuild:

- [Activate the flight system.](/USE/working_with_user_suite/flight_system.md)
- Create the easybuild installation for the user:

```bash
[flight@gateway1 ~]$ flight env create easybuild
Creating environment easybuild@default
   > ✅ Verifying prerequisites
   > ✅ Fetching prerequisite (lua)
   > ✅ Extracting prerequisite (lua)
   > ✅ Building prerequisite (lua)
   > ✅ Installing prerequisite (lua)
   > ✅ Fetching prerequisite (tcl)
   > ✅ Extracting prerequisite (tcl)
   > ✅ Building prerequisite (tcl)
   > ✅ Installing prerequisite (tcl)
   > ✅ Fetching prerequisite (lmod)
   > ✅ Extracting prerequisite (lmod)
   > ✅ Configuring prerequisite (lmod)
   > ✅ Installing prerequisite (lmod)
   > ✅ Fetching prerequisite (easybuild)
   > ✅ Bootstrapping EasyBuild environment (easybuild@default)
Environment easybuild@default has been created
```

- Activate the easybuild ecosystem:
```bash
    [flight@gateway1 ~]$ flight env activate easybuild
    <easybuild> [flight@gateway1 ~]$
```
- Check that easybuild can be run:
```bash
    <easybuild> [flight@gateway1 ~]$ module load EasyBuild
    <easybuild> [flight@gateway1 ~]$ eb --version
    This is EasyBuild 3.9.4 (framework: 3.9.4, easyblocks: 3.9.4) on host gateway1.pri.basic.cluster.local.
```

## Installing and Running Perl

An example workflow using perl is demonstrated below.

- View available versions:
```bash
    <easybuild> [flight@gateway1 ~]$ eb -S perl
    CFGS1=/home/flight/.local/share/flight/env/easybuild+default/software/EasyBuild/3.9.4/lib/python2.7/site-packages/easybuild_easyconfigs-3.9.4-py2.7.egg/easybuild/easyconfigs
     * $CFGS1/a/annovar/annovar-2016Feb01-foss-2016a-Perl-5.22.1.eb
     * $CFGS1/b/Bio-DB-HTS/Bio-DB-HTS-2.11-foss-2017b-Perl-5.26.0.eb
     * $CFGS1/b/Bio-DB-HTS/Bio-DB-HTS-2.11-foss-2018b-Perl-5.28.0.eb
     * $CFGS1/b/Bio-DB-HTS/Bio-DB-HTS-2.11-intel-2017b-Perl-5.26.0.eb
    <-- snip -->
     * $CFGS1/p/Perl/Perl-5.26.1-GCCcore-6.4.0.eb
     * $CFGS1/p/Perl/Perl-5.26.1-foss-2018a-bare.eb
     * $CFGS1/p/Perl/Perl-5.26.1-foss-2018a.eb
     * $CFGS1/p/Perl/Perl-5.28.0-GCCcore-7.3.0.eb
     * $CFGS1/p/Perl/Perl-5.28.1-GCCcore-8.2.0.eb
    <-- snip -->
     * $CFGS1/y/YAML-Syck/YAML-Syck-1.27-goolf-1.4.10-Perl-5.16.3.eb
     * $CFGS1/y/YAML-Syck/YAML-Syck-1.27-ictce-5.3.0-Perl-5.16.3.eb

    Note: 9 matching archived easyconfig(s) found, use --consider-archived-easyconfigs to see them
```
- Install specific version:
```bash
    <easybuild> [flight@gateway1 ~]$ eb Perl-5.28.1-GCCcore-8.2.0.eb --robot
    == temporary log file in case of crash /tmp/eb-MdohD2/easybuild-J6tjhZ.log
    == resolving dependencies ...
    == processing EasyBuild easyconfig /home/flight/.local/share/flight/env/easybuild+default/software/EasyBuild/3.9.4/lib/python2.7/site-packages/easybuild_easyconfigs-3.9.4-py2.7.egg/easybuild/easyconfigs/m/M4/M4-1.4.18.eb
    == building and installing M4/1.4.18...
    == fetching files...
    == creating build dir, resetting environment...
    == unpacking...
    == patching...
    == preparing...
    == configuring...
    == building...
    <-- snip -->
```

- Check installation location:
```bash
    <easybuild> [flight@gateway1 ~]$ which perl
```
- Install perl library (this may prompt for initial ``cpan`` configuration, once configuration is complete then the library will be installed):
```bash
    <easybuild> [flight@gateway1 ~]$ cpan File::Slurp
    Loading internal null logger. Install Log::Log4perl for logging messages
    Reading '/home/flight/.cpan/Metadata'
      Database was generated on Mon, 09 Sep 2019 15:47:03 GMT
    Running install for module 'File::Slurp'
    <-- snip -->
```
- Check installation worked:
```bash
    <easybuild> [flight@gateway1 ~]$ cpan File::Slurp
    Loading internal null logger. Install Log::Log4perl for logging messages
    Reading '/home/flight/.cpan/Metadata'
      Database was generated on Mon, 09 Sep 2019 15:47:03 GMT
    File::Slurp is up to date (9999.27).
```


+++ [Gridware](https://gridware.alces-flight.com/)

Gridware provides pre-compiled binaries for many different scientific computing programs which can be installed quickly and loaded into the environment via modules.

### Usage Example


# Gridware: Usage Example


## Creating and Using Ecosystem


Flight Env provides quick setup methods to create a gridware software ecosystem. 

To install and use gridware:

- [Activate the flight system.](/USE/working_with_user_suite/flight_system.md)
- Create the gridware installation for the user:
```bash
    [flight@gateway1 ~]$ flight env create gridware
    Creating environment gridware@default
       > ✅ Verifying prerequisites
       > ✅ Fetching prerequisite (modules)
       > ✅ Extracting prerequisite (modules)
       > ✅ Building prerequisite (modules)
       > ✅ Installing prerequisite (modules)
       > ✅ Fetching prerequisite (gridware)
       > ✅ Extracting prerequisite (gridware)
       > ✅ Installing prerequisite (gridware)
       > ✅ Configuring repo: main
       > ✅ Configuring repo: volatile
       > ✅ Creating environment (gridware@default)
    Environment gridware@default has been created
```
- Activate the gridware ecosystem:
```bash
    [flight@gateway1 ~]$ flight env activate gridware
    <gridware> [flight@gateway1 ~]$
```
- Check that gridware can be run:
```bash
    <gridware> [flight@gateway1 ~]$ gridware --version
    gridware 1.5.1
```

## Installing and Running Perl


An example workflow using perl is demonstrated below.

- View available versions:
```bash
    <gridware> [flight@gateway1 ~]$ gridware search perl
    2 repositories need to update ...
    Updating repository: main
              Update ... OK (At: 55916fd)
    Updating repository: volatile
              Update ... OK (At: 61cc544)
    main/apps/bismark/0.16.3                  main/apps/bismark/0.17.0                  main/apps/cegma/2.5.0
    main/apps/clusterflow/0.6.0-20170502      main/apps/clusterflow/0.6.0-20170530      main/apps/forks/0.36
    main/apps/ihrsr/1.5                       main/apps/perl/5.20.2                     main/apps/python/2.7.8
    <-- snip -->
    volatile/apps/perl/5.16.1                 volatile/apps/perl/5.16.3                 volatile/apps/perl/5.18.0
    volatile/apps/perl/5.20.2                 volatile/apps/python/2.7.3                volatile/apps/python/2.7.5
    <-- snip -->
```
- Install specific version:
```bash
    <gridware> [flight@gateway1 ~]$ gridware install main/apps/perl/5.20.2
    Preparing to install main/apps/perl/5.20.2
    Installing main/apps/perl/5.20.2

     > Preparing package sources
            Download --> perl-5.20.2.tar.gz ... OK
              Verify --> perl-5.20.2.tar.gz ... OK
            Packaged --> CPAN-Config.pm     ... OK
            Packaged --> CPAN-MyConfig.pm   ... OK

     > Preparing for installation
               Mkdir ... OK (/home/flight/.cache/flight/env/build/gridware/src/apps/perl/5.20.2/gcc-4.8.5)
             Extract ... OK

     > Proceeding with installation
             Compile ... OK
               Mkdir ... OK (/home/flight/.local/share/flight/env/gridware+default/depots/23cd1570/el7/pkg/apps/perl/5.20.2/gcc-4.8.5)
             Install ... OK
              Module ... OK

    Installation complete.
```

- Check installation location:
```bash
    <gridware> [flight@gateway1 ~]$ module load apps/perl
    apps/perl/5.20.2/gcc-4.8.5
     | -- libs/gcc/system
     |    * --> OK
     |
     OK
    <gridware> [flight@gateway1 ~]$ which perl
    ~/.local/share/flight/env/gridware+default/depots/23cd1570/el7/pkg/apps/perl/5.20.2/gcc-4.8.5/bin/perl
```
- Install perl library (this may prompt for initial ``cpan`` configuration, once configuration is complete then the library will be installed):
```bash
    <gridware> [flight@gateway1 ~]$ cpan File::Slurp
    Reading '/home/flight/gridware/share/perl/5.20.2/cpan/Metadata'
      Database was generated on Tue, 10 Sep 2019 01:17:03 GMT
    Running install for module 'File::Slurp'
    <-- snip -->
    Appending installation info to /home/flight/gridware/share/perl/5.20.2/lib/5.20.2/x86_64-linux/perllocal.pod
      CAPOEIRAB/File-Slurp-9999.27.tar.gz
      /usr/bin/make install INSTALLMAN3DIR=/home/flight/gridware/share/perl/5.20.2/man/man3 INSTALLMAN1DIR=/home/flight/gridware/share/perl/5.20.2/man/man1 -- O
```
- Check installation worked:
```bash
    <gridware> [flight@gateway1 ~]$ cpan File::Slurp
    Reading '/home/flight/gridware/share/perl/5.20.2/cpan/Metadata'
      Database was generated on Tue, 10 Sep 2019 01:17:03 GMT
    File::Slurp is up to date (9999.27).
```


+++ [Modules](http://modules.sourceforge.net/)

Modules provides simple environment management. Tools and software to be used with modules will be compiled or installed outside of the modules environment.

### Usage Example

# Modules: Usage Example


## Creating and Using Ecosystem


Flight Env provides quick setup methods to create a modules software ecosystem. 

To install and use modules:

- [Activate the flight system.](/USE/working_with_user_suite/flight_system.md)
- Create the modules installation for the user:
```bash
    [flight@gateway1 ~]$ flight env create modules
    Creating environment modules@default
       > ✅ Verifying prerequisites
       > ✅ Fetching prerequisite (modules)
       > ✅ Extracting prerequisite (modules)
       > ✅ Building prerequisite (modules)
       > ✅ Installing prerequisite (modules)
       > ✅ Creating environment (modules@default)
    Environment modules@default has been created
```
- Activate the modules ecosystem:
```bash
    [flight@gateway1 ~]$ flight env activate modules
    <modules> [flight@gateway1 ~]$
```
- Check that modules can be run:
```bash
    <modules> [flight@gateway1 ~]$ module --version
    Modules Release 4.3.0 (2019-07-26)
```

## Installing Software - General Overview


Unlike the other :ref:`package ecosystems <package-ecosystems>`, modules provides the ecosystem management tool but not any package management tools. Therefore, with the modules ecosystem, you are free to compile and install software in a module compatible manner.

Module files can be installed to `~/.local/share/flight/env/modules+default/modulefiles` (for local modules ecosystems) or to `/opt/apps/flight/env/modules+global/modulefiles` (for global modules ecosystems).

!!!
If the modules ecosystem has been installed with a [custom ecosystem name](/USE/working_with_user_suite/flight_environment/#custom-ecosystem-names) then the path will not be `modules+default`/`modules+global` but instead `modules+mycustomname`
!!!

For more information on building software for modules, see the `modulefile reference <https://modules.readthedocs.io/en/latest/modulefile.html>`_ and build documentation for the chosen software.


## Installing and Running Perl


### Compile Perl from Source


- Download perl 5.30.1 source:
```bash
    <modules> [flight@gateway1 ~]$ wget https://www.cpan.org/src/5.0/perl-5.30.1.tar.gz
```
- Decompress the source files:
```bash
    <modules> [flight@gateway1 ~]$ tar -xzf perl-5.30.1.tar.gz
```
- Configure the software to install to a localperl directory:
```bash
    <modules> [flight@gateway1 ~]$ cd perl-5.30.1
    <modules> [flight@gateway1 ~]$ ./Configure -des -Dprefix=$HOME/localperl
```
- Compile and install perl:
```bash
    <modules> [flight@gateway1 ~]$ make
    <modules> [flight@gateway1 ~]$ make install
```
### Create Modulefile and Test


- Create the perl modulefile:
```bash
    <modules> [flight@gateway1 ~]$ cat << EOF > ~/.local/share/flight/env/modules+default/modulefiles/perl-5.30.1
    #%Module1.0
    proc ModulesHelp { } {
    global dotversion

    puts stderr "\tPerl 5.30.1"
    }

    module-whatis "Perl 5.30.1"
    conflict perl
    prepend-path PATH ~/localperl/bin
    prepend-path LD_LIBRARY_PATH ~/localperl/lib
    prepend-path LIBRARY_PATH ~/localperl/lib
    prepend-path MANPATH ~/localperl/man
    EOF
```
- Check install location:
```bash
    <modules> [flight@gateway1 ~]$ module load perl-5.30.1
    <modules> [flight@gateway1 ~]$ which perl
    ~/localperl/bin/perl
```
- Install perl library (this may prompt for initial `cpan` configuration, once configuration is complete then the library will be installed):
```bash
    <modules> [flight@gateway1 ~]$ cpan File::Slurp
    Loading internal logger. Log::Log4perl recommended for better logging
    Reading '/home/flight/.cpan/Metadata'
      Database was generated on Wed, 11 Mar 2020 15:29:03 GMT
    <-- snip -->
    Appending installation info to /home/flight/localperl/lib/5.30.1/x86_64-linux/perllocal.pod
      CAPOEIRAB/File-Slurp-9999.30.tar.gz
      /usr/bin/make install  -- OK
```
- Check installation worked:
```bash
    <modules> [flight@gateway1 ~]$ cpan File::Slurp
    Loading internal logger. Log::Log4perl recommended for better logging
    Reading '/home/flight/.cpan/Metadata'
      Database was generated on Wed, 11 Mar 2020 15:29:03 GMT
    File::Slurp is up to date (9999.30).
```


+++ [Singularity](https://www.sylabs.io/)

Singularity is high-performance container technology specifically designed to enhance Enterprise Performance Computing by building containers that support HPC, analytics, artificial intelligence, machine learning, and deep learning to provide â€œintelligence anywhere.â€

### Usage Example

# Singularity: Usage Example


## Creating and Using Ecosystem


Flight Env provides quick setup methods to create a singularity software ecosystem. 

To install and use singularity:

!!! 
If installing singularity for a user then there are a number of restrictions and additional steps to consider in configuring the environment. See the `Personal Environment` section of `flight env info singularity`. 
!!!

- [Activate the flight system.](/USE/working_with_user_suite/flight_system.md)
- Create the singularity installation for the user:
```bash
    [flight@gateway1 ~]$ flight env create singularity
    Creating environment singularity@default
       > ✅ Verifying prerequisites
       > ✅ Fetching prerequisite (squashfs)
       > ✅ Extracting prerequisite (squashfs)
       > ✅ Building prerequisite (squashfs)
       > ✅ Installing prerequisite (squashfs)
       > ✅ Fetching prerequisite (go)
       > ✅ Extracting prerequisite (go)
       > ✅ Fetching prerequisite (singularity)
       > ✅ Extracting prerequisite (singularity)
       > ✅ Building prerequisite (singularity)
       > ✅ Installing prerequisite (singularity)
       > ✅ Creating environment (singularity@default)
    Environment singularity@default has been created
```
- Activate the singularity ecosystem:
```bash
    [flight@gateway1 ~]$ flight env activate singularity
    <singularity> [flight@gateway1 ~]$
```
- Check that singularity can be run:
```bash
    <singularity> [flight@gateway1 ~]$ singularity --version
    singularity version 3.2.1
```

## Installing and Running Perl


An example workflow using perl is demonstrated below.

!!!
The perl container is built from a docker container which can be searched for in the [docker hub](https://hub.docker.com/). To search the singularity container library, use `singularity search SEARCHTERM`.
!!!

- Install specific version:
```bash
    <singularity> [flight@gateway1 ~]$ singularity build --sandbox perl_5.30.simg docker://perl:5.30
    INFO:    Starting build...
    Getting image source signatures
    Copying blob sha256:4ae16bd4778367b46064f39554128dd2fda2803a5747fddeff74059f353391c9
     48.05 MiB / 48.05 MiB [====================================================] 0s
    Copying blob sha256:bbab4ec87ac4f89eaabdf68dddbd1dd930e3ad43bded38d761b89abf9389a893
     7.44 MiB / 7.44 MiB [======================================================] 0s
    <-- snip -->
    Writing manifest to image destination
    Storing signatures
    INFO:    Creating sandbox directory...
    INFO:    Build complete: perl_5.30.simg
```
- Check installation location:
```bash
    <singularity> [flight@gateway1 ~]$ singularity exec perl_5.30.simg which perl
    /usr/local/bin/perl
```
- Install perl library (this may prompt for initial ``cpan`` configuration, once configuration is complete then the library will be installed):
```bash
    <singularity> [flight@gateway1 ~]$ singularity exec -w perl_5.30.simg cpan File::Slurp
    INFO:    Convert SIF file to sandbox...
    perl: warning: Setting locale failed.
    perl: warning: Please check that your locale settings:
        LANGUAGE = (unset),
        LC_ALL = (unset),
        LC_CTYPE = "en_GB.UTF-8",
        LANG = "en_GB.UTF-8"
        are supported and installed on your system.
    perl: warning: Falling back to the standard locale ("C").
    Loading internal null logger. Install Log::Log4perl for logging messages
    Reading '/home/flight/.cpan/Metadata'
      Database was generated on Wed, 11 Sep 2019 13:29:02 GMT
    Running install for module 'File::Slurp'
    <-- snip -->
```
- Check installation worked:
```bash
    <singularity> [flight@gateway1 ~]$ singularity exec perl_5.30.simg cpan File::Slurp
    perl: warning: Setting locale failed.
    perl: warning: Please check that your locale settings:
        LANGUAGE = (unset),
        LC_ALL = (unset),
        LC_CTYPE = "en_GB.UTF-8",
        LANG = "en_GB.UTF-8"
        are supported and installed on your system.
    perl: warning: Falling back to the standard locale ("C").
    Loading internal logger. Log::Log4perl recommended for better logging
    Reading '/home/flight/.cpan/Metadata'
      Database was generated on Wed, 11 Sep 2019 13:29:02 GMT
    File::Slurp is up to date (9999.27).
```


+++ [Spack](https://spack.io/)

Spack is a package manager for supercomputers, Linux, and macOS. It makes installing scientific software easy. With Spack, you can build a package with multiple versions, configurations, platforms, and compilers, and all of these builds can coexist on the same machine.

### Usage Example

# Spack: Usage Example


## Creating and Using Ecosystem


Flight Env provides quick setup methods to create a spack software ecosystem. 

To install and use spack:

- :ref:`Activate the flight system <activate-flight-system>`
- Create the spack installation for the user:
```bash
    [flight@gateway1 ~]$ flight env create spack
    Creating environment spack@default
       > ✅ Verifying prerequisites
       > ✅ Fetching prerequisite (spack)
       > ✅ Extracting Spack hierarchy (spack@default)
       > ✅ Bootstrapping Spack environment (spack@default)
    Environment spack@default has been created
```
- Activate the spack ecosystem:
```bash
    [flight@gateway1 ~]$ flight env activate spack
    <spack> [flight@gateway1 ~]$
```
- Check that spack can be run:
```bash
    <spack> [flight@gateway1 ~]$ spack --version
    spack 0.12.1
```

## Installing and Running Perl


An example workflow using perl is demonstrated below.

- View available versions:
```bash
    <spack> [flight@gateway1 ~]$ spack list perl
    ==> 148 packages.
    perl                          perl-extutils-pkgconfig     perl-math-cdf                    perl-sub-uplevel
    perl-algorithm-diff           perl-file-copy-recursive    perl-math-cephes                 perl-svg
    perl-app-cmd                  perl-file-listing           perl-math-matrixreal             perl-swissknife
    perl-array-utils              perl-file-pushd             perl-module-build                perl-task-weaken
    perl-b-hooks-endofscope       perl-file-sharedir-install  perl-module-implementation       perl-term-readkey
    <-- snip -->

    <spack> [flight@gateway1 ~]$ spack info perl
    Package:   perl

    Description:
        Perl 5 is a highly capable, feature-rich programming language with over
        27 years of development.

    Homepage: http://www.perl.org

    Tags:
        None

    Preferred version:
        5.26.2     http://www.cpan.org/src/5.0/perl-5.26.2.tar.gz

    Safe versions:
        5.28.0     http://www.cpan.org/src/5.0/perl-5.28.0.tar.gz
        5.26.2     http://www.cpan.org/src/5.0/perl-5.26.2.tar.gz
```
- Install specific version:
```bash
    <spack> [flight@gateway1 ~]$ spack install perl@5.26.2
    ==> Installing pkgconf
    ==> Searching for binary cache of pkgconf
    ==> Warning: No Spack mirrors are currently configured
    ==> No binary for pkgconf found: installing from source
    ==> Fetching http://distfiles.alpinelinux.org/distfiles/pkgconf-1.4.2.tar.xz
    <-- snip -->
    ==> Successfully installed perl
      Fetch: 0.83s.  Build: 2m 31.21s.  Total: 2m 32.04s.
    [+] /home/flight/.local/share/flight/env/spack+default/opt/spack/linux-centos7-x86_64/gcc-4.8.5/perl-5.26.2-wavwojlef7lshvx2awf4zze2lrx5l7l4
```
- Check installation location:
```bash
    <spack> [flight@gateway1 ~]$ module load perl-5.26.2-gcc-4.8.5-wavwojl
    <spack> [flight@gateway1 ~]$ which perl
    ~/.local/share/flight/env/spack+default/opt/spack/linux-centos7-x86_64/gcc-4.8.5/perl-5.26.2-wavwojlef7lshvx2awf4zze2lrx5l7l4/bin/perl
```
- Install perl library (this may prompt for initial ``cpan`` configuration, once configuration is complete then the library will be installed)::
```bash
    <spack> [flight@gateway1 ~]$ cpan File::Slurp
    Loading internal null logger. Install Log::Log4perl for logging messages
    Reading '/home/flight/.cpan/Metadata'
      Database was generated on Wed, 11 Sep 2019 14:41:02 GMT
    Running install for module 'File::Slurp'
    <-- snip -->
```
- Check installation worked:
```bash
    <spack> [flight@gateway1 ~]$ cpan File::Slurp
    Loading internal null logger. Install Log::Log4perl for logging messages
    Reading '/home/flight/.cpan/Metadata'
      Database was generated on Wed, 11 Sep 2019 14:41:02 GMT
    File::Slurp is up to date (9999.27).
```
+++