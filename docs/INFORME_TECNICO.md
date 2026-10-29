# UNBUNKER-SECURITY — Informe técnico de arquitectura

**Identificación:** UNBUNKER-SECURITY / SQ-ONE Research Labs  
**Responsable:** Sergio Alberto Albornoz  
**Organización de desarrollo:** Herramet Design  
**Versión documental:** 1.0  
**Fecha:** 29 de octubre de 2026  
**Estado:** prototipo estructural experimental; validación criptográfica independiente pendiente.

## 1. Resumen ejecutivo

UNBUNKER-SECURITY explora una arquitectura de software para representar y comprobar estados, relaciones de reciprocidad, integridad de transiciones y trazabilidad. El concepto se desarrolló alrededor del módulo DiamondUnBunker y tuvo una integración experimental en el entorno GENESIS.

El objetivo de esta etapa es organizar el diseño, hacer explícitos sus supuestos y preparar un proceso de evaluación reproducible. La arquitectura se presenta como investigación y prototipo, no como un producto criptográfico validado ni como una solución lista para proteger infraestructura crítica.

## 2. Objetivos

- Modelar estados de componentes y sus relaciones.
- Detectar divergencias entre estados que deberían mantener reciprocidad.
- Controlar reinicialización y recuperación del estado operativo.
- Registrar versiones, eventos y resultados de pruebas para facilitar la auditoría.
- Preparar un modelo de amenazas y un plan de validación independiente.
- Investigar cómo complementar el modelo estructural con primitivas criptográficas estándar.

## 3. Arquitectura conceptual

La propuesta se organiza en capas funcionales:

1. **Representación:** estructura abstracta de unidades y estados.
2. **Organización estructural:** distribución de las unidades en una secuencia de seis lados.
3. **Motor de validación:** comprobaciones de coherencia y relaciones de reciprocidad.
4. **Control de estados:** tratamiento de errores, reinicialización y recuperación del estado interno.
5. **Integración:** interfaz con el entorno de prueba GENESIS.
6. **Trazabilidad:** identificación de versiones, registro de resultados y documentación de cambios.

Estas capas describen la organización conceptual del sistema. Su alcance exacto debe confirmarse contra el código publicado y pruebas reproducibles.

## 4. Modelo estructural de referencia

La configuración conceptual de referencia es:

- 6 lados.
- 4 posiciones por lado.
- 3 unidades por posición.
- Total: 6 × 4 × 3 = 72 unidades.
- 3 estados teóricos posibles por unidad, según el modelo planteado.

Bajo la hipótesis matemática de que todas las unidades pueden adoptar sus tres estados, el espacio combinatorio ideal sería 3^72 configuraciones. El logaritmo en base 2 de ese espacio es aproximadamente 114,12 bits.

**Interpretación rigurosa:** esta cifra es una cuenta combinatoria teórica, no una medición de entropía criptográfica ni una demostración de seguridad. Para estimar la seguridad efectiva hay que establecer cómo se generan y distribuyen los estados, si son independientes, qué información observa un atacante, cómo se producen las claves, qué sesgos existen y qué ataques son posibles. La estructura por sí sola no permite afirmar una seguridad de 114 bits ni alcanzar un objetivo de 128 bits.

## 5. Comprobaciones preliminares descritas

En el trabajo previo se registraron como áreas de comprobación funcional:

- existencia y organización de las 72 unidades;
- recorrido o secuencia de seis lados;
- detección de fallos de reciprocidad;
- reinicialización del sistema;
- integración experimental con GENESIS.

Este informe conserva estas actividades como comprobaciones preliminares descritas en el historial del proyecto. Para considerarlas evidencia formal, el repositorio deberá incluir casos de prueba, instrucciones de ejecución, resultados observados, versión exacta del código y condiciones del entorno. Este documento no afirma que se haya realizado una auditoría independiente.

## 6. Integración y límites actuales

La integración experimental previa en GENESIS mantenía la configuración de activación criptográfica deshabilitada (cryptoActivated: false) y posesión deshabilitada (possession: false). En esa configuración no queda demostrada una función criptográfica activa ni la protección efectiva de datos.

El módulo debe evaluarse como componente aislado antes de considerarlo parte de un sistema de seguridad. La integración no equivale a una certificación, auditoría ni validación de resistencia a ataques.

## 7. Modelo de amenazas por desarrollar

La siguiente fase debe especificar, como mínimo:

