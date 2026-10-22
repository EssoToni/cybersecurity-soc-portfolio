# Lab Limitations

## Purpose and Design Goals

The goal of this SOC lab is to demonstrate detection, correlation, investigation, and response. The priority is therefore to build an environment that supports those goals using the resources available, rather than to replicate a production-scale SOC.

This is a resource-constrained lab with only the minimal components needed for our activities.

## Environment Constraints

With 12 GB of physical RAM and 70 GB of storage, we built a small Wazuh SOC lab in VirtualBox. This required several compromises.

The main constraint is not Wazuh alone: it is running the Wazuh stack, Windows Server 2019, and Ubuntu within the same host.

## Resource Allocation Approach

Our resource allocations are not based on official vendor minimums. Instead, they are sized to guarantee a working environment for building an end-to-end detection workflow within our available resources.

## Operational Limits

Due to these constraints, we will only practice activities within the limits of our resources. This means:

- No excessive RAM- or CPU-consuming processes
- No high-volume data

## Progress and Evidence

The lab’s progress, findings, and evidence are available in the dedicated repository.