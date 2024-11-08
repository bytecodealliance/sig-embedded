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

* Zephyr
* FreeRTOS
* NuttX

#### Game Console Platforms

The XBox (Windows) and PlayStation (FreeBSD) are examples of high end embedded platforms which the E-SIG should target. This is different from targeting a game engine, like Unity, but focusing on targeting system integration. In targeting games consoles the E-SIG would also have a opportunity to consider how high speed access can be given to hardware peripherals like graphics accelerators and storage / decompression accelerators, focusing on data throughput and application latency.

It is noted that access to the Development Kits for XBox and PlayStation can be expensive.

### Development Platforms (Operating Systems)

The following operating systems should be supported as development environments:

1. Linux 
2. Windows

## 5. Publicly Available Hardware Platforms

It is important to provide all stake holders with a quick list of targert development boards and hardware they can purchase and work on. The following table outlines example hardware which most closely matches the requirements detailed above for each major ISA. This is not an exhaustive list, and of course any hardware which meets the requirements detailed above should be suitable. However, this should help those wishing to quickly purchase hardware and get started contributing.

| ISA       | Board / Purchasble Hardware                                                            |
| --------- | -------------------------------------------------------------------------------------- |
| Xtensa    | [ESP32-S3-BOX-3](https://www.espressif.com/en/news/ESP32-S3-BOX-3)                     |
| RISC-V 32 | *N/A - Suggestions welcome*                                                            |
| ARM 32    | [STM32H747AG](https://www.st.com/en/microcontrollers-microprocessors/stm32h747ag.html) |
| RISC-V 64 | [PINE64 Ox64](https://pine64.org/devices/ox64/)                                        |
| ARM 64    | [Raspberry Pi 3](https://www.raspberrypi.com/products/raspberry-pi-3-model-b/)         |
| x86-64    | [Lattepanda-v1](https://www.lattepanda.com/lattepanda-v1)                              |

### Reasoning for target platform provided processor proposal

It was looked at the Arm32/Arm64 processors available

- STM32F0 (Cortex M0) is a contrained device with an 32-bit arm achritecture that has no MPU. It is utilized in various cost sensitive application and shall represent a platform for brownfield support. Remark: The Cortex-mO is mostly replaced by m0+ which includes the MPU capabilities.
- STM32F7 (Cortex-M7) is a constrained device with an 32-bit arm architecture. It is utilized in various performance sensitive application and shall represent a platform for brownfield support utilizing realtime OS.
- STM32U5 (Cortex-M33) is a constrained device with a 32-bit arm architecture. It is designed for low power application and shall represent a platform for greenfield application utilizing realtime OS with an enhanced cybersecurity feature set.
- IMX6ULL (Cortex -A7) is an embedded device with a 32-bit arm architecture. It is designed as an application processor and shall represent a platform for brownfield application utilizing embedded linux. 
- IMX8M (Cortex-A53) is an embedded device with a 64-bit arm architecture. It is designed as an application processor and shall represent a platform for brownfield and greenfield application utilizing embedded linux. 
- IMX8Plus (Cortex-A53) is an embeddedd device with a 64-bit architecture. It is designed as an application processor including a neural network and shall represent a platform for greenfield application if an NPU is needed.

## 6. Runtime Support

The following runtimes should be supported:

1. WAMR
2. Wasmtime
3. Wazero
4. WasmEdge