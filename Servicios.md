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

Lo que se recomienda son los sistemas de autenticación fuerte: sistemas de doble factor.

Todos los sistemas de autenticación nacen para evitar la posible impersonación de alguien de  
confianza. Por lo tanto, ha de existir una fase inicial en la que la persona de confianza queda  
registrada.