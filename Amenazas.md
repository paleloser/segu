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

<pre>
|	----	----	|	La primera vía será atacar una vulnerabilidad en servidores. Cogerse la checklist  
|			|	de vulnerabilidades software (XSS, SQLi, CSRF, Overflows...) e ir aplicando ataques  
|			|	hasta dar con alguna.
|			|	Otro tipo puede ser mediante ataques a vulnerabilidades conocidas en versiones con-  
|			|	cretas de software (CVE-NNN-YY para Apache A.B).
|	APLICACIÓN	| 	 Finalmente están las condiciones de carrera: cuando hay multiples instancas del mis-  
|			|	mo programa que no manejan bien la concurrencia (revisar más tarde).
|			|
|			|	Cuando se descubre la vulnerabilidad se publica el expliot: programa que explota la  
|			|	vulnerabilidad.
| - - - - - - - |	
|	TCP / UDP 	|	
| - - - - - - - |	
|	 RED / IP 	|
| - - - - - - - |
|	  ENLACE	|
| - - - - - - - |
</pre>