- activos y datos que se pretende proteger;
- capacidades, acceso y objetivos del atacante;
- observación, repetición, alteración e inyección de estados;
- manipulación de entradas y condiciones de carrera;
- reinicio, restauración y rollback;
- exposición de secretos, claves y registros;
- errores de implementación, configuración y dependencia;
- disponibilidad, denegación de servicio y recuperación;
- límites de confianza entre módulo, interfaz, dispositivo y sistema anfitrión.

Cada amenaza deberá vincularse con un requisito, un control propuesto, una prueba y un resultado reproducible.

## 8. Requisitos de seguridad a especificar

Antes de afirmar propiedades criptográficas deben definirse:

- primitivas criptográficas estándar y usos concretos;
- generación de números aleatorios y evaluación de sesgos;
- generación, almacenamiento, rotación y destrucción de claves;
- autenticación e integridad de mensajes;
- resistencia a repetición y manipulación;
- protección de secretos en memoria y almacenamiento;
- mecanismos de recuperación y sus riesgos;
- registros auditables que no expongan secretos;
- estrategia de pruebas, revisión de código y análisis de dependencias.

No se debe diseñar una primitiva criptográfica propia como sustituto de algoritmos estándar revisados sin un proceso de investigación y evaluación especializado.

## 9. Plan de validación

La validación debe avanzar por etapas:

1. **Reproducibilidad:** documentar versión, dependencias, entorno y comandos.
2. **Pruebas unitarias:** estados válidos, transiciones, límites y entradas inválidas.
3. **Pruebas negativas:** reciprocidad rota, estados inconsistentes, datos truncados y secuencias inesperadas.
4. **Pruebas de reinicialización:** recuperación tras errores y comportamiento ante reinicios.
5. **Pruebas de propiedades:** invariantes que deben mantenerse para todas las secuencias permitidas.
6. **Fuzzing:** entradas aleatorias o malformadas y análisis de fallos.
7. **Análisis estático y dependencias:** errores comunes, vulnerabilidades conocidas y componentes externos.
8. **Modelo de amenazas:** evaluación sistemática de escenarios de ataque.
9. **Revisión independiente:** revisión de seguridad y criptografía por especialistas.
10. **Informe de resultados:** evidencias, limitaciones, incidencias abiertas y criterios de aceptación.

No deben publicarse resultados como aprobados hasta disponer de evidencia verificable de cada etapa.

## 10. Trazabilidad y gestión de cambios

Cada resultado debería registrar:

- identificador de prueba;
- objetivo e hipótesis;
- versión o hash del código evaluado;
- sistema operativo, runtime y dependencias;
- procedimiento exacto;
- resultado esperado y observado;
- evidencia o log;
- fecha y responsable;
- estado: pendiente, ejecutado, aprobado, fallido o bloqueado.

Los cambios de arquitectura deben quedar asociados a commits y a una nota de impacto sobre las pruebas existentes.

## 11. Hoja de ruta

**Fase A — Documentación:** arquitectura, vocabulario, alcance, supuestos y límites.

**Fase B — Reproducibilidad:** publicación del código relevante, instrucciones de ejecución y pruebas automatizadas.

**Fase C — Seguridad del diseño:** modelo de amenazas, requisitos, análisis de estados y revisión de decisiones criptográficas.

**Fase D — Evaluación técnica:** pruebas negativas, fuzzing, análisis estático y revisión de dependencias.

**Fase E — Revisión independiente:** evaluación especializada, corrección de hallazgos y publicación del informe final.

**Fase F — Prototipo evaluable:** únicamente tras superar criterios acordados, definir integración, mantenimiento y respuesta a incidentes.

## 12. Presentación responsable a concursos y clientes

Descripción recomendada:

> UNBUNKER-SECURITY es un proyecto experimental de arquitectura de software orientado a la verificación de estados, la reciprocidad, la integridad y la trazabilidad. Cuenta con un modelo estructural y áreas de comprobación funcional preliminar documentadas. La validación criptográfica independiente y la evaluación frente a un modelo de amenazas formal están pendientes.

La comunicación comercial debe distinguir claramente entre concepto, prototipo, pruebas funcionales, evaluación independiente y producto validado. No se debe presentar como certificado, invulnerable, equivalente a una clave criptográfica de 128 bits ni listo para producción sin evidencia correspondiente.

## 13. Conclusión

UNBUNKER-SECURITY dispone de una línea de investigación y una arquitectura conceptual que pueden organizarse en un proceso verificable de ingeniería. El siguiente avance consiste en publicar el código fuente relevante, acompañarlo con pruebas reproducibles y someter las propiedades de seguridad a análisis formal y revisión independiente.

**Estado final de este documento:** informe de arquitectura y plan de trabajo. No constituye certificación, auditoría ni garantía de seguridad.
