---
order: 100
label: 
---

# What is OpenFlightHPC Compute?

OpenFlight Compute is the software environment designed to help researchers and scientists run their own high-performance compute research environment quickly and easily. The basic structure provided for users is as follows:

 - One gateway node, plus a configurable number of compute nodes
 - An Enterprise Linux operating system
 - A shared filesystem, mounted across all nodes
 - A batch job scheduler
 - Access to various libraries of software applications

OpenFlight Compute is designed to get researchers started with HPC as quickly as possible, providing a pre-configured environment which is ready for work immediately. The research environment you build is personal to you - users have root-access to the environment, and can setup and configure the system to their needs. 

Your research environment is designed to be **ephemeral** - i.e. you run it for as long as you need it, then shut it down. Although there is no built-in time limit for OpenFlight Compute research environments, the most effective way of sharing compute resources in the cloud is to book them out only when you need them. Contrary to popular belief, you can achieve huge cost savings over purchasing server hardware if you learn to work effectively in this way.

## Who is it for?


**OpenFlight Compute is designed for use by end-users** - that's the scientists, researchers, engineers and software developers who actually run compute workloads and process data. This documentation is designed to help these people to get the best out this environment, without needing assistance from teams of IT professionals. Flight provides tools which enable users to service themselves - it's very configurable, and can be expanded by individual users to deliver a scalable platform for computational workloads. 


## What doesn't it do?


**An important part of having ultimate power to control your environment is taking responsibility for it.** While no one is going to tell you how you should configure your research environment, you need to remember good security practice, and look after both your personal and research data. OpenFlight Compute provides you with a personal, single-user research environment - please use responsibility. OpenFlight Compute is not indended as a replacement for your national super-computer centre.

If you're running OpenFlight Compute on AWS, then there are some great tutorials written by the Amazon team on how to secure your environment. Just because you're running on public cloud, doesn't mean that your research environment is any less secure than a research environment running in your basement. Start at the [AWS Security Pages](https://aws.amazon.com/security), and talk to a security expert if you're still unsure.


