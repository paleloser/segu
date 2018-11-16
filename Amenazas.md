# Amenazas

Se dividen, principalmente en **tecnológicas** (vulnerabilidades software, web...) y 
**humanas** (ingeniería social).

## Ingeniería Social

Existen tres medios principales para realizar enagños:

* Engaños con presencia física.
* Engaños con medios tradicionales (correo, teléfono, fax...): más exposición pero más efec-  
tividad
* Engaños por internet: mayor anonimidad pero menos efectivos.

### Engaños Presenciales

Típico timo que se puede hacer a una persona: el timo de la estampita. Técnicas de pretexto.
El atacante se inventa un escenario falso.

Las técnicas que se usan:

  * Impersonación: puede ser física o no (por teléfono).
  * Desvío de envíos: apropiarse de envíos que van destinados a otros (convencer al de UPS)
  * Baiting: tirar pinchos USB por el parking de una oficina para que los empleados los cojan y los  
  usen en sus ordenadores. El USB tendrá algún malware...
  * Dumpster diving: rebuscar en la basura (de orgaciones o personal)
  * TailGating: pasar un control de torno pegado al de delante (parking del D)
  * Shoulder surfing: mirar por encima del hombro a alguien para ficharle la contraseña.  

En la mayoría de las técincas anteriores te pueden identificar ya que son personales, aún así son más  
efectivos. 

### Engaños por Internet

Los objetivos son que la víctima ejecute un malware o que revele información confidencial.

#### Ejecución de Malware

  * Correo electrónico (+ técnicas de pretexto): mandar el malware como adjunto...
  * Enlaces a programas maliciosos en servidores web.
  * Documentos maliciosos: documentos alterados con malware para explotar una vulnerabilidad de cierto  
  programa, al explotar la vulnerabilidad se ejecuta el código guardado...

### Revelación de Secretos

Casi siempre se trara de correos electrónicos maliciosos contando engaños. Otro modo tamién es mediante  
sevidores falsos (phishing).

## Búsqueda de Información

Cuanto más se sepa del activo, más se podrá personalizar el ataque.

	1. Redes Sociales: twitter, Facebook, Instagram. La más importante actualmente para recabar  
	   información actual es LinkedIn.
	2. Actualizaciones de posición: bien en redes sociales como con dispositivos de deporte, GPS  
	   en cualquiera de sus formas.
	3. Metadatos: pueden contener absolutamente TODO. Autor, IP, versión de software de edición,  
	   fechas, dispositivos con que se hizo el documento...
	4. BOE: nombramientos de funcionarios, publicando nombre y DNI de cada persona.
	5. Mensajes en foros: se cruzan nicknames entre foros varios pudiendo establecer un perfil del  
	   activo. 

## Ataques Tecnológicos

### Nivel de Aplicación

La primera vía será atacar una vulnerabilidad en servidores. Cogerse la checklist de vulnerabilidades  
software (XSS, SQLi, CSRF, Overflows...) e ir aplicando ataques hasta dar con alguna.  

Otro tipo puede ser mediante ataques a vulnerabilidades conocidas en versiones concretas de software  
(CVE-NNN-YY para Apache A.B).

Finalmente están las condiciones de carrera: cuando hay multiples instancas del mismo programa que no  
manejan bien la concurrencia (revisar más tarde).

Cuando se descubre la vulnerabilidad se publica el expliot: programa que explota la vulnerabilidad.

Al final todos los ataques debidos a aplicación se deben a configuraciones de usuario mal imlementadas  
ó servicios desactualizados.

### Pila de protocolos TCP/IP

No son vulnerabilidades frecuentes, pero las hay.

La vulnerabilidad en el nivel de red puede ser una vulnerabilidad de diseño o de implementación. Ante  
un fallo de diseño sólo queda rediseñar el protocolo, ya que aplicará a todos.
Los ataques de implementación son debidos otra vez a que los usuarios implementan mal los protocolos en  
sus sistemas.

	* MITM
	* Christmass Day Attack

#### SSL Heartbleed

En SSL las sesiones tienen TIMEOUT por defecto. Existe un modo para mantener la sesión que es mediante  
hearbeat, es decir, mandar pequeños paquetes de peticiones al servidor solicitando una palabra e indicando  
la longitud de la palabra. Si introducíamos una longitud de palabra mucho mayor que la que pediamos el  
servidor acababa devolviéndonos su contenido en memoria.

### Ataques en cliente

Hacer reversing engineering a los programas que corren en cliente a fin de revelar las claves que usan 
para conectarse a los servidores o para cifrar sus comunicaciones. Estos ataques se pueden hacer en  
cualquier momento y no podemos controlar, como servidores, cuándo nos lo están haciendo.
Si alguien revela cómo funciona el programa por dentro se pueden controlar cifrados, hacer respuestas mali-  
ciosas...
También se pueden craftear ficheros destinados a abrirse con el programa cliente, de manera que conocida la  
vulnerabilidad del programa se pueda explotar.

### Remote Code Execution / DoS

Mandar payloads que o causen stack smash o buffer overflow ó causen excepciones y hagan que el servidor se  
caiga.

	* DDOS: distributed denial of service, es un DoS causado por exceso de peticiones coordinadas.

## Defensas Tecnológicas

### Nivel de Aplicación

	* Instalar sólo los servicios que se van a usar.
	* Tener todo actualizado al momento.
	* Nunca se puede defender correctamente una vulnerabilidad de dia 0.
	* DEP: Data Execution Prevention. Especifiar al OS qué zonas de memoria pueden ejecutar programas y cuales no.
	* ASLR: Adress Space Layout Randomization
	* Bastionado de Sistemas: revisar todas las configuraciones de los programas asegurando que no tienen  
	vulnerabilidades. Hay programas dedicados a esto: NESUS, Bastille-Linux...

## Consecuencias de Ataque

	* Ejecución de código malicioso.
	* DoS
	* Instalación de un malware: virus, gusano o troyano.
	* Ransomware.

**NOTA**: un troyano es la instalación de un servidor adicional de manera que aunque se parchee el programa que  
estaba con la vulnerabilidad inicialmente, seguiremos teniendo acceso a la víctima. Al meterte un troyano pasas  
a formar parte de una botnet.

### Advanced Persistent Threat (APT)

Se trata de ataques personalizados a un sujeto.

	* Comienzan por la recolección de información: Doxing, OSINT
	* Intrusión inicial: bien mediante ingeniería social, vulnerabilidades 0 day ó no parcheadas.
	* Asegurar comunicación continuada.
	* Búsqueda de información sensible.
	* Exfiltración de datos. Covert channels (se puede attachear información en un paquete ICMP).