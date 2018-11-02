# Planificación

## Introducción

Activos que protejer: switches, bbdd, ordenadores...

### ¿Qué tipo de servicios tenemos que implementar para protejerlos?
  
¿Cómo protegerías tu casa? Alarma, puerta blindada, cámaras, perro... Seguro de hogar.  
Son dos conceptos de protección distintos; mientras que el primero está enfocado a evitar  
intrusiones, nunca podremos evitar al atacante profesional que conoce absolutamente todas  
las maneras de sobrepasar esas defensas. Es entonces donde se ve el segundo tipo de seguri-  
dad. Un seguro de hogar nos cubrirá la pérdida siempre.
  
  * Firewall: tipo 1
  * Backup: tipo 2
  * Elaboración de planes de contingencia: incluye el tipo 2 y lo extiende. Agrega planificación

### ¿Cómo hacemos una planificación? Diseñar una política de seguridad.

  Existen tres fuentes que me van a alimentar a la hora de diseñar la política de seguridad:

  1. Realización de un análisis de riesgos: formal, identificar los riesgos a los que me enfren-  
  to en mi entorno.
  2. Vías de buenas prácticas: checklist donde se comprueban que se han aplicado las políticas que  
  hemos estudiado. Verificar que todo lo que se exige se cumple (p.ej. ver que ningún empleado  
  tiene pegada su passwd en un post-it en el escritorio).
  3. Cumplimiento legislativo: estar al orden de las leyes (p.ej. implementar ley de protección de   
  datos). 

  Tras diseñar una política adecuada es interesante:

  * Certificar la política (ISO).
  * Auditarla y verificar su validez.

## Análisis de Riesgos

Un análisis de riesgos se basa en la ejecución del _Ciclo de Seguridad_:

  * Identificar los activos: ¿qué tienes que puede ser atacado? (SW, HW, personal...)
  * Amenazas sobre los activos: ¿qué amenazas se aplican a cada activo? (atacantes, naturales...)
	- Identificar tipos de amenazas y nuestro grado de vulnerabilidad a cada amenaza: riesgo
  * Daño / impacto resultante de una amenaza efectiva: ¿qué ocurre si la amenaza se efectúa?

Ciclo: Activos sujeto a amenazas a las que tengo una vulnerabilidad, que nos generarían un cierto  
impacto.

El riesgo se mide en lo vulnerable que soy a una amenaza y el impacto que me puede causar ésta =>  
Factor de importancia.

Ejemplo:

  (1) Activo: Rec. Físicos, Amenaza: Incendio, Impacto: Total, Vulnerabilidad: Media.  
  (2) Activo: BBDD, Amenaza: Empleado deshonesto, Impacto: Muy grave, Vulnerabilidad: Alta.  
  ...  
  (q) Activo: Servidor Web, Amenaza: Atacante externo, Impacto: Bajo, Vulnerabilidad: Media - Alta.  

Tendremos que tomar medidas para disminuir el Factor de Riesgo: o disminuir el impacto, o medidas.  
orientadas a disminuir el impacto.

### Componentes del Análisis de Riesgos

#### Activos (ejemplo de clase)
  * Personal
  * Recursos físicos
  * Información Almacenada
  * Información en Tránsito
  * Imagen y reputación

#### Amenazas (ejemplo de clase)

Según su origen:

  * Ambientales: agua, frío, calor, incendios, atentado...
  * Suministro: gas, agua...
  * Personas: atacante externo (perfil menos peligroso, es múcho más peligroso el empleado dehones-  
  to, error humano).

Según objetivo:

  * Personal: ataques a infraestructuras críticas, presas de agua, electricidad, biomédicos...
  