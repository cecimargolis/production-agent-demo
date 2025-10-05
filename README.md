# 🤖 Production Planning Assistant

Asistente conversacional inteligente para la **planificación de producción**, desarrollado con **Dialogflow ES** y un **backend en Python (Google Cloud Run)**.

## 🚀 Descripción general

Este agente permite capturar información clave del proceso productivo a través de diálogo natural y calcular automáticamente el plan de producción óptimo por período.

El chatbot guía al usuario paso a paso, solicitando datos como:

- 📦 Producto a planificar  
- 📅 Unidad de período (día, semana o mes)  
- 🔢 Número de períodos  
- 📈 Demanda esperada por período  
- 🏭 Inventario inicial y capacidad máxima  
- ⏱️ Tiempo por unidad, acumulación y horizonte de lookahead  

Finalmente, genera un **plan de producción detallado**, mostrando:
- Cantidad a producir por período  
- Alertas de capacidad o materiales  
- Inventario final y producción total  

---

## 🧠 Arquitectura

- **Frontend:** Dialogflow Messenger (integrado en esta página)
- **Backend:** Python (Flask/FastAPI) desplegado en Google Cloud Run
- **Integración:** Webhook HTTPS (maneja la lógica del flujo y cálculos)
- **Persistencia temporal:** Contextos de sesión (`plan-session`)  
- **Modelo de conversación:** Multietapa (intents secuenciales)

---

## 🧩 Intents principales

| Intent | Función |
|--------|----------|
| `CaptureProduct` | Captura el nombre del producto |
| `CapturePeriodUnit` | Define si los períodos son días, semanas o meses |
| `CaptureNPeriods` | Indica cuántos períodos se planifican |
| `CaptureDemandLoop` | Captura demanda por período |
| `CaptureFGInventory` | Almacén inicial de producto terminado |
| `CaptureCapacity` | Capacidad máxima por período |
| `CaptureTimePerUnit` | Tiempo requerido por unidad |
| `CaptureAllowAccumulation` | Si se permite acumulación |
| `CaptureLookahead` | Si se usa horizonte de planificación futura |
| `CaptureLookaheadHorizon` | Cuántos períodos mirar hacia adelante |
| `ComputePlan` | Ejecuta el cálculo final del plan de producción |

---

## 🌐 Deploy y uso

1. **Abrir este agente en Dialogflow Console:**  
   [https://dialogflow.cloud.google.com/](https://dialogflow.cloud.google.com/)

2. **Integración web (Dialogflow Messenger):**
   ```html
   <script src="https://www.gstatic.com/dialogflow-console/fast/messenger/bootstrap.js?v=1"></script>
   <df-messenger
     intent="WELCOME"
     chat-title="Production Assistant"
     agent-id="084865e4-8977-4a49-9d05-79e832009949"
     language-code="es">
   </df-messenger>
