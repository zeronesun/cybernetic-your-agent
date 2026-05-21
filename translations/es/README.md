[English](../en/README.md) | [简体中文](../../README.md) | [繁體中文](../zh_TW/README.md) | [日本語](../ja/README.md) | [한국어](../ko/README.md) | [Русский](../ru/README.md) | [Deutsch](../de/README.md) | Español

# Entrenar Agentes de IA con la Cibernética de Ingeniería de Qian Xuesen

> No enseñes a la IA nuevos conocimientos. Usa **control predictivo, control integral, descomposición jerárquica y autocontrol** — cuatro conceptos — para reestructurar la arquitectura de memoria y habilidades del agente, transformándolo de una herramienta pasiva en un motor de colaboración autocorrectivo y evolutivo.

---

## Qué Es Esto

Un tutorial completo, reproducible y práctico.

Adapta las ideas fundamentales de la *Cibernética de Ingeniería* de Qian Xuesen para plataformas modernas de agentes de IA (Hermes, Claude con MCP, GPT personalizados, etc.). Sin añadir entradas de prompt ni introducir nuevos modelos, utiliza **reestructuración arquitectónica** para hacer que el agente:

- 🎯 **Control predictivo para evitar obstáculos** — carga proactivamente tus preferencias y lecciones históricas antes de que comience una tarea
- 🔧 **Control integral para prevenir oscilación** — una queja única sólo consigue una corrección temporal; el mismo feedback dos veces desencadena un cambio sistemático
- 🧹 **Separación jerárquica** — la memoria almacena sólo el "por qué"; las habilidades almacenan sólo el "cómo"; nunca mezclados
- 🚦 **Puerta de entrega con autocontrol** — una puerta de calidad de cinco verificaciones se ejecuta antes de cualquier salida; los resultados no calificados nunca se entregan
- 🔄 **Evolución de ciclo cerrado** — di "despegar" una vez a la semana y el agente se revisa y optimiza automáticamente

---

## Inicio Rápido

Envía este comando a tu agente, y completará automáticamente el entrenamiento completo (≈ 40 minutos):

```
按 github.com/zeronesun/cybernetic-your-agent 的 scripts/deployment-commands.md 训练我。每步确认，完成后闭环测试。
```

**Requisitos**: Tu agente debe poder acceder a GitHub, escribir en memoria y crear habilidades. Si no se cumplen, sigue los pasos manuales a continuación.

1. Asegúrate de que tu plataforma de agentes tenga: **memoria persistente** + **habilidades / módulos procedimentales**
2. Lee el tutorial (se recomienda en orden, o al menos lee el Capítulo 1 para entender el enfoque)
3. Ve al [Capítulo 5](chapters/05-deployment.md), copia y pega las instrucciones e implementa paso a paso (≈ 1 hora)
4. El [Capítulo 6](chapters/06-daily-usage.md) te dice cómo usarlo diariamente y cómo verificar que está funcionando

---

## Estructura del Tutorial

| Capítulo | Archivo | Resumen de una frase |
| :------- | :----------------------------------------------------------- | :--------------------------------------------------- |
| Prólogo  | [`PREFACE.md`](PREFACE.md) | Por qué la IA aprende todos los conocimientos pero aún no te "entiende" |
| Capítulo 1 | [`chapters/01-background.md`](chapters/01-background.md) | Antecedentes y filosofía central |
| Capítulo 2 | [`chapters/02-prerequisites.md`](chapters/02-prerequisites.md) | Prerrequisitos y preparación |
| Capítulo 3 | [`chapters/03-core-theory.md`](chapters/03-core-theory.md) | Cuatro conceptos de cibernética en detalle (control predictivo / integral / separación / autocontrol) |
| Capítulo 4 | [`chapters/04-architecture.md`](chapters/04-architecture.md) | Arquitectura del sistema en detalle (memoria de tres niveles + capa de habilidades + flujo de datos) |
| Capítulo 5 | [`chapters/05-deployment.md`](chapters/05-deployment.md) | Guía práctica (instrucciones de implementación paso a paso que puedes copiar directamente) |
| Capítulo 6 | [`chapters/06-daily-usage.md`](chapters/06-daily-usage.md) | Uso diario y verificación |
| Capítulo 7 | [`chapters/07-faq-extensions.md`](chapters/07-faq-extensions.md) | Solución de problemas + extensiones multi-agente / nueva teoría |
| Epílogo | [`EPILOGUE.md`](EPILOGUE.md) | Después de la implementación: significado y direcciones futuras |

### Nota sobre Nombres de Archivos

El directorio raíz y los nombres de archivos de capítulos utilizan inglés para la compatibilidad entre plataformas y herramientas. Mapeo de nombres de archivos de origen chino a nombres de GitHub:

