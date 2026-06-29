# HireVerse
<p align="center">
  <img src="https://github.com/user-attachments/assets/112deae5-a9f6-46cd-b127-560955a0517e" width="571" alt="image">
</p>
**Research Paper: [AI-Powered Interview Assessment Platform](https://journals.ekb.eg/article_501902.html)**: AI-DRIVEN MOCK INTERVIEW SIMULATION USING RETRIEVAL-AUGMENTED GENERATION AND MULTIMODAL TRAIT ANALYSIS — Published in the Journal of Al-Azhar University Engineering Sector, this project introduces an AI-driven platform designed to help users practice job interviews and assist companies in conducting initial candidate screenings. The system features an AI avatar that conducts realistic video interviews, analyzes interview performance through speech, facial expressions, and response patterns, and generates comprehensive feedback on behavioral and technical competencies. The platform combines computer vision, speech analysis, and machine learning techniques to provide automated, data-driven interview evaluation.


## Repository Scope

**Note**: This repository contains only the **behavioral assessment component** of the HireVerse project. The complete HireVerse project, including the web application, AI avatar, LangChain integration, and all other components, is available in the main monorepo: [Hireverse-Master](https://github.com/Ali-Aref1/Hireverse-Master)

## Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [Technical Architecture](#technical-architecture)
- [AI Models](#ai-models)
- [Dataset Citation](#dataset-citation)

## Overview

HireVerse serves two primary audiences:

1. **Job Seekers**: Practice interviews with an AI avatar, receive personalized feedback on behavioral and technical performance
2. **Companies**: Automate initial recruitment screening by conducting AI-powered interviews with applicants

The platform analyzes multiple dimensions of candidate performance including engagement, emotional cues, facial expressions, tone, confidence, and provides corrections for both behavioral and technical answers.

## Key Features

### 1. Feature Extraction

The platform extracts three types of features for comprehensive performance analysis using multiprocessing:

**A. Facial Features**
- Extracted per frame using MediaPipe for face landmark detection
- Face alignment and regions of interest (ROI) computation
- Metrics analyzed:
  - Smile intensity (via DeepFace)
  - Eye positioning and alignment
  - Facial landmarks and distances (brow, eye, lip)
  - Head pose angles (via solvePnP)

<img width="400" alt="image" src="https://github.com/user-attachments/assets/9a62e4bc-6baf-4b9d-8e53-dcd60b8278c7"/> <img width="400" alt="image" src="https://github.com/user-attachments/assets/2c8e37ca-9d66-4231-9419-46026e2c6ad4" />

**B. Prosodic Features**
- Extracted from interview audio using Praat, Librosa, and WebRTC VAD
- Per-frame features undergo statistical aggregation (mean, min, max, std) for per-video metrics
- Metrics analyzed:
  - Pitch variations
  - Speech intensity
  - Speaking rate
  - Pause duration and frequency
  - Jitter and shimmer (voice stability)

**C. Lexical Features**
- Analysis of word choice, filler words, and linguistic patterns
- LIWC-based emotional and cognitive content assessment
- Communication clarity and structure evaluation

### 2. AI Avatar

- **Platform**: Unreal Engine 5 with MetaHuman technology
- **Animation**: NeuroSync for real-time facial animation synchronized with speech
- **Streaming**: Pixel Streaming for cloud-based rendering and device-independent access
- **Interaction**: Live Link framework for low-latency animation data streaming

### 3. Technical/Behavioral Questions Evaluation

**LangChain Integration** for structured two-phase evaluation:

**Phase 1: Behavioral Interview**
- Utilizes Retrieval-Augmented Generation (RAG) with structured question database
- Evaluates communication skills, problem-solving abilities, and professional experiences
- Identifies key weaknesses and areas for improvement
- STAR methodology assessment

**Phase 2: Technical Interview**
- Dynamically adjusted based on behavioral interview insights
- Powered by separate RAG-based technical question database
- Assesses coding skills, technical problem-solving, and knowledge gaps
- Live coding evaluation with Google ADK integration
- Adaptive hints and feedback

### 4. Web Application

**Design & Development Stack**:
- **Design**: Figma for UI/UX prototyping
- **Frontend**: React for responsive, component-based interface
- **Backend**: Node.js (primary server), Flask (ML inference), FastAPI (LLM evaluation)
- **Database**: MongoDB for flexible, scalable data storage
- **Real-Time Communication**: WebRTC for video streaming, Socket.io for messaging

## Technical Architecture

### System Components

**Frontend (React)**
- Real-time transcription overlay
- WebRTC video streaming integration
- Interactive code editor interface
- Responsive dashboard design

**Backend Services**

1. **Node.js Server**: Primary backend handling WebRTC, Socket.io messaging, JWT authentication, MongoDB integration
2. **Flask Service**: ML model inference, speech/facial analysis, avatar communication bridge, text-to-speech
3. **FastAPI Service**: Code evaluation using Google ADK, high-performance async handling

**Database (MongoDB)**
- Flexible NoSQL structure for dynamic interview data
- Efficient storage of complex nested structures
- Aggregation pipelines for analytics

**3D Rendering (Unreal Engine 5)**

- MetaHuman avatar rendering
- Pixel Streaming for cloud-based delivery
- Live Link for real-time animation
<img width="700" alt="image" src="https://github.com/user-attachments/assets/149bc93e-f32b-4d64-8d5a-0e363a1b3629" />

## AI Models
<img width="700" height="405" alt="image" src="https://github.com/user-attachments/assets/4cd0c40c-68fe-47de-9087-8918716ad41c" />


### Interview Flow Management
- **LangChain**: LLM orchestration with chain-like workflow structure
- **RAG Pipeline**: CV parsing, embedding, and retrieval using FAISS vector database
- **Primary LLM**: Mistral AI for greeting, behavioral, and technical phases
- **Coding Evaluation**: Google Gemini 2.5 with ADK for code execution

### Behavioral Assessment
- **Models**: Support Vector Regression (SVR) with LASSO feature selection
- **Features**: 108 multimodal attributes (facial, prosodic, lexical)
- **Tools**: MediaPipe FaceMesh, Praat/Parselmouth, Librosa, WebRTC VAD
- **Deployment**: AWS SageMaker
- **Validation**: Monte Carlo cross-validation (1,000 iterations, 80/20 split)

### Emotion Classification
- **Model**: DistilBERT (fine-tuned)
- **Dataset**: Combined CARER and GoEmotions (neutral subset)
- **Classes**: Anger, fear, happiness, sadness, surprise, neutral
- **Loss Function**: Adaptable Focal Loss for class imbalance handling
- **Data Augmentation**: Synonym replacement, random deletion, back-translation (MarianMT)
- **Deployment**: Hugging Face Hub

## Dataset Citation

This project utilizes the MIT Interview Dataset:

```
I. Naim, I. Tanveer, D. Gildea, M. E. Hoque, 
"Automated Analysis and Prediction of Job Interview Performance," 
IEEE Transactions on Affective Computing, 2016.
```

<img src="https://github.com/user-attachments/assets/836201c4-81c4-4283-81a5-7ec33408ac0e" width="500">
