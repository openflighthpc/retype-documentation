---
order: 100
label: Bowtie
icon: dot-fill
---

Bowtie is a sequencing toolset for aligning sets of DNA into large genomes.

## Workflow

### Installing Bowtie with Spack

!!!
The flight environment will need to be activated before the environments can be created so be sure to run `flight start` or [setup your environment to automatically activate the flight environment](/hpc_environment_usage/flight_overview/flight_system/#activating-the-flight-system).
!!!

- Create a spack software environment:

```bash
[flight@chead1 (mycluster1) ~]$ flight env create spack
```

- Activate the environment:

```bash
[flight@chead1 (mycluster1) ~]$ flight env activate spack
```
- Install bowtie:

```bash
<spack> [flight@chead1 (mycluster1) ~]$ spack install bowtie
```
### Running a Bowtie Job

- Download example ecoli data:

```bash
<spack> [flight@chead1 (mycluster1) ~]$ wget -O ecoli.fq https://raw.githubusercontent.com/BenLangmead/bowtie/master/reads/e_coli_1000.fq
```

- Create a job script in the current working directory:

```bash
<spack> [flight@chead1 (mycluster1) ~]$ cat << EOF > mybowtiejob.sh
#!/bin/bash -l
#SBATCH -N 1
flight env activate spack
spack load bowtie
bowtie-build ecoli.fq e_coli
EOF
```

- Submit the job to the queue:

```bash
<spack> [flight@chead1 (mycluster1) ~]$ sbatch mybowtiejob.sh
```

The results can then be reviewed from the slurm output file for the job in the current working directory. 