| Nombre de archivo local (chino) | Nombre de archivo en GitHub |
| :---------------------------------- | :---------------------------- |
| 序章：为什么 AI…md | `PREFACE.md` |
| 第一章：背景与核心理念.md | `chapters/01-background.md` |
| 第二章：适用条件与准备工作.md | `chapters/02-prerequisites.md` |
| 第三章：核心理论详解.md | `chapters/03-core-theory.md` |
| 第四章：系统架构详解.md | `chapters/04-architecture.md` |
| 第五章：实操指南.md | `chapters/05-deployment.md` |
| 第六章：日常使用与验证.md | `chapters/06-daily-usage.md` |
| 第七章：常见问题与延伸思考.md | `chapters/07-faq-extensions.md` |
| 结尾：架构之后.md | `EPILOGUE.md` |

Los encabezados y el texto dentro de los archivos permanecen en chino. El directorio `translations/` está reservado para traducciones a otros idiomas (por ejemplo, `en/`, `ja/`).

### Archivos Complementarios

| Archivo | Descripción |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [`scripts/deployment-commands.md`](scripts/deployment-commands.md) | Extracción pura de todos los comandos del Capítulo 5 (sin explicaciones, para ejecución rápida) |
| [`examples/`](examples/) | Ejemplo L2/L3, ejemplo de tabla de control integral, ejemplo de salida de revisión profunda |
| [`CONTRIBUTING.md`](CONTRIBUTING.md) | Guía de contribución |
| [`LICENSE`](LICENSE) | Licencia de código abierto |

---

## Plataformas Soportadas

- ✅ **Hermes 3** (soporte nativo completo, todas las instrucciones funcionan perfectamente)
- ✅ **Claude (con MCP)** (ajustes menores de sintaxis para llamadas a herramientas; arquitectura central totalmente aplicable)
- ✅ **GPT Personalizados** (usa archivos de Conocimiento para simular memoria, Acciones para simular habilidades)
- 🔸 Otras plataformas de agentes con **memoria persistente + habilidades / módulos procedimentales**
- 🔸 Plataformas sin función de Habilidades (pueden ejecutarse en modo degradado, ver [Capítulo 7 §7.1](chapters/07-faq-extensions.md))

---

## En Resumen: Antes y Después

| Dimensión | Antes | Después |
| :--------------- | :----------------------------------------- | :------------------------------------------- |
| Inicio de tarea | Plantas la necesidad; el agente comienza directamente | El agente genera primero una lista de verificación de obstáculos y evaluación de riesgos; tú confirmas |
| Errores recurrentes | Corriges cada vez; el mismo error vuelve a ocurrir | Se hunde automáticamente en regras después de la segunda ocurrencia; no sucederá una tercera vez |
| Relación señal/ruido de memoria | Principios, pasos, ejemplos todo mezclado | Separación de tres niveles; principios y pasos cada uno tiene su propio lugar |
| Calidad de salida | Inspeccionas, encuentras clichés / problemas de formato, luego pides correcciones | El agente ejecuta su propia puerta de calidad de cinco verificaciones; no entrega hasta que pase |
| Evolución del sistema | Ocasionalmente ajustado basado en intuición | Di "despegar" semanalmente; revisión automática y auto-optimización |

---

## Filosofía Central

> **Lo que estás haciendo no es ingeniería de prompting. Es ingeniería de arquitectura.**
>
> No estás enseñando al agente nuevos conocimientos. Estás utilizando el pensamiento de ingeniería de sistemas para diseñar una arquitectura interna que funcione de manera estable y evolucione continuamente.

Para más antecedentes y elaboración, consulta el [Prólogo](PREFACE.md) y el [Capítulo 1](chapters/01-background.md).

---

## Nombre del Proyecto

**Cybernetic Your Agent** — inyectando genes cibernéticos en tu agente.

No enseñamos a la IA nuevos conocimientos. Utilizamos los cuatro conceptos de la Cibernética de Ingeniería de Qian Xuesen — control predictivo, control integral, descomposición jerárquica y autocontrol — para reestructurar la arquitectura de memoria y habilidades del agente. El agente pasa de entender comandos a entender *tu lógica de juicio* — convirtiéndose verdaderamente en *tu* agente.

---

## Licencia

Este proyecto está licenciado bajo la [Licencia MIT](LICENSE).

---

## Agradecimientos

- La *Cibernética de Ingeniería* de Qian Xuesen — la base teórica de este tutorial

- Todos los que ayudaron a probar y mejorar la arquitectura en sus primeras versiones

## Historial de Estrellas

<a href="https://www.star-history.com/?repos=zeronesun%2Fcybernetic-your-agent&type=date&legend=bottom-right">
 <picture>
   <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/chart?repos=zeronesun/cybernetic-your-agent&type=date&theme=dark&&legend=bottom-right" />
   <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/chart?repos=zeronesun/cybernetic-your-agent&type=date&legend=bottom-right" />
   <img alt="Gráfico de Historial de Estrellas" src="https://api.star-history.com/chart?repos=zeronesun/cybernetic-your-agent&type=date&legend=bottom-right" />
 </picture>
</a>
