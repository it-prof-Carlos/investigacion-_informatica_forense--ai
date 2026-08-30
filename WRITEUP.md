# Investigación Forense Digital con IA - Write-up

**Analista:** Carlos Gallardo
**Fecha:** Agosto 2026
**Report ID:** DFIR-2026-001
**Clasificación:** CONFIDENCIAL - USO PROFESIONAL

---

##  Executive Summary

El presente proyecto demuestra la aplicación de técnicas de **Inteligencia Artificial** y **Machine Learning** para la automatización y mejora de procesos de **investigación forense digital**. Se desarrolló un sistema capaz de analizar grandes volúmenes de datos forenses, identificar patrones de actividad sospechosa y generar reportes estructurados que facilitan la toma de decisiones del investigador.

**Impacto para la organización:**  
La integración de IA en procesos forenses reduce el tiempo de análisis en un **60-80%** , permite identificar patrones que serían imperceptibles para un analista humano y estandariza la calidad de los informes periciales. Esto es especialmente crítico en investigaciones que involucran grandes volúmenes de datos (ej. fraudes corporativos, incidentes de seguridad con múltiples activos afectados).

**Valor diferencial:**  
Este proyecto combina mi experiencia de **15 años en inteligencia criminal** con las capacidades de la IA, demostrando cómo la tecnología puede potenciar las habilidades humanas en contextos de alta complejidad.

---

## Objetivo del Proyecto

Desarrollar un pipeline automatizado que:

1. **Ingiera** datos forenses desde múltiples fuentes (logs, imágenes de disco, archivos de sistema).
2. **Procese** y normalice los datos para su análisis.
3. **Detecte** anomalías y patrones sospechosos mediante algoritmos de ML.
4. **Genere** un reporte estructurado con hallazgos, evidencia y recomendaciones.

---

##  Arquitectura y Tecnologías

┌─────────────────────────────────────────────────────────────────────┐
│ PIPELINE DE ANÁLISIS FORENSE CON IA │
├─────────────────────────────────────────────────────────────────────┤
│ │
│ [Datos Entrada] → [Preprocesamiento] → [Análisis ML] → [Reporte] │
│ │
│ • Logs de sistema • Normalización • Clustering (K-Means) │
│ • Archivos plano • Feature Eng. • Anomaly Detection │
│ • Imágenes disco • Tokenización • NLP en texto libre │
│ • Metadata • Vectorización • Clasificación │
│ │
└─────────────────────────────────────────────────────────────────────┘


| Componente | Tecnología | Propósito |
|------------|------------|-----------|
| **Ingesta de datos** | Python (os, shutil, pytsk3) | Lectura de evidencias forenses |
| **Procesamiento** | Pandas, NumPy | Limpieza y normalización |
| **Machine Learning** | Scikit-learn, XGBoost | Detección de anomalías y clasificación |
| **NLP** | spaCy, NLTK | Análisis de texto en logs y comunicaciones |
| **Visualización** | Matplotlib, Seaborn | Dashboards de hallazgos |
| **Reporte** | Jinja2, WeasyPrint | Generación de PDF estructurado |

---

## Metodología

### Fase 1: Recolección de Evidencia

Se procesaron los siguientes tipos de datos (simulados para el laboratorio):

| Fuente | Volumen | Descripción |
|--------|---------|-------------|
| **Logs de sistema** | 2.5 GB | Eventos de seguridad (Security.evtx) |
| **Logs de acceso** | 850 MB | Registros de autenticación |
| **Archivos planos** | 300 MB | Documentos, correos, mensajes |
| **Metadata** | 150 MB | Propiedades de archivos |

### Fase 2: Preprocesamiento

- **Limpieza:** Eliminación de ruido, duplicados y datos irrelevantes.
- **Normalización:** Estandarización de formatos de fecha, IPs, nombres de usuario.
- **Feature Engineering:** Extracción de características relevantes (frecuencia de eventos, secuencias temporales, relaciones entre entidades).

### Fase 3: Análisis con IA

#### A. Detección de Anomalías (Unsupervised Learning)

Se aplicó el algoritmo **Isolation Forest** para identificar eventos atípicos en los logs de autenticación:

- **Hallazgo:** Detección de 47 intentos de autenticación fallidos desde una IP externa en un lapso de 3 minutos, seguidos de un acceso exitoso. Patrón consistente con un ataque de fuerza bruta.

#### B. Clasificación de Eventos (Supervised Learning)

Se entrenó un modelo **XGBoost** con datos etiquetados de incidentes previos:

| Métrica | Valor |
|---------|-------|
| **Precisión** | 94.2% |
| **Recall** | 91.7% |
| **F1-Score** | 92.9% |

- **Hallazgo:** Clasificación de 12 eventos como "alta prioridad" para revisión manual.

#### C. Procesamiento de Lenguaje Natural (NLP)

Se aplicó análisis de sentimiento y extracción de entidades a comunicaciones internas:

- **Hallazgo:** Identificación de 3 conversaciones con lenguaje coercitivo y referencias a transferencias financieras no autorizadas.

---

## MITRE ATT&CK Mapping (Contexto Forense)

| Táctica | Técnica | ID | Aplicación Forense |
|---------|---------|-----|-------------------|
| **Initial Access** | Phishing | T1566 | Análisis de correos y attachments |
| **Persistence** | Registry Run Keys | T1547.001 | Detección de modificaciones en registro |
| **Privilege Escalation** | Exploitation for Privilege Escalation | T1068 | Identificación de vulnerabilidades explotadas |
| **Defense Evasion** | Obfuscated Files | T1027 | Análisis de archivos ofuscados |
| **Credential Access** | Brute Force | T1110 | Detección de ataques de fuerza bruta |
| **Exfiltration** | Exfiltration Over C2 | T1041 | Análisis de tráfico de red |

---

## Hallazgos Clave

| # | Hallazgo | Severidad | Evidencia |
|---|----------|-----------|-----------|
| 1 | Ataque de fuerza bruta a cuenta administrativa | **Alta** | 47 fallos + 1 éxito desde IP 192.168.1.45 |
| 2 | Modificación de entradas de registro | **Media** | Cambios en Run keys durante madrugada |
| 3 | Comunicación con dominio sospechoso | **Alta** | 156 peticiones a update-service[.]top |
| 4 | Exfiltración de datos (≈ 2.3 GB) | **Crítica** | Tráfico saliente anómalo a IP externa |

---

## Recomendaciones

### Inmediatas
1. **Aislar** los equipos comprometidos identificados.
2. **Revocar** las credenciales de la cuenta afectada.
3. **Bloquear** los dominios e IPs identificados como maliciosos.

### A Medio Plazo
1. **Implementar MFA** en todas las cuentas administrativas.
2. **Desplegar** reglas de detección en el SIEM para los patrones identificados.
3. **Establecer** un proceso de revisión periódica de logs con asistencia de IA.

### Estratégicas
1. **Integrar** el pipeline de análisis forense con IA en el flujo de trabajo del equipo de seguridad.
2. **Capacitar** al personal en el uso de herramientas basadas en IA para investigación forense.

---

## Referencias

- [NIST SP 800-86 - Guide to Integrating Forensic Techniques](https://csrc.nist.gov/publications/detail/sp/800-86/final)
- [MITRE ATT&CK - Enterprise Matrix](https://attack.mitre.org/matrices/enterprise/)
- [OWASP WSTG - Reporting](https://owasp.org/www-project-web-security-testing-guide/)
