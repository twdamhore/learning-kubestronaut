# Learning Kubestronaut

## Project Goal
Create a comprehensive MCQ study repository for all 5 Kubestronaut certifications (KCNA, KCSA, CKA, CKAD, CKS).

## Current Progress

### KCNA (Kubernetes and Cloud Native Associate)
**Curriculum:** 4 domains, 13 competencies, 2,600 total MCQs planned

| Domain | Competency | Status | Codex Verified |
|--------|------------|--------|----------------|
| 1. Kubernetes Fundamentals (44%) | Kubernetes Core Concepts | ✅ Done (200 MCQs) | ✅ Done |
| | Administration | ✅ Done (200 MCQs) | ✅ Done |
| | Scheduling | ✅ Done (200 MCQs) | ✅ Done |
| | Containerization | ✅ Done (200 MCQs) | ⏳ Pending |
| 2. Container Orchestration (28%) | Networking | ✅ Done (200 MCQs) | ⏳ Pending |
| | Security | ⏳ Pending | - |
| | Troubleshooting | ⏳ Pending | - |
| | Storage | ⏳ Pending | - |
| 3. Cloud Native App Delivery (16%) | Application Delivery | ⏳ Pending | - |
| | Debugging | ⏳ Pending | - |
| 4. Cloud Native Architecture (12%) | Observability | ⏳ Pending | - |
| | Cloud Native Ecosystem and Principles | ⏳ Pending | - |
| | Cloud Native Community and Collaboration | ⏳ Pending | - |

### Other Certifications
- **KCSA:** Not started
- **CKA:** Not started
- **CKAD:** Not started
- **CKS:** Not started

## MCQ Format
- 200 questions per competency
- Difficulty: 10% medium, 70% medium-hard, 20% hard
- Answers hidden with `<details>` collapsible tags
- Organized by topic clusters within each file

## Directory Structure
```
KCNA/
├── 01-kubernetes-fundamentals/
│   ├── 01a-kubernetes-core-concepts.md ✅ (Q1-100)
│   ├── 01b-kubernetes-core-concepts.md ✅ (Q101-200)
│   ├── 02a-administration.md ✅ (Q1-100)
│   ├── 02b-administration.md ✅ (Q101-200)
│   ├── 03a-scheduling.md ✅ (Q1-100)
│   ├── 03b-scheduling.md ✅ (Q101-200)
│   └── 04-containerization.md ✅
├── 02-container-orchestration/
│   ├── 01a-networking.md ✅ (Q1-100)
│   ├── 01b-networking.md ✅ (Q101-200)
│   ├── 02-security.md
│   ├── 03-troubleshooting.md
│   └── 04-storage.md
├── 03-cloud-native-application-delivery/
│   ├── 01-application-delivery.md
│   └── 02-debugging.md
└── 04-cloud-native-architecture/
    ├── 01-observability.md
    ├── 02-cloud-native-ecosystem-and-principles.md
    └── 03-cloud-native-community-and-collaboration.md
```

## Curriculum Source
[Linux Foundation KCNA](https://training.linuxfoundation.org/certification/kubernetes-cloud-native-associate/)

## GitHub Setup for Claude
Fine-grained PAT needed with:
- **Contents:** Read and write
- **Pull requests:** Read and write
- **Metadata:** Read-only (auto-selected)
