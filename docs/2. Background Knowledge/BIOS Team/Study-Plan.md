#BIOS Team Study Plan

## Week 1 : Foundations
C review and practice
- Focus on embedded-style C (no malloc, bitwise ops)
- Practice with structs, unions, and hardware-style I/O registers

Python review on parsing
- Learn parsing tools: json, xml, argparse
- Practice building CLIs

UEFI overview
- Read UEFI specs from UEFI.org

## Week 2 : UEFI Firmware and Tools
Study UEFI Boot flow & shell
- Learn stages (SEC, PEI, DXE, BDS, RT)
- Use OVMF in QEMU to emulate UEFI booting

Experiment with edk2
- Build simple UEFI app in C using edk2

Python parsing tool practice
- Parse UEFI HII database in JSON

## Week 3 : Testing + Debugging
Firmware debugging
- Learn how to use logs, GUIDs, memory maps
- Tools : UEFITool, Chipsec, and debug with serial logs

Basic Python Automation Scripts
- Automate parsing + report generation from HII data

Cross-reference Experiments
- Compare BIOS config changes and result logs

## Week 4 : AI Integration
Deploy local LLM
- Try Ollama or OpenWebUI with small open LLM
- Fine-tune or prompt engineer with mock firmware logs
Develop Proof of Concept Tool
- Chatbot using Python that explains BIOS logs from LLM
