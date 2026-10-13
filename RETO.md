# 🚀 NightBuild — Data lake dirigido por eventos

**Repositorio:** `NightBuilds-data-lake-eventos` · **Tipo:** ETL por eventos + API, en Floci · **Tiempo:** 10–12 h · **Después de:** lecciones 1 a 5 de esta sección

> Reglas, README y lista de cierre: [`NIGHTBUILDS.md`](docs/REGLAS.md). **No hay solución: el diseño es tuyo.**

## El caso

Cada sucursal del banco sube al final del día un CSV de movimientos. Finanzas quiere el resumen por cuenta disponible **en cuanto llega el archivo**, sin esperar a un proceso nocturno. Lo diseñas y lo reproduces completo en tu máquina con Floci.

## Datos

`datos/`: un CSV por sucursal y día (tres sucursales, del 1 al 3 de julio de 2026), más un archivo roto y uno repetido para probar los casos difíciles. Son datos sintéticos.

## Qué practicas

| Lección | Dónde aparece |
|---|---|
| Conceptos de nube | Elegir entre serverless y servidor, responsabilidad compartida |
| Floci y S3 | Buckets raw y clean, claves particionadas |
| Colas y eventos | S3 → SQS, DLQ, SNS |
| Lambda y DynamoDB | El procesamiento y la tabla de consulta |
| Diseño de arquitecturas | Los 6 pasos, antes de escribir código |

## Hitos

**Hito 1 — Diseño en papel.** Pasos 1 a 4 del método: requisitos, diagrama, tabla de decisiones y lista de fallos.
*Comprueba:* cada caja del diagrama tiene una alternativa descartada y un porqué.

**Hito 2 — Infraestructura como código.** `infra.py` crea en Floci todo lo necesario: buckets, colas (con DLQ), tema, tabla y funciones.
*Comprueba:* se ejecuta dos veces seguidas sin fallar; `docker compose down && up` y `infra.py` lo reconstruyen todo.

**Hito 3 — Un archivo, de punta a punta.** Subes un CSV a `raw` → evento → cola → Lambda → Parquet en `clean` y resumen por cuenta en DynamoDB.
*Comprueba:* tras subir el archivo, el resumen aparece sin que ejecutes nada más.

**Hito 4 — Cuando algo sale mal.** Un archivo roto acaba en la DLQ con su motivo. El mismo archivo subido dos veces no duplica el resumen.
*Comprueba:* dos archivos buenos, uno roto y uno repetido: los totales son correctos.

**Hito 5 — Servirlo.** Una API (FastAPI) con `GET /cuentas/{id}/resumen` que lee de DynamoDB.
*Comprueba:* el resumen cambia en la API segundos después de subir otro archivo.

**Hito 6 — Lo que el emulador no dice.** En el README: la política de IAM mínima de cada pieza y una estimación de costo mensual para 200 archivos diarios.
*Comprueba:* cada política nombra acciones y recursos concretos, sin `*`.

## Preguntas para defenderlo

- ¿Por qué hay una cola entre S3 y la Lambda?
- ¿Cómo garantizas que un archivo no se procesa dos veces?
- ¿Qué línea cambiarías para desplegarlo en AWS de verdad? ¿Qué más haría falta?
- Si los archivos pasaran de 5 MB a 5 GB, ¿qué caja ya no sirve y con cuál la sustituyes?

## Súbelo de nivel

- Llévalo a la capa gratuita de AWS con una alerta de facturación y bórralo al terminar.
- Orquesta varios pasos con Step Functions en lugar de una sola Lambda.
- La misma infraestructura con Terraform apuntando a Floci.
