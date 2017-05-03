
# RFC Decidim Identity Protocol

## Índice

* [Resumen](#DIP-summary)
* [Especificaciones Técnicas](#DIP-specs)
* [Discusión](#discusion)


## <a name="DIP-summary"></a> Resumen

En resumen, usuario se *registra* en el sistema (nombre de usuario asociado a una cuenta de correo y a una contraseña), luego se le piden datos de *verificación* (pueden ser datos del padrón o un número identificador único enviado por correo postal o conseguido en una oficina municipal), la cuenta de usuario queda verificada y no se guardan los datos de verificación. De esta manera el usuario puede acogerse al cuerpo digital (a modo de escafandra, vestimenta o armadura) y ejercer toda una serie de derechos en el espacio digital democrático, sin que nadie pueda conectar esa identidad digital con su identidad personal, pero asegurando a su vez que sólo existe una cuenta de usuario por cada indivíduo con derechos jurídicos o sociales, y que todo indivíduo puede acceder a tener una cuenta. En otra palabras, aseguramos que el mapeo entre usuarios del sistema e indivíduos o personas es uno-a-uno, pero no sabemos quién-es-quién.

Pero podemos ir más allá: puede ser la ciudadanía quien custodie su identidad digital verificada, sin depender de un servicio centralizado, y hacerla valer frente a terceros sin la intermediación del Ayuntamiento. Incluso podemos hacer acuerdos públicos, verificables por cualquier persona, entre ciudadanos, sin la intermediación del Ayuntamiento y, además, con la misma validez jurídica que si el Ayuntamiento mediara ese acuerdo. Y todo ello sin renunciar a la privacidad. Aunque parezca algo mágico, la tecnología actual permite hacer esto.

Todo esto sería posible con Decidim Identity Protocol basado en una combinación de (cuidado que aquí vienen palabras técnicas) critografía de clave asimétrica y sistemas distribuídos de *public ledger*. Si ya conoces lo que significan estos términos puede saltarte la siguiente sección y navegar directamente a la descripción técnica. Si todo esto te parece magia, o te suena a Klingon, a continuación tienes una explicación metafórica de cómo funcionaría el sistema.

### <a name="DIP-specs"></a>Especificaciones técnicas

Fundamentalmente DIP se basa en un sistema descentralizado de anonimato con verificación, basado en certificados público/privados (o criptografía de clave asimétrica) y gestionados con tecnología distribuída (tipo *blockchain* o *bittorrent*). La plataforma [Decidim](https://decidim.github.io) sirve a modo de *frontend* y mediación de un sistema distribuído de almacenamiento y acceso a identidades y contenidos y como intermediario descentralizador de un servicio centralizado de certificación (p.e. un padrón municipal). 

0. **Registro y verificación de usuarios**: Este es el sistema que funciona ahora mismo en [Decidim](https://decidim.github.io). Las personas usuarias se registran con un nombre de usuario, correo electrónico y contraseña asociada en Decidim. Para terminar el registro deben validar su dirección de correo electrónico. Una vez el usuario está registrado y su correo validado, puede pasar a ser verificado como ciudadano de Barcelona. Para ello se le piden datos adicionales de verificación de identidad y se realiza una consulta para verificar dichos datos: p.e. se le piden datos personales (nombre completo, fecha de nacimiento, dirección postal) y se comparan con el registro del padrón, también puede verificarse un código personal enviado a casa, o un SMS. Una vez se han comprobado dichos datos se marca como verificada esta identidad digital, pero no se almacenan los datos de verificación (excepto los estríctamente necesarios para revocar esa identidad, p.e. se guarda un *hash* del DNI [^9]). 
![Registro y verificación de usuarios](https://i.imgur.com/7E5YWen.png)

[^9]: En este punto existe mucho márgen de mejora en la seguridad del Decidim.


1. **Creación y almacenamiento de claves privadas**: es recomendable que la creación de claves privadas sea reproducible, por lo que además de una contraseña que sirva para descifrar la clave privada (en su espacio de almacenamiento habitual) sería recomendable tener un generador de claves privadas conbinando una contraseña (puede ser la misma que la de cifrado) con datos privados que sólo el dueño de la clave conozca pero que permita aumentar la entropia de entrada y mejorar la seguridad. Sistemas de este tipo son comunes en la generación de carteras de bitcoin. Esta clave se puede guardar de manera segura en el móvil o en otros dispositivos (p.e. una llave USB) o una carpeta del ordenador (para los usuarios que no quieran o no puedan depender de un móvil y tengan los conocimientos adecuados). El sistema *MobileID* del Ajuntament de Barcelona puede servir para generar y almacenar dicha clave de manera fácil para las personas no expertas. Esto es una gran ventaja porque el problema de los sistemas de cifrado con clave asimétrica reside precisamente en la barrera de acceso técnico a la gestión y segurida de dichas claves. *MobileID* es una plataforma ideal para romper con esa barrera al ser una app móvil de fácil instalación y usabilidad. 
![Creación y almacenamiento de claves privadas](https://i.imgur.com/lonhiGi.png)

2. **Verificación de clave pública**: cuando un usuario verificado entra en Decidim puede optar a verificar su clave pública. Para ello se le pide subir la clave pública (esta operación puede hacerse por el móvil o por el ordenador). La clave pública se firma con la clave privada del Ajuntament, se le re-envia a la usuaria y se publica en un listado oficial de Decidim desde donde se comparte en un sistema *blockchain*. El cliente debería de hacer un *push* a otros servidores para asegurarse de que su clave pública firmada se publica realmente.
![Verificación de clave pública](https://i.imgur.com/O7fMB7d.png)

3. **Firmas, contratos y verificación pública**: A partir de aquí cuando una usuaria da su apoyo a una iniciativa o propuesta lo que hace es firmarla con su clave privada y la iniciativa firma se publica. Esta publicación se distribuye posteriormente, o puede incluso firmarse de manera distribuída. Aunque el Decidim permita hacerlo aprovechando la usabilidad, calidad del servicio y referencialidad de un servicio centralizado, dicha centralización no es necesaria para el funcionamiento del sistema.
![Firma digital de iniciativas ciudadanas](https://i.imgur.com/hUMWd2H.png)


## <a name="discusion"></a>Discusión 

El problema central del DIP es la revocación en caso de corrupción, pérdidas o robo de la clave privada y las medidas necesarias para evitar dobles verificaciones. Solucionarlo no es fácil: o volvemos a un sistema (semi)centralizado para las verificaciones o perdemos el anonimato. Todas las soluciones pasan por re-equilibrar tres factores: 1) descentralización, 2) univocidad de la verificación, 3) anonimato. Las diferentes soluciones resultan en equilibrios diferentes en los que o bien se sacrifican garantías de anonimato para asegurar la verificación, o se descentraliza menos para garantizar el anonimato, etc. 

Uno de los grandes problemas a la hora de encontrar el equilibrio más adecuado es atender a tres tipos muy diferentes de usos de la identidad en el ejercicio de los derechos democráticos, ya que estos servicios demandan equilibrios diferentes entre descentralización, anonimato y verificación:

* Votaciones
* Firmas
* Asambleas

Para una votación la protección de la privacidad (o el anonimato) es sólo importante de cara a impedir que se relace a la persona con su voto. En las mesas electorales los nombres y DNI del censo están disponibles y visibles, se comprueba tu identidad. Eso no es un problema si se garantiza que el voto es secreto. Es decir, no importa que se sepa quién eres, siempre y cuando no se sepa qué votas. Existe tecnología digital criptográfica que, separando la mesa electoral que te identifica (el servidor que gestiona las identidades), de la urna y el recuento (mixers y reconstrucción matemática de los resultados) pueden asegurar con bastante fiabilidad la protección del secreto de voto. 

Pero si el mismo sistema de identidad digital se quiere utilizar para la firma digital, como la que se requiere para recoger firmas para una iniciativa legislativa, y además queremos que cualquiera pueda auditar el recuento de firmas, entramos en un escenario diferente, en el que es preciso el anonimato con verificación para poder garantizar la privacidad de las firmas. 

Otro problema con el que nos encontramos en [Decidim](https://decidim.github.io) es que la plataforma está orientada a facilitar la integración entre lo presencial y lo virtual. En muchos casos es preciso inscribirse para una asamblea (para poder predecir el número de asistentes) y aquí entramos en la dificultad añadida de las identidades: ¿cómo protejo la privacidad de una persona que se presenta a una sala en la que hay una asamblea y que se ha inscrito digitalmente, pero aparecen otras dos que dicen lo mismo y no hay sitio para todos?.

Aún nos quedan problemas por resolver. Las decisiones que tomemos en este sentido van a condicionar mucho el ejercidio de derechos democráticos en el futuro. Ni Facebook, ni Google, ni Twitter, tienen un interés genuíno en democratizar la sociedad (o su interés es proporcional a la democratización de su junta de directivos o el mercado de valores en bolsa). Existen iniciativas tecnológicas que intentan abordar algunos de estos problemas (p.e. [Onename](https://onename.com/), [Sovrin](https://sovrin.org/) o el proyecto europeo [Decode](http://www.decodeproject.eu/)), pero les falta el anclaje institucional y la interfaz útil y pragmática de las plataformas de participación como Decidim que puedan atraer y legitimar el uso de estos sistemas. El futuro está en nuestras manos. 


