# MedFlow - Qingnang Smart Diagnosis System

## Project Overview

**Project Name**: MedFlow (Qingnang Smart Diagnosis)
**Type**: End-to-End AI Healthcare Framework
**Classification**: Medical Device Software - Clinical Decision Support System
**Deployment Status**: Field-deployed in multiple top-tier hospitals across China
**License**: Apache 2.0

## System Description

Qingnang Smart Diagnosis is an end-to-end AI healthcare framework with field-proven application capabilities, designed to provide efficient and intelligent solutions for the medical industry. By integrating advanced large language model (LLM) technologies, this framework has realized core functions including intelligent triage, patient registration, medical record creation, diagnosis, ordering lab tests, prescriptions, and treatment plan development.

**Mission**: Enhance healthcare efficiency, improve patient experiences, and drive intelligent transformation in the medical industry.

## Core Features

### Integration Capabilities
- **End-to-End Interface**: Supports HTTP service interfaces for pre-consultation, in-consultation, and post-consultation processes
- **Flexible Data Integration**: Enables customization of user-specific databases (drugs, disease names) with LLM + retrieval enhancement
- **High-Compatibility Deployment**: Direct access to various models via OpenAI services
- **Multi-Model Support**: Compatible with DeepSeek, Qwen, Llama, Baichuan, and other leading LLMs

### Deployment Flexibility
- **Multi-Scenario Adaptability**: Hospitals, telemedicine, pharmaceutical distribution
- **Multi-Role Support**: Medical staff, patients, administrators
- **Deployment Options**: Cloud-based or on-premises environments

## Technical Architecture

### AI/ML Models

#### Fine-Tuned Medical Models
| Model | Foundational Model | Purpose | Download |
|-------|-------------------|---------|----------|
| Qingnang-72B | Qwen2.5-72B-Instruct | Primary medical reasoning | HuggingFace, ModelScope |
| Qingnang-9B | GLM4-9B-Instruct | Lightweight medical tasks | HuggingFace, ModelScope |
| Qingnang-ASR | Whisper V3 | Chinese/Cantonese speech recognition | HuggingFace, ModelScope |
| Qingnang-TTS | GPT-Sovits2 | Text-to-speech for patient interaction | HuggingFace, ModelScope |

#### Compatible LLMs
- Deepseek v3, Deepseek R1 (reasoning-capable)
- Qwen2.5, Llama 3.1
- Baichuan4, QwQ

### Technical Stack

**Runtime Environment**:
- Ubuntu 20.04
- Python 3.12
- NVIDIA CUDA 12.2
- NVIDIA Driver 535.154.05

**Key Dependencies** (from requirements.txt):
- FastAPI 0.111.1 - API service framework
- Gradio 5.15.0 - Web UI interface
- Pydantic 2.8.2 - Data validation
- fastbm25 0.0.2 - Retrieval/ranking
- gradio-client 1.7.0 - Client interface

**Infrastructure**:
- Docker containers (NVIDIA CUDA base)
- OpenAI-compatible API gateway
- Custom knowledge base system
- Quality inspection engine

## Functional Modules

### Two Core Capabilities

1. **Dialogue Interaction System**
   - Natural AI-driven patient-doctor conversations
   - Patient registration, triage, follow-up care
   - Medical record generation and quality checks
   - Over 95% accuracy in critical workflows

2. **Clinical Reasoning Engine**
   - Diagnosis recommendations
   - Medication suggestions
   - Laboratory test ordering
   - Treatment plan development

### Complete Feature Matrix

| Function | Process Stage | Type | Target Users | Accuracy |
|----------|---------------|------|--------------|----------|
| Patient Registration | Pre-consultation | Dialogue Interaction | Patients, Hospitals | - |
| Intelligent Appointment | Pre-consultation | Dialogue Interaction | Patients, Hospitals | - |
| Symptom Pre-Consultation | Pre-consultation | Dialogue Interaction | Patients, Physicians | - |
| Department Recommendation | Pre-consultation | Dialogue Interaction | Patients, Hospitals | - |
| Medical Record QC | In-consultation | Dialogue + Clinical | Physicians, Hospitals | >95% |
| Medical Record Generation | In-consultation | Dialogue Interaction | Physicians | - |
| Specialist Record Gen. | In-consultation | Dialogue + Clinical | Physicians | - |
| Disease Diagnosis | In-consultation | Clinical Inference | Physicians | >95% |
| Medication Recommendations | In-consultation | Clinical Inference | Physicians | >95% |
| Medical Test Ordering | In-consultation | Clinical Inference | Physicians | >95% |
| Prescription Generation | In-consultation | Dialogue + Clinical | Physicians | - |
| Treatment Plan Development | In-consultation | Dialogue + Clinical | Physicians | - |
| Follow-up Management | Post-consultation | Dialogue Interaction | Patients, Hospitals | - |

## Technical Advantages

