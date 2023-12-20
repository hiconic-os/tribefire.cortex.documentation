# Tribefire Introduction

`Tribefire` (TF) is a platform optimized for building data processing applications.

## Core values

It's core paradigm is **modeling**, and it's power and innovation stems from its extremely consequent application. Modeling not just data, but also configuration and APIs, leads to normalization and code reusability across all these areas.

Another important paradigm is **modularity**. Tribefire applications consist of "artifacts" of distinct types (models, APIs, libraries, configuration, ...), which leads to a robust architecture with great reusability of individual components.

Finally, the heart and soul of a TF platform is `cortex` - a database containing TF's own configuration. It is on one hand a reflection of the hardcoded components of the core platform, and on another hand a blueprint for wiring the application on startup. Still, it can be manipulated at runtime, and the configuration can be applied without server restart. `Cortex` thus provides great flexibility when it comes to modifying and extending functionality. Modeled components can be simply added as data at design time or even runtime, and generic functionality can be added, e.g. endpoints like CRUD over REST for all existing persistence components.

## Content of this documentation

This document contains information on core `Tribefire` technology, it's internal architecture, code/artifact structure, build system and development tools. More precisely:

**[Generic Modeling](generic-modeling/gm-overview.md)** explains the core technology behind the modeling paradigm - `GM` - which can be viewed as an extension of a programming language with special support for data types. Note that this technology is usable and useful on its own, without `Tribefire platform`.

**[Build System](build-system/build-system-overview.md)** explains, well, how to build a `GM` and `Tribefire` application.

**[Developer Tools](tools/tools-overview.md)** describes the tools needed to develop `GM` and `Tribefire` applications, namely the `Eclipse` plugins (`DevRock`) and a command line tool called `Jinni`.

**[Tribefire Platform](tribefire-platform/tribefire-platform.md)** explains the application platform built on top of `GM` technology, focusing on its modularity and the magic of `cortex`.

## How to read this documentation

This documentation is aspiring to be short and to the point.

When more details are needed, key parts are **highlighted in bold** for **easier skimming**.

The structure resembles a file system, with `articles` inside `topics`, similar to files in folders. All articles under a topic are intended to be read in the order from top to bottom when considering the order in the left menu.

Articles marked with a `Reference:` **prefix**. These are stand-alone articles which explain something in full detail.

Articles or their parts  marked with an `Extra:` **prefix**. These parts may go deeper and even slightly off topic, explaining additional insights / motivation / terminology origins and similar things **not essential for understanding of given topic**. When trying to learn something quickly, "extra" stuff can be skipped.

