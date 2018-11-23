# Servicios de Seguridad

Dada una organización en toda su infraestructura tecnológica, el objetivo será **proteger todos  
los activos**. Para ello podemos poner servicios que controlen los **servicios de intrusión**.  
Habrá que identificar todas las fuentes de ataques y aplicar medidas acorde a la seguridad que  
cada una requiera.  
También está la vía de la securización de la información mediante cifrado y firma.  

Ante amenazas que no se les pueda aplicar una medida de seguridad siempre queda el seguro.  

## Control de Acceso

Distinquimos entre controles de acceso lógico y físico.  

### Físico

**Amenazas**: manipulación y alteración de recursos físicos.  
**Contramedidas**: establecer zonas de seguridad y establecer fronteras entre zonas. Habrá que  
prestar atención a las comunicaciones innalámbricas, metiendo sistemas de autenticación adicionales.  
Hay ataques más sofisticados como los TEMPEST que consisten en captar la radiación que emite una  
pantalla para reproducirla en otra.

### Lógico 

La vía más rápida pero menos eficiente sería cortar las comunicaciones. Pero eso es completamente  
inútil. Lo que se hace es aplicar cortafuegos para decidir qué vías son válidas de entrada, en este  
caso hay que agregar autenticación para asegurar que por las vías disponibles de entrada sólo entra  
quien queremos que entre.

## Sistemas de Autenticación

La vía primaria de autenticación es la visual, por características físicas: **algo que se es**.  
Pero la intención es autenticación en entornos digitales; en este caso usaremos un secreto compar-  
tido **algo que se sabe**.  
Otro tipo de autenticación es mediante **algo que se tiene**, como pueda ser un DNI, o un segundo  
factor de autenticación...  
También existen técnicas de localización: **sitio donde se está**.

Lo que se recomienda son los sistemas de **autenticación fuerte**: sistemas de doble factor.

Todos los sistemas de autenticación nacen para evitar la posible impersonación de alguien de  
confianza. Por lo tanto, ha de existir una fase inicial en la que la persona de confianza queda  
registrada.

Ojo: siempre hay que tener claro que estamos autenticándonos ante un servidor autorizado.

### Autenticación por algo que se lleva

Lo más típico son las tarjetas. Este concepto difiere del de _algo que se sabe_ porque el segundo  
sólo permanece en nuestra memoria, mientras que el primero es físico.

  *	Tarjetas magnéticas.
  *	Tarjetas inteligentes. Estas ya tienen una EPROM y pueden ser por contacto o sin él
  *	Teléfono móvil. Por SMS, por Google Authenticator...
  *	Token USB. De manera que la autenticación sólo se efectúa si el token está conectado.
  *	También podría ser llevar claves almacenadas en disco duro.

Centándonos en tarjetas inteligentes: las dimensiones de la tarjeta y del chip son estándares. El  
DNIe tiene 8 contactos (el chip que tiene). El chip contiene una CPU que se conecta, mediante un  
bus a un RAM, una ROM y una EPROM (a demás puede conectarse a un coprocesador criptográfico).  
La lámina central (la grande) es una toma de tierra. La superior derecha es una toma de energía,  
al igual que la inferior derecha, que le permiten trabajar a dos tipos de voltaje distintos.  
La segunda lámina superior izquierda es la de sincronismo de reloj, la segunda de la derecha es  
la de reset. Las dos izquierdas (superior e inferior) están reservadas para futuros usos.  
Queda el segundo contacto inferior izquierdo que va destinado a I/O.

