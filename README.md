# The ESCAPE — The JAMS

> **When reality collapses, would you risk everything for a world whose rules you do not understand?**

## Project

**The ESCAPE** is an interactive digital-world experience built around three stages:

**First World → Portal / Transition → After World**

The project uses **OpenUSD and NVIDIA Omniverse** as the shared world-composition pipeline while allowing different team members and tools to contribute independently.

Our current workflow explores:

- OpenUSD composition and references
- NVIDIA Omniverse / USD Composer
- PhysX collision and interaction
- Action Graph / runtime world switching
- Python
- TouchDesigner
- GLSL shaders

---

## Team Ownership

| Team Member | Main File / Area | Responsibility |
| --- | --- | --- |
| Jiayue | `layers/firstworld_jiayue.usda` | First World / city |
| Si | `layers/portal_si.usda` + `touchdesigner/` | Portal, TouchDesigner, shaders, portal integration |
| Avita | `layers/afterworld_avita.usda` | After World |
| Avi | `layers/integration_avi.usda` | Player, interaction, transitions, world-switch testing and integration |

### Important rule

**Each team member edits only their own USD layer.**

Do not directly edit another member's `.usda` file unless the team agrees first.

`main.usda` is the shared composition stage and should be changed carefully during integration.

---

## Repository Structure

```text
The-JAMS/
│
├── main.usda
│
├── layers/
│   ├── firstworld_jiayue.usda
│   ├── portal_si.usda
│   ├── afterworld_avita.usda
│   └── integration_avi.usda
│
├── touchdesigner/
│   ├── project/
│   ├── shaders/
│   └── exports/
│
├── assets/
├── data/
├── scripts/
│
├── docs/
│   ├── progress/
│   ├── screenshots/
│   └── diagrams/
│
├── .gitattributes
├── .gitignore
└── README.md
```

---

## What Goes Where?

### `main.usda`

The master OpenUSD composition.

It brings the team's separately authored content together into the final experience.

Conceptually:

```text
main.usda
│
├── First World
│   └── firstworld_jiayue.usda
│
├── Portal
│   └── portal_si.usda
│
├── After World
│   └── afterworld_avita.usda
│
└── Integration
    └── integration_avi.usda
```

Do not use `main.usda` as your personal working file.

---

### `layers/`

Contains each team member's OpenUSD authoring file.

Each person should primarily work in their own layer.

---

### `touchdesigner/`

TouchDesigner source and output files.

- `project/` — TouchDesigner `.toe` project files
- `shaders/` — GLSL and related shader source
- `exports/` — exported portal visuals, textures, videos, or other output used by the experience

---

### `assets/`

Shared project assets such as:

- 3D models
- textures
- materials
- images
- audio
- video
- environment assets

Large binary assets are handled through **Git LFS** according to `.gitattributes`.

---

### `scripts/`

Python or other scripts used by the final experience, including portal, interaction, world-switch, or utility logic.

---

### `data/`

CSV, JSON, datasets, or other structured data used by the project.

---

### `docs/`

Project documentation and progress evidence.

- `progress/` — weekly progress material
- `screenshots/` — screenshots and testing evidence
- `diagrams/` — pipeline, OpenUSD, interaction, or system diagrams

---

## Current Interaction Prototype

Our Omniverse tests have demonstrated the following workflow:

```text
World 1
   ↓
Portal / Trigger Event
   ↓
PhysX + Action Graph
   ↓
World 1 visibility → invisible
World 2 visibility → inherited
   ↓
World 2
```

We also tested:

- PhysX colliders
- Rigid bodies and gravity
- Character Controller navigation
- WASD movement
- Environment collision
- Trigger volumes
- Action Graph events
- OpenUSD references
- Runtime switching between separately authored USD worlds

The next integration challenge is connecting the **player and TouchDesigner portal experience** to the world-transition system reliably.

---

## Git Workflow

### Before starting work

Always pull the newest version:

```bash
git pull
```

### Work

Edit **your own files only** whenever possible.

Save and test your work before committing.

### Check your changes

```bash
git status
```

### Stage only your work

Example:

```bash
git add layers/integration_avi.usda
```

Do not automatically use `git add .` without checking what changed.

### Commit

Use a short, descriptive message:

```bash
git commit -m "Test portal world transition"
```

### Update before pushing

```bash
git pull --rebase
```

Resolve any conflicts before continuing.

### Push

```bash
git push
```

---

## Collaboration Rules

1. **Pull before starting work.**
2. **Edit your own USD layer.**
3. Do not overwrite another person's layer.
4. Do not use `main.usda` as a personal workspace.
5. Keep files inside the correct repository folders.
6. Check `git status` before every commit.
7. Use clear commit messages.
8. Push finished working changes so teammates can pull them.
9. Large assets must follow the project's Git LFS configuration.
10. Tell the team before making structural changes to `main.usda`.

---

## Core Pipeline

```text
DESIGN / CONTENT TOOLS
        ↓
      OpenUSD
        ↓
NVIDIA OMNIVERSE
        ↓
COMPOSITION + INTERACTION
        ↓
THE ESCAPE
```

Different tools can create different parts of the experience, while OpenUSD provides the shared structure used to compose the final digital world.
