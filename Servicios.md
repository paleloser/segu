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

### Algo que se lleva

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

Figura izquierda:
![alt text](https://www.sbprojects.net/knowledge/footprints/smart/iso-contacts.png "Descripción del chip.")

La CPU es de 8 bits.
Los tamaños de memoria son: ROM de 8 a 32k, RAM de 256B a 4kB, EEPROM de 1k a 32k

### Autenticación por algo que se es

Autenticación biométrica: retina, iris, huella, sistema sanguíneo...