# Embedded SIG Target Platforms

## Purpose of this Document

This document defines the minimum hardware and software platforms that all contributions to the Embedded Special Interest Group should address. This document should define what devices and software platforms are in scope (targeted), and also what devices and platforms are out of scope.  

## Intended Audience

This document is intended to be read and contributed to by members of the Embedded Special Interest Group. 

## Criteria of Device and Software Selection

The hardware and software targeted in this document should be easily available to anyone who would like to contribute to the Embedded Special Interest Group. This means not just specifying a CPU architecture or model, but specifying a development platform / board which can be easily purchased by anyone wishing to contribute.

### What do we mean by "Target Platform"

As a Special Interest Group we will discuss new software features for WebAssembly and new interfaces for WASI. When we consider these new software features we should keep in mind that any implementation will need to address a minimum set of hardware and operating system features. This document aims to define these minimum requirements.

### How do we use the "Target Platform"

Please be aware that this doesn't mean that other platforms are excluded, but only that the special interest group will focus on the subset defined in this document. For a new feature to be recommended by the Embedded Special Interest Group it should address these minimum hardware and operating system requirements.

### The Impact of "Moore's Law" on the Embedded Ecosystem

Moore's law is continuing to impact the embedded ecosystem and new hardware features are continuing to become available. This is particularly true when it comes to MPU (memory protection unit) and MMU (memory management units), in some circumstances the the special interest group will target the lowest common denominator, but accept that this is likely to change in the future. Please see the discussion on MPU and MMU below. 

### Deployed verses Development Platforms

Embedded development typically revolves around cross platform development, development on a PC, and deployment on another device. The development experience is an important aspect affecting tool and target platform adoption. It is therefore important that we ensure we have support for both our Deployed (Target) Platforms and also for our Development Platforms. You will see this called out in the operating system and instruction set architectures below.

## Approach

In order to produce this document and narrow down the platforms selections we will follow the approach outlined below:

1. Select hardware instruction set
2. Define if MMU / MPU support is required
3. Define minimum RAM and storage requirements
4. Select RTOS / Operating Systems which need to be supported on the target hardware as defined in steps 1,2 and 3.
5. Select publicly available platforms which provide the best coverage for the selected hardware requirements.
6. Define the WebAssembly Runtimes that should be considered on the chosen platforms

## 1. Hardware Instruction Set Requirements (ISA)
The set of ISAs the SIG should address are broken down into two groups, a "Development Platform" - the platform a developer uses to create software, and a "Deployed Platform" the platform upon which the final software product will run.

### Deployed Platforms (ISA)

The following hardware instructions sets should be supported by any proposal:

1. Xtensa
2. RISC-V 32-bit + 64-bit
3. ARM 32-bit + 64-bit

### Development Platforms (ISA)

The following hardware instruction sets should be supported for development environments:

1. X86-64 bit

## 2. MMU / MPU Support

It is becoming increasingly difficult to find development boards for purchase which do not have, at least an MPU. However there are a number of platforms currently deployed in production today which the Special Interest Group feels it should address which do not have either an MMU or an MPU. It is noted that addressable size of the deployed devices is likely to reduce over time as the impact of Moore's Law is felt in the embedded space.

### The Compromise, Balancing Available Devices and Moore's Law

As a compromise, the E-SIG will ask that software proposals will be able to, where possible, work on devices without either an MMU or MPU. It is accepted  that this will mean that some features will be unavailable (not possible to implement on devices without MMU or MPUs) or if available run with degraded performance.

## 3. Minimum RAM and Storage Requirements

Software the E-SIG focuses on should be possible to run with the following RAM and Storage requirements: 

**RAM**: 512kb

**Storage**: 1Mb of Non-Volatile storage 



## 4. Required RTOS / Operating System Requirements
The list of operating systems the imbedded SIG should address is broken down into two groups, a "Development Platform" - the platform a developer uses to create software, and a "Deployed Platform" the platform upon which the final software product will run. There are many other groups which address desktop and server operating systems. The Embedded SIG should focus on the operating systems which are needed for the embedded ecosystem which would not be addressed by another other community. These will predominantly be real time operating systems (RTOS). 

### A Discussion on Real Time Linux

While Linux with a RT kernel patch applied is often a Deployment Platform for larger embedded applications, from the WebAssembly runtime point of view, there is little difference between Linux with a real time patch, and Linux without a real time patch. Indeed Linux is a operating system which has a lot of support across the WebAssembly ecosystem.



### Deployment Platforms (Operating Systems)

The following RTOS / Operating Systems should be supported:

1. Zephyr
2. FreeRTOS
3. NuttX

### Development Platforms (Operating Systems)

The following operating systems should be supported as development environments:

1. Linux 
2. Windows



## 5. Publicly Available Hardware Platforms

The following table maps the ISA, memory protection support, RAM and Storage requirements with a reference implementation. This table will also highlight the platforms, or combination of platform requirements, which are not supported, e.g. an x86-64 bit processor without an MMU as this doesn't exist in the market place, or running Linux on a device without an MMU.

*NB: This might be better in an excel / spreadsheet*

| ISA       | MMU / MPU | RAM  | Storage | OS   | Board    |
| --------- | --------- | ---- | ------- | ---- | -------- |
| Xtensa    | None      | ?    | ?       |      |          |
| Xtensa    | MPU       | ?    | ?       |      |          |
| Xtensa    | MMU       | ?    | ?       |      |          |
| RISC-V 32 | None      | ?    | ?       |      |          |
| RISC-V 32 | MPU       | ?    | ?       |      |          |
| RISC-V 32 | MMU       | ?    | ?       |      |          |
| RISC-V 64 | None      | ?    | ?       |      |          |
| RISC-V 64 | MPU       | ?    | ?       |      |          |
| RISC-V 64 | MMU       | ?    | ?       |      |          |
| ARM 32    | None      | ?    | ?       |      |          |
| ARM 32    | MPU       | ?    | ?       |      |          |
| ARM 32    | MMU       | ?    | ?       |      |          |
| ARM 64    | None      | ?    | ?       |      |          |
| ARM 64    | MPU       | ?    | ?       |      |          |
| ARM 64    | MMU       | ?    | ?       |      |          |
| x86-64    | None      | ?    | ?       |      | Excluded |
| x86-64    | MPU       | ?    | ?       |      | Excluded |
| x86-64    | MMU       | ?    | ?       |      |          |

 

## 6. Runtime Support

The following runtimes should be supported:

1. WAMR
2. Wasmtime
3. Wazero