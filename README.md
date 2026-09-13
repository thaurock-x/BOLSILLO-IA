# ⚡ BOLSILLO IAs • Local LLM & Edge RAG Engine
[![Deployment Status](https://img.shields.io/badge/Deploy-Vercel-000000?style=for-the-badge&logo=vercel&logoColor=white)](https://bolsillo-ia.vercel.app/)
[![License](https://img.shields.io/badge/License-MIT-green.svg?style=for-the-badge)](LICENSE)
[![WebGPU](https://img.shields.io/badge/WebGPU-Enabled-00ff9d?style=for-the-badge&logo=googlechrome&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/API/WebGPU_API)
[![Privacy](https://img.shields.io/badge/Privacy-100%25%20Offline%20%2F%20Zero--Data-blue?style=for-the-badge)](#-privacidad-y-seguridad)
**BOLSILLO IAs** "Tu IA privada que vive en tu dispositivo" es una plataforma WebApp client-side de última generación que ejecuta un Modelo de Lenguaje de Gran Escala (LLM) de parámetros cuantizados directamente en la **GPU local del navegador** mediante WebGPU. 
Procesamiento local: tus documentos y conversaciones no necesitan enviarse a un servidor para generar respuestas, al eliminar por completo la dependencia de servidores externos y APIs centralizadas, garantiza inferencia con latencia ultra baja, funcionamiento **100% offline después del primer inicio** y privacidad absoluta (*Zero-Knowledge*). Además, incluye un sistema RAG (Retrieval-Augmented Generation) vectorial local para procesamiento y consulta de documentos en tiempo real.
---
## 🌟 Virtudes y Capacidades Principales
- **Inferencia 100% On-Device:** El modelo corre directamente en la aceleración de hardware del usuario (WebGPU). Sin llamadas API, sin latencias de red y sin tarifas por token.
- **RAG Vectorial Client-Side (Vector DB Local):** Sistema de búsqueda semántica local que procesa documentos PDF, archivos TXT e imágenes mediante OCR. Los datos se fragmentan, vectorizan y consultan completamente en memoria local.
- **Operatividad Offline Garantizada:** Una vez descargados e indexados los pesos del modelo en la caché del navegador, la aplicación no requiere conexión a Internet.
- **Agentes Especializados (Personas):** Configuración dinámicas de prompts de sistema enfocados en áreas clave: Matemáticas, Historia, Consejos, Tecnología de Combate, Sistemas Quantum, Economía de Guerra, Energía & Sostenibilidad, IA en Combate y Redes & Ciberespacio.
- **Accesibilidad Multimodal Integrada:**
  - **OCR Local:** Reconocimiento óptico de caracteres para imágenes usando Tesseract.js en español.
  - **Lector de Documentos:** Extracción nativa de texto para PDFs (`PDF.js`) y archivos `.txt`.
  - **Text-To-Speech (TTS):** Sintetizador de voz nativo en español neutro (AR).
---
## 🛠️ Arquitectura Técnica y Stack Tecnológico

| Componente | Tecnología / Librería | Función |
| :--- | :--- | :--- |
| **Aceleración Hardware** | WebGPU API | Aceleración gráfica por hardware directo dentro del navegador |
| **Motor LLM** | `@mlc-ai/web-llm` | Ejecución de inferencia de modelos cuantizados (Phi-3.5-mini-instruct-q4f16_1-MLC) |
| **Embeddings & Vector DB** | `@xenova/transformers` | Pipeline de extracción de características con `Xenova/all-MiniLM-L6-v2` |
| **OCR Local** | `tesseract.js` | Extracción de texto desde imágenes |
| **Procesamiento PDF** | `pdf.js` | Renderizado y extracción de texto página por página |
| **Parseo Markdown** | `marked` | Renderizado de código y formato en tiempo real |

---
## 🧠 Flujo del Sistema RAG Vectorial Local
```mermaid
graph TD
    A[Archivo: PDF / TXT / Imagen OCR] --> B[Extracción de Texto Local]
    B --> C[Chunking: Fragmentos de 400 caracteres]
    C --> D[Embedder: Xenova/all-MiniLM-L6-v2]
    D --> E[Vector Store en Memoria Local]
    F[Consulta del Usuario] --> G[Vector de Consulta]
    G --> H[Cálculo Similitud Coseno vs Embeddings]
    H --> I[Extracción Top-3 Chunks Relevantes]
    I --> J[Prompt Contextual + Phi-3.5 LLM via WebGPU]
    J --> K[Respuesta en Streaming]