![Descripción del chip.](https://www.sbprojects.net/knowledge/footprints/smart/iso-contacts.png "Descripción del chip.")

La CPU es de 8 bits.
Los tamaños de memoria son: ROM de 8 a 32k, RAM de 256B a 4kB, EEPROM de 1k a 32k

### Autenticación por algo que se es

Autenticación biométrica: retina (cada persona tiene una disposición de conos y bastones), iris, huella,  
sistema sanguíneo, geometría de la mano, facial, ADN.

Retina: se tiene que hacer por láser, lo cual no es válido a largo plazo ya que se daña el ojo.
Irirs: produce rechazo social a pesar de que funciona bien.

Existe un sitema alternativo que es basado en las características de comportamiento. La voz puede ser un  
mecanismo pero nunca usado como principal o único, ya que nuestra voz puede variar si estamos malos.
Otros métodos son el estrés, o el ritmo de tecleo.

### Autenticacion por algo que se sabe

El primer método es informando al servidor del servicio sobre la contraseña. Posteriormente en un login  
le remitiremos nuesrta contraseña y comprobará que es correcta. En este caso no estamos necesitando ningún  
periférico, lo que implica que es escalable. Nunca se guarda una clave en claro.

Para poder guardar las claves previamente se le aplica un hash. Como norma, cualquier secreto se tiene que  
guardar cifrado.

Ataques por man in the middle, bruteforce y shoulder surfing.
Los ataques de fuerza bruta se realizan en local para evitar denegación de acceso por intentos fallidos.

#### Defensas contra el bruteforce
	
* Buenas claves
* Fáciles de recordar
* Difíciles de adivinar por un ordenador, con alta entropía
* Exigir condiciones en el registro de las claves
* Esconder el fichero shadow

![Entropía en las claves.](http://imgs.xkcd.com/comics/password_strength.png "La entropía de las claves.")

#### Defensas contra MITM

* Enviar claves cifradas
* No fiarse de terminales de terceros

NOTA: los protocolos POP3 e IMAP inicialmente iban en claro. Como ellos, inicialmente muchos protocolos no  
estaban cifrados. Lo que se hizo para arreglarlo fué, en vez de cambiar todos los protocolos para que fuesen  
cifrados, añadir un wrapper que añadía una capa de cifrado sobre cualquier cosa (SSL/TLS).

## Sistemas de autenticación dinámica

Se basa en utilizar claves de un sólo uso. Son claves de usar y tirar de manera que casi no nos importa si  
nos la llegan a pillar.

### S/Key

Es un sistema basado en un servidor que, partiendo de una clave maestra elegida por el cliente, genera N  
hashes consecutivos y se las da al usuario que se va a autenticar. En el proceso de autenticación, el  
cliente solicita el acceso y será el servidor el que le pida el hash N al cliente, en vez de la clave inicial.  
En un acceso siguiente, el servidor le pedirá el hash N-1 y así sucesivamente. 
De este modo, si un atacante se hace con un hash, en el próximo login no le va a servir de nada.

El problema de este mecanismo es que el cliente tiene que almacenar los N hashes, si alguien se hace con el  
terminal del cliente, está vendido. A su vez, como se genera un número fijo de claves, el uso está acotado.

### Time-based key

El servidor conoce un mecanismo temporal de variación de claves, de forma que cada x tiempo la clave es distinta.  
El cliente tendrá un dispositivo físico con el mismo mecanismo implementado de tal manera que al darle al botón  
'generar' del dispositivo, saque por un display la clave.  
Este sistema se usa como mecanismo de doble factor. (SecureID)

### Uso del Móvil

Mecanismos de doble factor diversos: google authenticator, sms...

### Sistemas de Reto-Respuesta

El usuario solicita autenticación. El servidor responde con el reto X, con lo que el usuario, conocedor de  
la clave, ha de mandar la respuesta al reto X. El _reto_ se trata de una función criptográfica.

Este sistema tiene dos problemas.

* Repetción de retos: si un atacante sabe la respuesta a un reto porque la ha snifeado antes, ante una  
repetición de reto podrá hacer la impersonación.
* Tampoco es un sistema inmune a la captura de la contraseña en el terminal (keylogger). 

## Protocolos de Autenticación

* PAP: personal access protocol -> La clave va en claro
* CHAP: challenge based authentication protocol
* EAP: extended authenticated protocol
|--> EAP-MD5
|--> EAP-OTP
|--> EAP-GTC
|--> EAP-TLS
|--> EAP-TTLS: solo se autentica el servidor