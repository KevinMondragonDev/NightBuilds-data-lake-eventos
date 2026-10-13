# sideproject-data-lake-eventos

> Data lake dirigido por eventos en AWS local: S3, SQS, Lambda y DynamoDB, con una API que sirve el resumen.

**Estado:** 🚧 sin empezar · **Tipo:** ETL por eventos + API, en Floci · **Módulo del programa:** 06/07 · Nube con Floci

## La problemática

Cada sucursal sube al final del día un CSV de movimientos y finanzas quiere el resumen por cuenta en cuanto llega el archivo, sin esperar a un proceso nocturno. Y sin perder archivos ni contar dos veces el que se sube repetido.

## Los datos

| Dónde | Qué es |
|---|---|
| `datos/` (11 archivos) | Un CSV por sucursal y día (tres sucursales, 1 al 3 de julio de 2026), más un archivo roto y uno repetido |

Los archivos de `datos/` son **sintéticos**, generados para practicar: no corresponden a personas ni a operaciones reales.

## Qué hay que construir

El enunciado completo, con sus hitos y cómo comprobar cada uno, está en [`RETO.md`](RETO.md). No trae solución: el diseño es tuyo.

- [`docs/REGLAS.md`](docs/REGLAS.md): cómo se trabaja un sideproject y qué debe tener este README al terminar.
- [`docs/RUBRICA.md`](docs/RUBRICA.md): con qué criterios se evalúa.

## Cómo se ejecuta

*Pendiente: se escribe al cerrar el primer hito. Los comandos exactos, desde `git clone`.*

## Decisiones

*Pendiente: tres decisiones técnicas y la alternativa que se descartó en cada una.*

## Qué aprendí

*Pendiente.*

---

Reto del programa de Python e ingeniería de datos: [UNIR_Python_Certification](https://github.com/KevinMondragonDev/UNIR_Python_Certification).
