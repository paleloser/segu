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

## Protocolos de Autenticación (Control de acceso Lógico)

* PAP: personal access protocol --> La clave va en claro
* CHAP: challenge based authentication protocol
* EAP: extended authenticated protocol  
|--> EAP-MD5  
|--> EAP-OTP  
|--> EAP-GTC  
|--> EAP-TLS  
|--> EAP-TTLS: solo se autentica el servidor  

### Single Sign On (SSO) 

Un cliente quiere acceder a un servidor. El servidor solicita una autenticación y cuando el cliente se la  
provee comprueba que es verídica. Para evitar que el cliente tenga que recordar muchas claves surge un tercer  
agente que será el que verifique la identidad tanto del servidor como del cliente. El tercer agente, autenticador  
almacenará las claves privadas de cada uno de tal modo que sea el único en la comunicación capaz de realizar  
ese trabajo.

Existen dos modos de hacer esta verificación:

* En el primer caso, el cliente/servidor le da la clave privada al verificador, quien le da un token para que use  
en el momento de la autenticación.
* El segundo modelo es aceder primero al servidor, ofreciéndole nuestras claves públicas. El servidor le remitirá esa  
clave pública al autenticador, quien le confirmará que esa clave pública se corresponde con mi identidad.

El primer caso es más seguro ya que no estamos revelando nuestra clave pública ante nadie más que el autenticador.  
El segundo caso es más cómodo ya que no tenemos que actualizar nuestras aplicaciones, simplemente emitir nuestra clave  
y que el servidor sea quien haga el resto del trabajo.

#### Verficación antes de los servidores (KERBEROS)

En este escenario tenemos:

* Cliente (U)
* Servidor (V)
* S. Autenticador 1: almacena las claves de los servidores (TGS)
* S. Autenticador 2: almacena las claves de los usuarios (AS)

Cuando el usuario/cliente se loguea en el ordenador por la mañana lo que está haciendo es iniciar una sesión.  
Al iniciar sesión será el AS quien le ceda un token que tenga una valided por el número de horas que  
trabaja el usuario (8 horas, por ejemplo). A partir de ahora, cuando el usuario quiera usar un programa del  
sistema, emitirá una solicitud de uso junto con su token a el TGS. El TGS le emitirá un segundo token de  
servicio, que le permitirá usar el servicio durante un tiempo. Teniendo ya el toquen de sesión y el de  
servicio, el cliente ya podrá usar el servicio concreto.

		Usuario  		-------------------- <ID_U, ID_TGS, T1> ---------------------> AS
    <ID_U, Ku, ADDRu> 	<------- <E_K-U(TIC_TGS, K_U-TGS, ID_TGS, T2, LT2)> -----------

    		TIC_TGS: <E_K-TGS(ID_U, ADDR_U, K_U-TGS, ID_TGS, T2, LT2)>

TIC_TGS: Es a su vez un conjunto cifrado con la clave del servicio que contendrá <ID_U, ADDR_U, K_U-TGS, ID_TGS, T2, LT2>
Así, cuando el cliente reciba el paquete del AS, podrá descifrar con su clave la clave de sesión conjunta con el servicio  
(K_U-TGS), la duración de la sesión (LT2), el identificador del servidor de autenticación (ID_TGS) y el conjunto cifrado.  
Precisamente por la encriptación de dicho conjunto, se lo podrá reenviar al TGS, para que este lo descifre con su clave  
y pueda conocer la clave común K_U-TGS y la dirección del cliente que la comparte (ADDR_U). También conocerá la duración  
de la clave y los identificadores.

    Usuario --------------------- <ID_V, TIC_TGS, AUTH_U > ------------> TGS
    		<----------------- <E_K-U(TIC_V, K_U-V, ID_V, T4)> ---------- 

    		AUTH_U: E_K_U-TGS(ID_U, ADDR_U, T3)
    		TIC_V: <E_K-V(ID_U, ADDR_U, K_U-V, ID_V, T4, LT4)>

Ahora se repite el mismo proceso con el servidor de autenticación de servicios, generándose la clave entre el servicio y  
cliente (K_U-V) que servirá para cifrar la comunicación entre ambos.

