---
order: 100
label: What is the Flight User Suite?
icon: dot-fill
---

# What is the Flight User Suite?

The Flight User Suite is a collection of environment tools that provide users with easy and intuitive ways to manage the software and desktop sessions in a research environment. The purpose of these tools is to get researchers started with HPC as quickly as possible without needing to worry about their environment, leaving them to do what they do best - research!

The tools are non-intrusive to the research environment, defaulting to a "deactivated" state. Leaving admins and users free to configure and utilise their systems how they want.

Flight User Suite is made up of the following tools:

- Runway: Flight Runway provides a self-contained Ruby environment and an entrypoint for accessing the other flight tools
- Env: Flight Env provides access to, and management of, various software managers to ensure access to a wide variety of HPC applications
- Desktop: Flight Desktop provides an intuitive tool for launching VNC-ready virtual desktops of many different desktop environments (gnome, xterm, kde, etc)
- Starter: Flight Starter provides profile scripts for integrating the user suite into the shell environment
- Job: Flight Job Manager allows you to create and manage customized job scripts from predefined templates, launch jobs and monitor their activity.


# What is the Flight User Suite?

The Flight User Suite is a software environment designed to help researchers and scientists run their own high-performance compute research environment quickly and easily. The basic structure provided for users is as follows:

 - One gateway node, plus a configurable number of compute nodes
 - An Enterprise Linux operating system
 - A shared filesystem, mounted across all nodes
 - A batch job scheduler
 - Access to various libraries of software applications

The Flight User Suite is designed to get researchers to make the most of their HPC. The research environment you build is personal to you - users have root-access to the environment, and can setup and configure the system to their needs. 

## Who is it for?


**The Flight User Suite is designed for use by end-users** - that's the scientists, researchers, engineers and software developers who actually run compute workloads and process data. This documentation is designed to help these people to get the best out this environment, without needing assistance from teams of IT professionals. Flight provides tools which enable users to service themselves - it's very configurable, and can be expanded by individual users to deliver a scalable platform for computational workloads. 


## What doesn't it do?


**An important part of having ultimate power to control your environment is taking responsibility for it.** While no one is going to tell you how you should configure your research environment, you need to remember good security practice, and look after both your personal and research data. The Flight User Suite provides you with a personal, single-user research environment - please use responsibility. The Flight User Suite is not indended as a replacement for your national super-computer centre.

If you're running the Flight User Suite on AWS, then there are some great tutorials written by the Amazon team on how to secure your environment. Just because you're running on public cloud, doesn't mean that your research environment is any less secure than a research environment running in your basement. Start at the [AWS Security Pages](https://aws.amazon.com/security), and talk to a security expert if you're still unsure.


