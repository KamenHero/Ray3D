# Ray3D

> A 3D maze renderer built from scratch in C using raycasting — inspired by the legendary **Wolfenstein 3D** engine. A 42 School team project.

---


## 📁 Project Structure

```
Ray3D/
├── gnl/                  # Get Next Line library
├── libft/                # Custom C library
├── xpms/                 # XPM wall textures
├── cub3d.h               # Main header
├── cub3d.c               # Entry point & game loop
├── raycast.c             # Raycasting engine (DDA)
├── draw.c                # Wall & screen rendering
├── mapping.c             # Map loading & validation
├── parsing.c             # .cub file parser
├── checkingpath.c        # Map path/flood-fill validation
├── splitting.c           # String splitting utilities
├── move_p.c              # Player movement & rotation
├── colors.c              # Floor & ceiling color rendering
├── screen.c              # Screen/window initialization
├── errors.c              # Error handling
├── utils.c / utils2.c / utils3.c  # Helper functions
├── map.cub               # Example map file
└── makefile
```

---

## ⚙️ How It Works

Ray3D uses **raycasting** to simulate a 3D perspective from a 2D map, the same technique used in Wolfenstein 3D (1992).

For each vertical slice of the screen, a ray is cast from the player's position in the direction they're facing. When the ray hits a wall, the distance is used to determine how tall to draw that wall slice — closer walls appear taller, creating the illusion of depth.

Key steps:
- Parse a `.cub` map file defining the world layout and textures
- Validate the map (closed walls, valid characters, flood-fill check)
- Cast rays across the player's field of view using DDA (Digital Differential Analysis)
- Calculate wall distances and correct for fisheye distortion
- Render directional XPM textures on walls, and solid colors on floor & ceiling
- Handle player movement and rotation via keyboard input

---

## 🗺️ Map Format

Maps use the `.cub` file format:

```
NO ./xpms/north.xpm
SO ./xpms/south.xpm
WE ./xpms/west.xpm
EA ./xpms/east.xpm

F 220,100,0
C 135,206,235

        1111111
        1000001
        1011101
        1000001
111111111011101
100000000000001
111111111011101
        1000001
        1111111
```

| Symbol | Meaning |
|--------|---------|
| `1` | Wall |
| `0` | Empty floor |
| `N` `S` `E` `W` | Player spawn + facing direction |
| `NO` `SO` `WE` `EA` | XPM texture paths for each wall face |
| `F` / `C` | Floor / Ceiling RGB color |

---

## 🚀 Getting Started

### Prerequisites

- GCC
- Make
- MinilibX for Linux
- X11 development libraries:

```bash
sudo apt-get install libxext-dev libxrandr-dev libx11-dev libbsd-dev libgl1-mesa-dev
```

### Build

```bash
git clone https://github.com/KamenHero/Ray3D.git
cd Ray3D
make
```

### Run

```bash
./cub3D map.cub
```

---

## 🎮 Controls

| Key | Action |
|-----|--------|
| `W` `A` `S` `D` | Move forward / left / backward / right |
| `←` `→` | Rotate camera left / right |
| `ESC` | Exit the program |

---

## 🛠️ Makefile Rules

| Rule | Description |
|------|-------------|
| `make` | Build the project |
| `make clean` | Remove object files |
| `make fclean` | Remove object files and binary |
| `make re` | Full rebuild |

---

## 📚 References

- [Lode's Raycasting Tutorial](https://lodev.org/cgtutor/raycasting.html) — the go-to reference for raycasting in C
- [MinilibX Documentation](https://harm-smits.github.io/42docs/libs/minilibx)
- [Wolfenstein 3D source code](https://github.com/id-Software/wolf3d) — the original inspiration

---