### Agent Capabilities
- **Optimized Prompt Engineering**: Meticulously crafted prompt instructions
- **Reasoning Workflow Orchestration**: Advanced multi-step reasoning chains
- **Intent Recognition**: LLM-based intent classification with fallback mechanisms

### Key Challenge Solutions
- Intent recognition with SQL distribution interfaces
- Multi-channel retrieval (knowledge base + database)
- Format parsing for reasoning models (DeepSeek R1, QwQ)

### Developer Experience
- **Lightweight Technical Examples**: Intent, retrieval, database implementations
- **Ready-to-Use**: Pre-configured with fine-tuned medical models
- **Demo Interface**: Visual business trial (user-friendly for non-technical personnel)
- **Easy Secondary Development**: Application tips for customization and upgrades

## Security & Compliance

### Data Processing
- Custom knowledge base import (diagnoses, medicines, examination forms)
- Quality inspection rules customization (quality/quality.json)
- Database location: `../data/processed/database`

### Usage Restrictions
- **Apache 2.0 License**: Commercial use permitted without authorization
- **Prohibited Uses**:
  - Any purpose harmful to country and society
  - Services without security assessments and filings
- **Liability Disclaimer**: Users assume full responsibility for risks related to data security, model manipulation, misuse, or improper utilization

### Model Limitations
- Cannot guarantee 100% output accuracy (probabilistic nature)
- Susceptible to input instruction biases
- Requires security assessment before deployment

## Service Architecture

### API Service (inference.py)
```bash
python3 inference.py \
  --model <model_name> \
  --model-url http://<openai_ip>:<port>/v1 \
  --fastbm25 \
  --log \
  --host <server_ip> \
  --port <server_port> \
  --max-round 30 \
  --database ../data/processed/database
```

**Key Parameters**:
- `--model`: LLM model identifier
- `--model-url`: OpenAI-compatible service endpoint
- `--fastbm25`: Enable BM25 retrieval ranking
- `--max-round 30`: Maximum conversation turns
- `--database`: Custom knowledge base path

### Web UI Service (inference_gradio.py)
```bash
python3 inference_gradio.py \
  --host <server_ip> \
  --port <server_port> \
  --gradio-port <webui_port> \
  --model <model_name>
```

**Access**: `http://<webui_ip>:<webui_port>`

## Testing & Validation

### Available Test Scripts (tests/)
1. `test-clientinfo.sh` - Patient registration dialogue
2. `test-hospitalguide.sh` - Medical guidance dialogue
3. `test-basicmedicalrecord.sh` - Pre-consultation report
4. `test-register.sh` - Appointment booking
5. `test-diagnosis.sh` - Diagnosis generation
6. `test-examineassay.sh` - Examinations and tests
7. `test-therapyscheme.sh` - Treatment plan
8. `test-returnvisit.sh` - Return visit dialogue
9. `test-doctormedicalrecord.sh` - Medical record generation

### Deployment Documentation
- Model deployment guides (ollama, fastchat, vllm)
- Located in `./docs` directory
- Curl request testing documentation in `./tests`

## Intended Use

### Clinical Environment
- **Primary**: Top-tier hospitals in China
- **Secondary**: Telemedicine platforms
- **Tertiary**: Pharmaceutical distribution systems

### Patient Population
- All patient demographics
- Acute and chronic care settings
- Pre-consultation, in-consultation, post-consultation workflows

### User Roles
1. **Patients**: Registration, triage, follow-up management
2. **Physicians**: Diagnosis, prescriptions, treatment planning
3. **Medical Staff**: Record generation, quality checks
4. **Administrators**: System management, workflow optimization
5. **Hospitals**: Integration with HIS (Hospital Information System)

## Integration & Customization

### HIS Integration
- Partner: Skytek (https://www.skytek.com.cn)
- Private hospital deployments available
- HIS-related customization support

### Data Processing
- Medical domain data processing via EPAI platform
- Routine training and enhancement training support
- Custom knowledge base creation (`create_database.py`)

### Quality Control
- Customizable quality inspection rules
- Configuration: `quality/quality.json`
- Real-time medical record QC with >95% accuracy

## Repository Information

**Repository**: https://github.com/MedFlow2025/medflow
**Branch**: develop
**Issues**: Submit via GitHub Issues page
**Support**: Active community and vendor support

## Development Roadmap

### Current Status
- ✅ Field-deployed in multiple top-tier hospitals
- ✅ 95%+ accuracy in critical clinical workflows
- ✅ Multi-model compatibility (DeepSeek, Qwen, Llama, Baichuan)
- ✅ Complete pre/in/post-consultation workflow coverage

### Contact & Support
- **Technical Issues**: GitHub Issues
- **Data Processing**: EPAI Platform (Enhanced Platform for AI Innovation)
- **Hospital Deployments**: Skytek partner referrals
- **Community**: Active participation and support welcome

## Vision

To drive transformative changes in healthcare through large model inference deployments, delivering superior services to patients and medical staff.

---

**Last Updated**: 2025-12-03
**Document Version**: 1.0
**Maintained By**: MedFlow Development Team
