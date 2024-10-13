# Concepts

#hypervisors

---
# Virtual Machines
## Virtualization Types

- Hardware virtualization
- Server virtualization
- Storage virtualization
- Software virtualization
- OS virtualization
 
## Virtualization Tools

![|600](https://remnote-user-data.s3.amazonaws.com/-_lLtrTjN9lETsTbakNKWtYSPdazwUaf3L-o8uQNGw0Qo02HAnA6aDTmHP-TQ9DS6WgEX3FEWJs1uGxf7aV7qnQvfBW3MxLweN1lvfEBGaohGDDFWRJ_tO12fTQROPBl.png) 
 
## Hypervisors

![|600](https://remnote-user-data.s3.amazonaws.com/2QydkWvpDvayTOH8---wy7_akZfe3wHBtcTGkgWYbKW8crgMifOrCwwJE9c_f_odjOXsU3Gfn6aOqzafBZ7HlDwcux4L6ZcdCyOws2zNw1zuMBneN7FF_IPpMYZejgYg.png)

![|600](https://remnote-user-data.s3.amazonaws.com/BS7vqjvMrILRv8H3-3mSRcP8Xo02crzCoXGcCiYAeBOG-0EKGAxuRzDviwB3aa-SDYLGOxInxDTqr9-3ZuRdIc-EiLj6i0lcLBSUPzbTWx80EK8XSLRDAZFHcYeAHklU.png)

Capable hardware can virtualize many instances at once

Hypervisor virtualizes the hardware to install an OS and then an application
 
## Workstation Hypervisors

VMWare
- Commercial

VirtualBox
- Open Source
 
## Enterprise Hypervisors

Such as VMWare

Will often provide GUI for additional support

![|400](https://remnote-user-data.s3.amazonaws.com/6ug83LICKb31E47eU4zSFxGPrwZZrsmYTrxvy_QNxNzLn991nczBgOkL2D8BRK42Np-Xjc5PNk1WckpjbwKm1JMtbKySx8rBe90hY2e5RK9uDxvRKGqaTueXFvVvg6BH.png) 

## Hypervisors - Pass-Through

![|400](https://remnote-user-data.s3.amazonaws.com/f26BggGHvfAHHKb2tUdjbOK_P5qO_sOQNs7eoIqbcQhi4snTxnMSHYbzCwzbQ3Ff1zmcjNcCrFxTy60CNx2qYN-ChUXYcsdOeEPOo0WZpV9PFwdnoP_efFnxixfsvnl9.png) 

You can pass through actual hardware to a virtual machine
- e.g. A GPU
 
## Virtual Machine Vulnerabilities

- Virtual Machine Escape - The process of a program breaking out of a virtual machine and interacting with the host operating system
- Hyperjacking - Involves installing a malicious, fake hypervisor that can manage the entire server system
- Meltdown - Instead of attacking the hypervisor, you go from one instance of a virtual machine into another, bypassing the hypervisor and getting into the hardware
	- Breaks the most fundamental isolation between user applications and the operating system. The attack allows a program to access the memory of other programs on the operating system
- Spectre - Breaks the isolation between different applications. Allows an attacker to trick error-free programs, which follow best practises, into leaking information. Safety checks of these best practises increase the attack surface and may make applications more susceptible to Spectre
