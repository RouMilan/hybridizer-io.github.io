---
id: when-to-use
title: When to Use Hybridizer
description: Use cases, suitability checklist, and limitations to set expectations.
keywords: [use cases, suitability, limitations, GPU, SIMD]
---

Great fit when:

- Using  data-parallel workloads, such as large arrays, linear algebra, image/signal.

- Dealing with hot paths in C# that dominate runtime.

- Needing cross-platform performance without rewriting in CUDA/C++.

Considerations:

- Memory transfer cost GPU↔CPU.

- Algorithm requires a highly parallel structure; frequent control flow splits can slow down processing.

- Complex integration with existing native libraries.

- Known limitations (see [Reference Glossary](/Reference/Glossary) at the bottom of the page).
