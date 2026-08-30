# Investigación Forense Digital con IA

**Autor:** Carlos Gallardo
**Contexto:** Proyecto de investigación aplicada - Ingeniería en Inteligencia Artificial

## Resumen Ejecutivo

Esta aplicación web demuestra la integración de técnicas de **Inteligencia Artificial** y **Machine Learning** en procesos de **investigación forense digital**. El sistema permite analizar grandes volúmenes de datos forenses (logs, metadatos, comunicaciones) para identificar patrones de actividad sospechosa, reduciendo el tiempo de análisis en un 60-80%.

## Tecnologías Utilizadas

| Componente | Tecnología |
|------------|------------|
| **Frontend** | Next.js, TypeScript, Tailwind CSS |
| **Backend/API** | Next.js API Routes |
| **Machine Learning** | Python (scikit-learn, pandas) - Backend independiente |
| **Visualización** | Chart.js, Recharts |

## Estructura del Proyecto

investigacion-_informatica_forense--ai/
├── app/ # Next.js App Router
│ ├── page.tsx # Dashboard principal
│ └── api/ # Endpoints para análisis
├── public/ # Assets estáticos
└── ...

## Funcionalidades Clave

- **Carga de datos forenses** (logs, archivos planos, metadata)
- **Análisis de anomalías** mediante Isolation Forest
- **Clasificación de eventos** con XGBoost
- **Procesamiento de lenguaje natural** para análisis de comunicaciones
- **Dashboard interactivo** con visualización de hallazgos

## Reporte Técnico Completo

Para el análisis forense detallado, metodología y hallazgos, consultar el [**WRITEUP.md**](WRITEUP.md) en este repositorio.

## Instalación y Ejecución

```bash
npm install
npm run dev

Abrir http://localhost:3000

Enlaces Relacionados
Repositorio de Análisis de Malware: https://github.com/it-prof-Carlos/Malware-Analysis-Trojan-Dropper

Repositorio de Detección de Fraudes: https://github.com/it-prof-Carlos/financial_fraud_detector

Perfil de LinkedIn: www.linkedin.com/in/carlos-gallardo-746059194


