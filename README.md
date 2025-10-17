# 🚀 Full Stack Open CI/CD – Automated Deployment Pipeline

Este proyecto implementa un **pipeline completo de Integración y Despliegue Continuo (CI/CD)** utilizando **GitHub Actions** y **Heroku**, como parte del módulo CI/CD del curso [Full Stack Open](https://fullstackopen.com/).

El objetivo es **automatizar todo el ciclo de vida de la aplicación**, desde la validación del código hasta su despliegue en producción, garantizando calidad, rapidez y fiabilidad en cada cambio.

---

## ⚙️ Características principales

✅ Ejecución de **Linting** para mantener la calidad del código.  
✅ **Build automatizado** con Webpack.  
✅ **Pruebas unitarias y E2E (Cypress)** ejecutadas en paralelo.  
✅ **Prevención de builds redundantes** con `cancel-workflow-action`.  
✅ **Despliegue automático en Heroku** con rollback si falla el healthcheck.  
✅ **Caching de dependencias npm** para acelerar la ejecución del pipeline.  

---

## 🧠 Estructura del Pipeline (GitHub Actions)

El flujo de CI/CD está definido en [`pipeline.yml`](.github/workflows/pipeline.yml), que organiza el trabajo en varios *jobs* interconectados:

| Job | Descripción | Dependencias |
|-----|--------------|--------------|
| 🟡 **avoid_redundancy** | Cancela ejecuciones anteriores redundantes para evitar builds innecesarias. | Ninguna |
| 🔵 **lint** | Analiza el código con ESLint para asegurar la calidad. | — |
| 🟢 **build** | Genera el build de producción y lo guarda como artefacto. | — |
| 🧪 **test** | Ejecuta las pruebas unitarias con Jest. | `lint`, `build` |
| ⚙️ **e2e** | Ejecuta pruebas end-to-end con Cypress. | `lint`, `build` |
| 🚀 **deploy** | Despliega automáticamente la app en Heroku si todas las pruebas pasan. | `test`, `e2e` |

🧩 Gracias a la configuración con `needs`, algunos jobs se ejecutan **en paralelo**, optimizando el tiempo total del pipeline.

---

## 🧰 Tecnologías utilizadas

- **GitHub Actions** → Automatización del pipeline CI/CD  
- **Heroku** → Despliegue continuo en la nube  
- **Node.js (v20)** → Entorno de ejecución  
- **Webpack** → Empaquetado del frontend  
- **ESLint** → Análisis de código  
- **Jest** → Pruebas unitarias  
- **Cypress** → Pruebas end-to-end  

---

## 💻 Comandos del proyecto

Antes de ejecutar cualquier comando, instala las dependencias:

```bash
npm install
npm start
npm run eslint
npm run build
npm run start-prod

🌍 Despliegue
El proyecto se despliega automáticamente en Heroku mediante el job deploy.
🔗 URL del despliegue:
👉 https://vaquiro-ci-ga-101b6931ab82.herokuapp.com
El pipeline incluye un healthcheck automático, que verifica que la aplicación esté respondiendo correctamente (/health).
Si el chequeo falla, el workflow realiza un rollback al despliegue anterior de forma automática.

🏁 Resultado final
Un pipeline totalmente automatizado que garantiza calidad continua, builds rápidos y despliegues confiables.
Este proyecto demuestra cómo llevar un flujo de CI/CD moderno de principio a fin utilizando herramientas gratuitas y profesionales.“Automatizar no es solo ahorrar tiempo, es asegurar calidad continua.”
