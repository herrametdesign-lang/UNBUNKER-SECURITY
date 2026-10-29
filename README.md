# UNBUNKER-SECURITY

**SQ-ONE Research Labs · Herramet Design**  
**Responsable del proyecto:** Sergio Alberto Albornoz  
**Estado:** prototipo estructural experimental; evaluación técnica en curso.

UNBUNKER-SECURITY es una línea de investigación y desarrollo en seguridad informática centrada en la representación y verificación de estados, la reciprocidad entre componentes, la integridad de las transiciones y la trazabilidad de eventos.

El repositorio documenta la arquitectura propuesta, el alcance de las comprobaciones preliminares, las limitaciones conocidas y una hoja de ruta para evaluación técnica independiente.

## Estado y alcance

- **Etapa:** arquitectura conceptual y prototipo de software.
- **Comprobaciones preliminares descritas:** estructura de unidades, secuencia de seis lados, detección de fallos de reciprocidad y reinicialización.
- **Integración experimental:** el módulo DiamondUnBunker se había integrado en el entorno GENESIS para exploración funcional.
- **Validación criptográfica independiente:** pendiente.
- **Seguridad para producción:** no establecida.

Estas comprobaciones preliminares no equivalen a una auditoría independiente ni demuestran resistencia frente a ataques reales. No se debe usar este prototipo como único mecanismo de protección de sistemas, credenciales, claves o fondos.

## Modelo estructural de referencia

La propuesta de representación contempla 6 lados × 4 posiciones por lado × 3 unidades por posición = 72 unidades. Si cada unidad admite tres estados teóricos, el espacio combinatorio ideal sería de 3^72 configuraciones. Esa cifra describe el modelo matemático bajo sus supuestos; **no demuestra por sí sola 114 bits de seguridad criptográfica**, porque la entropía efectiva depende de la independencia, distribución, generación, observabilidad y control de los estados, además del diseño completo.

La meta de diseño de 128 bits se considera una dirección de investigación pendiente de especificación y validación, no una propiedad alcanzada.

## Principios de trabajo

1. Definir con precisión los estados válidos y las transiciones.
2. Detectar inconsistencias de reciprocidad e integridad.
3. Mantener trazabilidad reproducible de pruebas y versiones.
4. Separar el modelo estructural de los mecanismos criptográficos estándar.
5. Documentar resultados, límites y evidencia sin atribuir propiedades no demostradas.

## Contenido del repositorio

- docs/INFORME_TECNICO.md: informe técnico, alcance, arquitectura, comprobaciones preliminares y hoja de ruta.
- docs/PLAN_DE_VALIDACION.md: plan inicial para pruebas reproducibles y revisión independiente.

## Próximos hitos

1. Publicar el código fuente del módulo y sus instrucciones de ejecución.
2. Incorporar pruebas automatizadas reproducibles y resultados verificables.
3. Definir el modelo de amenazas y los requisitos de seguridad.
4. Evaluar aleatoriedad, gestión de claves, autenticación, recuperación y resistencia a ataques.
5. Solicitar revisión criptográfica independiente antes de formular afirmaciones de seguridad para producción.

## Licencia

La licencia del proyecto debe definirse explícitamente antes de conceder permisos de uso, modificación o redistribución.
