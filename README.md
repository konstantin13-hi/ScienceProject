# ScienceProject

# CG/CI/CD Project – Technology Stack

## 📌 Overview
This project focuses on extending traditional CI/CD by introducing **Continuous Generation (CG)** — automatic code generation from design artifacts (e.g., UML models).  

The concept can be described as:  
**CG/CI/CD – Continuous Generation, Integration & Deployment**

---

## 🧩 1. CASE Tools & Modeling

Used as a source of design artifacts for code generation.

### Tools:
- Enterprise Architect
- Visual Paradigm
- StarUML
- Modelio

### Standards:
- UML (Class, Sequence diagrams)
- BPMN
- SysML

---

## ⚙️ 2. Code Generation (Model-Driven Development)

Core part of the system — generating source code from models.

### Tools:
- Acceleo
- Eclipse Modeling Framework (EMF)
- OpenAPI Generator
- Swagger Codegen
- Yeoman

### Techniques:
- Template engines (Mustache, Freemarker)
- Domain Specific Languages (DSL)

---

## 🔄 3. CI/CD Platform

Automates the pipeline.

### Tools:
- Jenkins
- GitLab CI/CD
- GitHub Actions
- TeamCity

### Pipeline stages:
1. Fetch models/artifacts  
2. Generate code  
3. Build application  
4. Run tests  
5. Deploy  

---

## 🗂️ 4. Version Control

### Tools:
- Git

### Platforms:
- GitHub
- GitLab
- Bitbucket

---

## 🐳 5. Containerization & DevOps

### Tools:
- Docker
- Kubernetes
- Docker Compose
- Terraform
- Ansible

---

## 💻 6. Programming Languages

Used for generators, scripts, and application development.

- Java
- Python
- JavaScript (Node.js)
- Groovy (Jenkins pipelines)

---

## 🏗️ 7. Build Tools

- Maven
- Gradle
- npm

---

## 🧪 8. Testing

- JUnit
- Selenium
- Postman

---

## 🧱 9. Example PoC Architecture

1. Create UML model in CASE tool  
2. Export model (XMI / JSON)  
3. Generate code using generator  
4. Push generated code to Git repository  
5. Jenkins pipeline executes:
   - Build  
   - Test  
   - Docker image build  
   - Deployment  

---

## 🚀 Minimal Stack for PoC

- CASE: Enterprise Architect / Visual Paradigm  
- Code Generation: Acceleo / Python templates  
- CI/CD: Jenkins  
- VCS: Git + GitHub/GitLab  
- Containerization: Docker  
- Language: Java or Python  

---

## 🎯 Goal

To build a Proof of Concept (PoC) system that:
- Automatically generates code from design artifacts  
- Integrates generated code into CI/CD pipeline  
- Enables automated build, test, and deployment  

---