¿ Por qué usamos dos servidores de autenticación y no uno?

La respuesta es la _federación_: teniendo servidores de servicios separados de los de clientes, usuarios de una empresa A  
podrían usar servicios de otra empresa B. De este modo, con servidores separados, los de la empresa A no tienen que saber  
los de la empresa B, mientras que si fuese con un sólo servidor el de la empresa A tendría que saber las claves del B.

#### Verificación después del servidor

* AAA: Authentication Authoritation Accounting
* A4C: AAA + Auditability + Charging

**AAA - RADIUS**

Sólo se establece entre el servidor y el autenticador. La propuesta historicamente más aceptada fué el TACACS. Luego CISCO  
lo upgradeó a TACACS+ y, para que se convirtiese en un standard no propietario se creó el RADIUS (RFC 2865/66).

En el handshake del RADIUS se sigue el siguiente orden:

1. ACCESS REQUEST: el servidor lo manda al autenticador, conteniendo el UID y la clave del usuario cifrada E(k)
2. ACCESS ACCEPT/DENY: según la vericidad de la clave, le responde el autenticador al servidor. En esta respuesta se envían  
atributos/parámetros para configurar en la red del servidor - cliente, esos atributos pueden ser tipo de servicio, dirección  
IP, parámetros específicos del vendor...  

También se puede usar una autenticación basada en retos:

1. ACCESS REQUEST -> 
2. ACCESS CHALLENGE <-
3. ACCESS REQUEST ->
4. ACCESS ACCEPT/DENY <-

El servicio de accounting no es más que una base de datos en el servidor de autenticación donde se va registrando el uso  
del cliente para luego poder cobrar a medida. El servidor es el que notificará al autenticador acerca del uso del servicio  
por parte del cliente.

**A4C- DIAMETER**

Parte del RADIUS, añadiéndole amplificaciones negociables, es decir, utilicar el mecanismo de RADIUS aplicado de manera  
específica para ciertos servicios: MOBILE_IP, UMTS, NASREQ. 

#### SSO En entornos WEB

1. OpenID: login with facebook, Google... Es una comunicación triangular entre cliente - servidor -  
verificador (OpenID provider).

  C ---------------- (OpenID) --------------> S
  C <----------------- 303 ------------------ S

  C ---- Auth. Req ---> V -- Init. Assoc. --> S
  C <-- Sign. Assoc. -- V <-- Assoc. Keys --- S
  
  C -------------- Sign. Assert. -----------> S

2. SAML: Security, Assertion, MarkUp Language
3. OAUTH.

## Defensa Perimetral

Existen dos tipos de entornos de defensa perimetral: el perímetro del sistema y el de la red.  

### Sistemas
#### Cortafuegos personales

Cortafuegos configurados específicamente a cada usuario. Se puede seleccionar bloqueos tanto  
de entrada como de salida bien por puerto, direcciones o aplicaciones. Esto es rentable en  
escenarios con pocos sistemas. 

Las grandes desventajas de este mecanismo es que en un entorno grande la administración es  
mucho más compleja. También jode para entornos donde cada sistema tiene su OS (heterogeneos)  
y en entornos heredados (Legacy Systems). 

### En Red

El objetivo es aplicar una política de seguridad a un conjunto de sistemas. Primero tendremos  
que definir lo que significa conjunto.

* Establecer **zonas** de seguridad: estableciendo un conjunto de políticas comunes a dichas  
zonas/departamentos.

**¿Cómo hacemos un cortafuegos?**


1. Cortafuegos de aplicación: nivel 7
2. Cortafuegos de circuitos: nivel 4
3. Filtro de paquetes: nivel 3
4. Cotrafuegos transparente: nivel 2

#### Filtro de Paquetes

Un filtro de paquetes es un router inteligente. Mira las cabeceras de los paquetes que le llegan,  
compara las cabeceras IP con la tabla de filtrado (Security Table) y verifica si ese paquete ha de  
ser enrutado (por la ruta que tenga en su iptable) o si ha de ser deshechado.