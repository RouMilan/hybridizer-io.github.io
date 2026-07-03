---
id: what-is-hybridizer
title: What is Hybridizer?
description: Overview of Hybridizer, how it operates, inputs, outputs, and supported platforms.
keywords: [Hybridizer, compiler, MSIL, CUDA, AVX, OMP, .NET]
---

# What is Hybridizer?

The aim of the Hybridizer is to let developers seamlessly use different hardware execution environments to make sure their work is done the fastest way possible. 

It integrates in the compilation toolchain: from an intermediate language, it generates source code for different types of architectures. 

The Hybridizer abstracts the specific SDK and language features of processors, therefore reducing the learning curve to many-core processor programs.

## Hybridizer in Operation

The Hybridizer operates on **intermediate language** — code that has been compiled to be either executed by a virtual machine or compiled to machine code. 

The supported input intermediate languages are:

| Input Language | Description |
|----------------|-------------|
| **MSIL** | Microsoft Intermediate Language — the .NET platform |
| **LLVM-IR** | The intermediate representation of LLVM |

Then, depending on the selected **Flavor** (see [Platforms & Flavors](/platforms/overview)), 
the Hybridizer generates source code with all the necessary annotations and code hints to make use of the 
specific features of each hardware architecture.

Here is an example of all the possibilities of Hybridizer :

![Hybridizer Overview](../images/what-is-hybridizer.png)

From a single version of the source intermediate language, **several platforms can be targeted**.

## Key Concepts

- **Single-source**: Write standard C#; Hybridizer will compile MSIL to high-performance native code.

- **Multiple Available backends**: CUDA kernels, OpenMP+CUDA, and vector backends (AVX/AVX512/NEON/POWER).

- **Performance**: Automatically optimizes code for the underlying hardware, utilizing GPU (SIMT) and CPU (SIMD) capabilities.

- **Connectivity**: Generated code is callable from your .NET host.

## Why Hybridizer?

| Benefit | Description |
|---------|-------------|
| **Speed** | Usage of GPU instead of CPU |
| **Productivity** | No need to manually rewrite kernels in C++/CUDA |
| **Portability** | Keep your .NET code; target multiple hardware |
| **Maintainability** | Fewer language boundaries; debug with powershell info support |
| **Reliability** | Predictable compilation pipeline, explicit attributes and annotations |

## Known Limitations

As of today, the following constructs are **not supported** within the code to be transformed:

- Allocating class instances (heap data)
- `string` type
- Catching and throwing exceptions (only partially supported)
- `lock` regions
- `foreach` (as it uses `try/catch` and heap-related operations)
- Recursion (though similar features may be achieved using interfaces)
- Generic functions (generic types are supported)
- Some combinations of generic types with vectorization (C++ targets such as AVX)

:::note
These limitations only apply to the code that will be transformed to accelerator code. Your host code has no such restrictions.
:::

## Next Steps

- [Architecture Overview](./architecture) — Understand the end-to-end pipeline
- [Quickstart](../quickstart/install) — Get started in minutes
- [Programming Guide](../guide/concepts) — Learn core concepts
