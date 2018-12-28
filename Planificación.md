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

1. Realización de un **Análisis de Riesgos**: formal, identificar los riesgos a los que me enfren-  
to en mi entorno.
2. Vías de **buenas prácticas**: checklist donde se comprueban que se han aplicado las políticas que  
hemos estudiado. Verificar que todo lo que se exige se cumple (p.ej. ver que ningún empleado  
tiene pegada su passwd en un post-it en el escritorio).
3. Cumplimiento **legislativo**: estar al orden de las leyes (p.ej. implementar ley de protección de   
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

  | Activo | Amenaza | Impacto | Vulnerabilidad |
  | :--- | :--- | :--- | :--- |
  | Recursos físicos | Incendio | Total | Media |
  | Bases de Datos | Empleado deshonesto | Muy grave | Alta |
  | ... | ... | ... | ... |
  | Servidor web | Atacante externo | Bajo | Media/Alta |

Tendremos que tomar medidas para disminuir el Factor de Riesgo: o disminuir el impacto, o medidas.  
orientadas a disminuir el impacto.

### Componentes del Análisis de Riesgos

#### Activos
  * Personal
  * Recursos físicos
  * Información Almacenada
  * Información en Tránsito
  * Imagen y reputación

#### Amenazas

Según su origen:

  * Ambientales: agua, frío, calor, incendios, atentado...
  * Suministro: gas, agua...
  * Personas: atacante externo (perfil menos peligroso), es múcho más peligroso el empleado dehones-  
  to, error humano.

Según objetivo:

  * Personal: ataques a infraestructuras críticas, presas de agua, electricidad, biomédicos...
  * Recursos físicos: ataques que vayan orientados a dañar recursos físicos, romper equipos...
  También existen ataques orientados a ganar el acceso a los recursos físicos. Se realizará con-    
  trol de acceso físico a sistemas que requieran alta seguridad.
  * Ataque a la información: modificar sus aspectos de autenticidad, integridad, confidencialidad  
  y disponibilidad (no repudio).
  * Utilización: ataques de denegación de servicio.
  * Imagen y reputación: ataque importante para empresas con alto caché, por ejemplo, un defacing  
  preocupará más a una empresa de ciberseguridad que a otra.

#### Impacto

**Cuantificar el daño** que te haría que una amenaza se materialice sobre un activo (ataque). El pro-  
blema es que la cuantificación en muchas ocasiones es relativa (no se puede asignar una cifra de €)  
al daño de un ataque. Si la cuantificación es medible decimos que es absoluta.

#### Vulnerabilidad

**Cuantificar la probabillidad** de que una amenaza se materialice sobre el activo. 

	V = p(amenaza) * p(éxito de la amenaza)

### Metodologías de Análisis de Riesgos

Metodología de Análisis y GEstión de Riesgos IT (MAGERIT). Es la que se aplica en la administración pú-  
blica de España. Muchas empresas privadas la usan también. De las herramientas de Análisis de Riesgos  
del CERT se usa Pilar.

### Tabla de Riesgos

| Riesgo | Activo | Amenaza | Impacto | Vulnerabilidad |
| :--- | :---: | :---: | :---: | ---: |
| 1	| BBDD | Empleado deshonesto | Muy grave | Media |
| ...	| ...	| ...	| ...	| ... |
| i | Servidor Web | Atacante externo	| Muy bajo | Media |

Los activos los protegeremos en función del coste asociado al impacto de las amenazas. Los costes podrán  
ser:

1. Directos: tocará reinvertir en equipos, controlar en RRHH, mantenimiento de los equipos...
2. Indirectos: se aumenta la dificultad de uso, se pueden aplicar restricciones de servicios que complican  
las prestaciones.

**Statement:** nunca se puede llegar a cubrir el 100% de las amenazas.

Tenemos que diferenciar dos tipos de costes: costes debidos a los impactos no cubiertos y el coste debido a  
la aseguración de los impactos. Lo ideal es asegurar todos ellos activos cuyo coste de aseguración sea menor  
o igual al coste de impacto. Es decir, alguien que no haga gastos en seguridad va a estar asumiendo un alto  
coste en impactos, pero tambiíen alguien que está asegurando absolutamente todo estará aplicando un exceso    
que le saldrá caro.


## Guía de Buenas Prácticas - ISO 27000

* ISO 27001: sistema de gestión de sistemas de la información.
* ISO 27002: guía de buenas prácticas a implementar en un SGSI => 134 controles. Se pide certificación.


## Legislación

* GDPR: reglamento general de protección de datos.
* LSSI
* LACSP: administración pública electrónica.
* PCI-DSS: operaciones con tarjetas de crédito. (Internacional)
* SOX: seguros
...

## Certificación y auditoría

Certificación: realizar la checklist hasta cumplir los requisitos para que te den una vez la certificación.
Auditoría: realizar pruebas periódicas para asegurar que mantienes los requisitos que te concedieron la cer-  
tificación.