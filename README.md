# init-lab — Custom Init and Supervision Playground

This repository contains my personal experiments and implementations of minimal init systems, including:

- 🧠 `pidmgr/`: My custom C++ PID manager
- 🪛 `s6/`: Service definitions and supervision scripts
- ⚙️ `runit/`: Exploratory stage-based scripts
- 🧪 `tests/`: Fake boot environments, service stressors

### Design Philosophy
This repository reflects a move away from monolithic service managers like systemd. It draws heavily from:

- Suckless ethos
- Plan 9 process models
- Garuda + BSD init modularity
- Practical supervision via daemontools-style architecture

### Goals
- Fully reproducible init systems
- Stateless bootable profiles
- Self-contained supervision for containers and bare metal
