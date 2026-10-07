# Workshop de Observabilidad y APM con IBM Instana

Workshop práctico y hands-on para la monitorización de rendimiento de aplicaciones empresariales (**APM**), análisis forense de sistemas distribuidos, diagnóstico de infraestructuras cloud-native y automatización de respuesta a incidentes con **IBM Instana**.

🌐 **Sitio Web del Workshop:** [https://ibm-automation-spgi.github.io/instana-workshop/](https://ibm-automation-spgi.github.io/instana-workshop/)

---

## 🎯 Estructura del Workshop

El taller está organizado en 8 módulos progresivos guiados por la interfaz gráfica de IBM Instana sobre aplicaciones reales (*Stan's Robot Shop*, *Keda-Scaler-RobotApp*, *OpenShift*):

- **[Introducción y Arquitectura](docs/index.md):** Fundamentos del Dynamic Graph, 5 diferenciales de Instana y acceso al sandbox.
- **[Lab 0 — Entorno, Consola y Dynamic Focus](docs/lab0/index.md):** Control del Time Picker, filtros universales DFQL y GraphQL API (⏱ 15 min).
- **[Lab 1 — Infrastructure 3D, 1s Metrics & JVMs](docs/lab1/index.md):** Topología 3D, telemetría a 1 segundo, Stack Viewer y diagnóstico de runtimes JVM (⏱ 20 min).
- **[Lab 2 — Application Perspectives & Service Flow](docs/lab2/index.md):** Mapeo de microservicios, señales doradas (RED), endpoints REST y Logs in Context (⏱ 20 min).
- **[Lab 3 — 100% Tracing No-Sampling & Analytics](docs/lab3/index.md):** Trazabilidad distribuida completa, vista Waterfall, payloads SQL y Unbounded Analytics (⏱ 20 min).
- **[Lab 4 — Incidentes, RCA & Change Events](docs/lab4/index.md):** Supresión de tormentas de alertas, correlación con IA, árbol de causa raíz y Release Markers (⏱ 15 min).
- **[Lab 5 — SmartAlerts, SLOs & Custom Dashboards](docs/lab5/index.md):** Alertas con Dynamic Baselines, gestión de SLOs, Error Budgets, Burn Rate y cuadros de mando (⏱ 15 min).
- **[Lab 6 — Kubernetes & OpenShift Observability](docs/lab6/index.md):** Control Plane, Requests vs Limits, CPU Throttling y navegación a trazas (⏱ 15 min).
- **[Lab 7 — OpenTelemetry, SDK & Action Automation](docs/lab7/index.md):** Ingesta OTLP, anotaciones `@Span` con el SDK de Instana y remediación automatizada con Action Framework (⏱ 15 min).

---

## 🚀 Ejecución Local

Para levantar el workshop en tu entorno local:

```bash
# 1. Clonar el repositorio
git clone https://github.com/IBM-Automation-SPGI/instana-workshop.git
cd instana-workshop

# 2. Crear y activar el entorno virtual
python3 -m venv .venv
source .venv/bin/activate

# 3. Instalar dependencias
pip install -r requirements.txt

# 4. Iniciar el servidor local
mkdocs serve
```

El sitio estará disponible en `http://127.0.0.1:8000/`.

---

## 🛠️ Tecnologías y Estándares

- **Generador de Documentación:** [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/)
- **Diseño & Paleta:** IBM Carbon Design System / IBM Plex Sans & Mono
- **Diagramas:** [Mermaid.js](https://mermaid.js.org/)
- **Despliegue Continuo:** GitHub Actions & GitHub Pages
