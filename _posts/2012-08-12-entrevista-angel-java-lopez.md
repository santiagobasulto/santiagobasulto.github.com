---
layout: post
title: "Entrevista con Angel Java Lopez"
category: entrevistas
tags: programacion entrevistas programadores
---

Antes de reunirme con Angel no sabía sinceramente qué me iba a esperar. Había leído bastante de su blog y había visto alguna charla dada por él, pero no mucho más. Cuando le envíé el correo para proponerle esta entrevista, me sorprendió su respuesta: "Cómo no! Podemos hacerlo!". Sin preámbulos, sin preguntas, sin lineamientos ni juicios.

Una vez charlando con él, me encontré con un tipo muy afable, que le gusta conversar y expresar sus ideas. Enseguida noté una latente fascinación por cuestiones no técnicas, las cuales traté de aprovechar al máximo por la riqueza inherente de entender la programación en contexto. Por ejemplo, hablamos mucho de historia; me contó de sus comienzos, con gran detalle; pasando por diferencias psicológicas entre hombres y mujeres, formas de hacer negocios, el futuro de la computación, y muchas otra cosas más. Espero que lo disfrutes tanto como yo.

Sin más rodeos, la entrevista con Angel.

---------------------------------------

**Santiago**: ¿Cómo arrancaste con la programación?

**Angel**: Yo arranqué en la UBA, en la facultad de Ingeniería, si bien antes ya había estado en algunos institutos. En ese entonces no había computadoras personales, había que programar en papel. Eso era cerca del año 78.

**Santiago**: ¿Era el nacimiento de la computación en Argentina?

**Angel**: Acá sí. En otros lugares no. Por ejemplo, Microsoft ya había sido fundada. Pero acá no se sabía lo que era una computadora personal. Era todo Cobol, Assembler de IBM 360, etc.

En el 80, cuando entré a la facultad de ingeniería se hacía todo con tarjetas perforadas, no tocabas la computadora. Había una IBM 360 que estaba en el cuarto piso encerrada. No había otras opciones (como comprar algo para tu casa, o en algún otro lado).

En el 81 un ayudante me convocó para una consultora y ahí arranqué a hacer más programación, y ahí vi empresas que tenían mini computadoras, o una computadora con varias terminales. En esa época empezaban a aparecer algunas micro coputadoras, que ocupaban el tamaño de una heladera de quiosco.

**Santiago**: ¿Cómo era programar en esa época?

**Angel**: Era difícil. Cuando mandabas a compilar algo te podías ir a tomar un café y volver y todavía no había terminado. Cada productor de hardware tenía su propio Sistema Operativo y su propio lenguaje. Eran principalmente mercados verticales, no estaba el concepto de un mercado horizontal.

Solamente en el ambiente académico había Unix, pero acá no había mucho. Habían varios proveedores, cada uno con su lenguaje y sistema operativo. Me acuerdo de *Ohio Scientific*, *Cromemco*, entre otras.

**Santiago**: ¿Qué clientes había?

**Angel**: De todo. Fábricas, gobierno, etc. Me acuerdo los sistemas de sueldos, que en aquel entonces cambió la forma de calcular el aguinaldo, que debía calcularse de forma proporcional a los meses que se habían trabajado y hubo que cambiar todos los sistemas, porque antes no hacía falta guardar memoria de los sueldos anteriores. Con el cambio empezó a ser necesario guardar la información de los sueldos. Usábamos diskettes, entonces la forma para calcularlo era: poner el diskette de Enero, apretar Enter, sacar el diskette de Enero, poner el diskette de Febrero, apretá Enter, y así sucesivamente.

Se usaba mucho las cintas continuas, y era común pasear de un lado para el otro con las cintas. En esa época hicimos algunos sistemas para el gobierno militar, que después fueron exportados a Italia o Francia.

Ya apartir del año 81 empezaron a llegar las primeras PCs, de la mano de IBM. Lo que hizo IBM bien en ese momento fue permitir la expansión del hardware de las PC con componentes de distintos fabricantes. Contrariamente a lo que hacían con sus Mainframes. En los mainframes no se podía cambiar nada sin romper la garantía, incluso si fabricabas algo podías ser demandado. IBM distribuía dos sistemas operativos, uno llamado UCSD Pascal, y el otro era PC-DOS. En el año 85 recuerdo haber booteado algún Xenix, que era una versión de Unix hecha por Microsoft, que eran como 12 diskettes y necesitabas cargarlos todos para bootear. Encima, las máquinas venían con una sola disketera, entonces necesitabas bootear con un diskette, sacarlo, y cargar otro diskette con el editor.

**Santiago**: ¿Cómo era el ambiente en la facultad en esa época?

**Angel**: En la facultad había bastante movimiento. Habían dos opciones, la UTN creo que apareció cerca del año 79. En la UBA la carrera era Analista de Sistemas. Era bastante variado, había materias en las que se programaba y en otras que no. Pero se hacía todo con tarjetas perforadas. No se usaban PCs en la universidad (aunque ya estuviesen en el mercado). Entonces dejabas tu trabajo con tarjetas peforadas el miércoles y al otro miércoles tenías el resultado. Un ejercicio como ordenar un vector te podía llevar un cuatrimestre. Lo más problemático de todo eso era perforar las tarjetas, porque había solo dos perforadoras en la facultad. Entonces había servicios alrededor de la facultad que las perforaban, porque en la facultad había colas de media cuadra para perforar.

Entonces en el 81, cuando me senté en una PC, que tenía un editor para mi solo, estuve dos días seguidos programando. Arranqué el viernes a la noche y me sacaron el lunes a la mañana. Estaba bárbaro, editabas , compilabas y ejecutabas en el mismo lugar. Eran editores de linea! pero para mi era fantástico. Veías las letras ahí en la pantalla fosforescente y podías compilar y probar en el momento.

En segundo año ya se arrancaba más de lleno con programación. El primer año era bastante filtro, era mucho assembler. En segundo ya se arrancaba con ALGOL W, y algunos otros lenguajes. Había uno interesante que se llamaba BCPL, que era bastante sencillo, y a su vez permitía implementar BCPL en el mismo BCPL. Entonces se hacía muy fácil migrarlo a diferentes arquitecturas.

**Santiago**: ¿Cuál fue el primer programa que escribiste?

**Angel**: El primero lo hice en papel, era un programa para calcular una jugada de Jaque Mate en dos movidas en Cobol. Tardé como dos años en correrlo, porque no tenía forma de hacerlo.

**Santiago**: ¿Anduvo?

**Angel**: Más o menos, no tenía recursión Cobol en aquel entonces. Por eso lo hice solamente en dos jugadas.

Después ya arranqué con las cosas que hago hoy, escribir intérpretes de pequeños lenguajes, que me puso más canchero en la parte de programación.

**Santiago**: ¿Qué profesores/mentores recordás de aquella época?

**Angel**: Había mucha gente brillante. Recuerdo puntualmente al Ingeniero Guido Vasallo, que en programación 4 nos enseñó mucho de lenguajes. Todos los sábados a la mañana me tomaba el 22 desde Quilmes Oeste, y me bajaba en la facultad. Entonces todos los sábados de 8 a 1 te daba un lenguaje diferente, por ejemplo un sábado veías Prolog, al otro Lisp, etc. Una vez me lo crucé en una clase y le pregunté qué lenguaje nuevo podía aprender, y él me sugirió Smalltalk.

El problema era que no pude usar mucho Smalltalk, como algunos Lisp, porque estaban orientados a terminales gráficas, y acá los monitores gráficos eran muy caros. Me acuerdo de las plaquetas Hércules, muy populares en la época, que eran gráficas monocromáticas, porque el color era más caro aún. Incluso, las de "color", tenían solamente 4 colores. Entonces Smalltalk quedó medio relegado, por las posiblidades que teníamos.

**Santiago**: ¿Te acordas de las primeras Macs?

**Angel**: Sí, pero tampoco programábamos mucho en Macs. Eran muy caras. Las PCs eran mucho más baratas. Recuerdo cuando apareció la Lisa, que ya venía con Mouse, y tenían interfaz gráfica monocromática. También pasaba que en su tiempo, para poder desarrollar en Apple tenías que firmar un contrato y unos libros. En esa época la comunicación era más difícil. Contactar a alguien internacionalmente era muy difícil. Incluso después de pedir todos los permisos tampoco te aseguraban que lo puedas conseguir, entonces la mayoría programaba para PCs. Tampoco había mucho mercado. De todas formas recuerdo gente que programó algún sistema para restaurants en Mac, pero después terminó migrándolo a PCs porque tenían más mercado.

**Santiago**: ¿Cuáles eran los lenguajes dominantes de la época?

**Angel**: Habían muchos. Recuerdo la movida que hizo Microsoft. Porque en los inicios de Windows se programaba todo en C, pero al tiempo largaron Visual Basic. Visual Basic en los 90 llevó la programación gráfica a las masas. Programar en C era muy complicado, quedó relegado para hacer programas específicos que necesitaban mucha terminación.

Clipper apareció al final de los 80, con el Clipper Summer 87, que hacía mucho más fácil programar para DOS que en C u otro lenguaje. Fue muy popular pero le costó hacer el cambio a la programación gráfica, como le pasó a Lotus 1-2-3 y a Quattro Pro.

Es muy interesante la historia de Turbo Pascal. En los años 80 Borland compra una empresa europea que distribuía un compilador de Pascal y el fundador de esa empresa era Anders Hejlsberg, que ahora es el principal arquitecto de .Net. Entonces cuando Borland compra la empresa de Hejlsberg, él se suma y crean Turbo Pascal, que después pasa a Delphi, y Object Pascal, entre otros.
Lo interesante de Turbo Pascal era el IDE, con un muy buen editor y debugger, que tenía inspección de variables, step-by-step, etc, que no era común en la época.

También estaba el Turbo C, que yo lo usé bastante y era muy lindo. En ese momento ocurrió algo curioso. La curva de complejidad y los precios fueron bajando. Se podía comprar en la calle Viamonte el Turbo C por cien dólares. Hasta que apareció Windows y nuevamente subió el costo de todo.

**Santiago**: ¿Y Unix? ¿Qué te acordás de esos años?

**Angel**: Lo que pasaba acá en Argentina, en el año 85 más o menos, era que las computadoras seguían siendo muy caras. Era posible acceder a una PC, pero era una tecnología costosa. Las empresas que necesitaban cargar datos tenían que comprar varias PCs, y no era económico. Entonces hubo un tiempo en que surgió Unix, con la idea de tener varias terminales bobas adelante de una sola computadora que corría Unix. Pero curiosamente, entre el año 85 y el 86 explotó lo que se venía gestando, que era la Red. Apareció la plaqueta Lantastic, después apareció Novell, e hizo fácil agregar una plaqueta y conectar varias PCs, y tener computadoras más poderosas y más económicas.

Aparte era bastante difícil programar para Unix. Entonces, Unix tuvo su ventana, pero lo terminó tapando la PC y la red.

**Santiago**: ¿Qué te acordás de los comienzos de Internet?

**Angel**: Empecé a navegar por algunos BBSs como MPOnline. Desués apareció algún Netscape o algún Internet Explorer, que eran de 16 bits. Cuando tenías que bajar una imagen tenías que esperar que termine de cargar la imagen para que siga cargando la página, porque eran monothread.

Ahí fue cuando conocí Java.

**Santiago**: Contanos un poco más de Java.

**Angel**: Comencé en el año 95. Fue muy importante Internet, porque te lo podías bajar y compilar gratis. En el año 97 escribí un libro para MP Ediciones de Java. Java prendió mucho, pero el problema era que Sun vendió más de lo que tenía que vender. Por ejemplo, JDBC apenas andaba en aquel entonces. Pero Sun lo vendió como un producto terminado para Enterprise, y no lo era. Aparte había algunos eventos raros, que te pasaban la gente felíz en el jardín con un perrito diciendo "Ahora voy a programar en Java". Una cosa muy marquetinera pero que no era la realidad de la programación. Entonces hubo gente acá, en la Universidad del Salvador que quisieron hacer cosas en Java, y ahí adquirió algo de mala fama, porque era muy básico todavía (por ejemplo, no existía Swing, era AWT). En parte porque Java apareció para hacer Applets, y Sun lo quiso posicionar para otro mercado, y todavía no estaba muy armado. Entonces ahí ellos reaccionan a final de los años 90 e impusieron todo lo que es J2EE. Dijeron, "bueno, vamos a hacer Java para algo mejor, más para negocio, para empresas" pero todavía no estaba listo, ni siquiera había transacciones! Por eso falló. Otra cosa que hicieron mal fue que se dedicaron a vender Solaris, y a Java nunca lo tomaron en serio. Cuando organizaban eventos y demás era todo para Solaris, para Java no había nada. Recién a principios de este siglo Sun empieza a cambiar un poco y se da cuenta que tiene que atender a la comunidad.

**Santiago**: ¿Cómo nace el apodo?

**Angel**: Por el BBS. El BBS de MPOnline te ponía como usuario las iniciales de tu nombre y el apellido. Entonces me quedaba "ajlopez", y como yo en los foros escribía de Java, alguien me dijo, "Ah, vos sos Angel Java Lopez".

**Santiago**: ¿Qué libros considerás importante para un programador? ¿Cuáles recordás de aquella época?

**Angel**: En aquella época venían muchas revistas. Sobre todo compraba la "Computer Language" que era americana, "Doctor Dobb" que era muy buena, y estaba la "Byte" que tenía bastante información sobre programación, sobre todo de hardware, aunque yo lo de hardware no lo veía tanto. Había una también que se llamaba "Tech Journal" donde había muchos temas comerciales, pero también de programación de PCs.

Había una consulta en linea que se llamaba "Dialog", que era como una base de datos a la que le podías hacer consultas, y algunos nodos de las universidades tenían conexión con Dialog. De alguna forma ahí, por abajo, ya había internet, o algo parecido. Aunque era solamente para académicos.

Los libros eran difíciles de conseguir. Las librerías trabajaban solamente libros en español. No existía Cúspide, y El Ateneo no traía cosas en inglés ni a pedido. Había una librería en Tucumán, cerca de 9 de Julio, en un primer piso, que se llamaba American Books, ahí se podían ir a buscar libros en inglés o pedirlos, pero tardaban 6 meses. Entre los libros que recuerdo habían varios tecnológicos, tipo Turbo C, Turbo Pascal, apareció al final de los 80 uno para programar en Windows. Había uno muy interesante que se llamaba "Programmers at work", que la traducción era "Programadores en acción" y también otro en español que es "Fuego en el valle" que era toda la historia de la movida de la PC. Cómo se creo el primer chip, como pasaron de 4 bits a 8 bits, etc.

Lo que me quedó de ese libro es que mucha de esa gente se habían conocido en lo que se llamaban los clubes "Homebrew", que eran clubes de aficionados que empezaban a intercambiar cosas. Todo eso me gustó y cuando acá en el año 95 apaerció el club Byte, el MUG y todo lo demás, fue cuando yo me prendí. Antes del 95 no había ese tipo de grupos.

**Santiago**: ¿Qué usas para programar? ¿Qué le recomendarías a cualquier programador?

**Angel**: TDD. Cualquier tipo de código de producción tiene que estar hecho con TDD. Después recomiendo siempre aprender dos tipos de lenguajes. Uno de tipado estático, tipo Java o C#, y uno de tipado dinámico, tipo Ruby, Python o Javascript. El IDE ya no es tan importante. Tal vez sí para los de tipado estático, pero hay mucha gente que sigue usando Vim.

Si haces TDD, el mismo TDD te va creando baby steps y no tenés que estar con cuatro ojos mirando todo lo que pasa en el programa. Lo que es útil de algunos IDEs es la completación de código, aunque en algunos lenguajes no se puede completar todo. Ninja IDE tiene autocompletado, que deduce de los imports, eso está bueno.

Cuanto más grande el sistema, y por lo tanto más complejo, más recomiendo TDD. O sea, ¿cómo se come un elefante? Pedacito a pedacito. Si no hacés TDD caes en la falacia de querer hacer arquitectura de algo complejo, cuando no es necesario.

**Santiago**: ¿Usás debugger?

**Angel**: No, con TDD casi no uso debugger. A lo mejor necesitás el debugger las primeras veces porque no sabés cómo funciona algo, pero después cuando te ponés canchero, a las dos semanas ya no necesitás debugger.

**Santiago**: ¿Cómo arrancás con los programas? ¿Te sentás con una hoja de papel una hora a planearlo, o vas directo al código?

**Angel**: Generlamente arranco a tirar código. Puede ser que alguna vez cuando desayuno escribo algo, pero sino me pongo a tirar código.

**Santiago**: ¿Y la legibilidad? ¿Preferís comentarios, variables y métodos largos, etc? ¿Usás `i`, `l`?

**Angel**: Arranco con `i`, `l` y después refactoreo. Pongo esos nombres para que ande, para que quede en verde, y después hago refactoring. Ahora, para un for `k=1` dejo `k`. Practicamente no uso comentarios. Si uso comentarios es porque algo raro hice. El nombre de la función tiene que ser lo bastante chico para que se entienda. Tal vez tengo algún comentario por clase. Pero hasta el nombre de la clase tiene que ser autodescriptivo.

**Santiago** ¿Lees código de otros?

**Angel**: Sí, porque a veces te pasan un proyecto y tenés que hacer code review. Enseguida te das cuenta cuando lo hicieron con TDD. Si no lo hicieron con TDD quedan muchas cosas, como yo las llamo, *convoluted*, o sea, están puestas por arquitectura, por patrones, pero a lo mejor no se necesitaban.

Cuando aprendes patrones no te tenés que olvidar que los patrones tienen un contexto. No hay que poner todos los patrones solo porque aparecen en los libros. Prefiero codificar sin patrones al principio y después aplicarlos a medida que son necesarios. Usarlos porque son necesarios, no solo porque se me ocurre usarlos.

**Santiago**: ¿Leiste "Patrones de Diseño", de GoF? ¿Lo recomendas?

**Angel**: Sí, pero en ese entonces no tenían TDD. En aquella época ellos decían "programá contra una interfaz", pero la gente lo entendió mal. "Programar contra una interfaz" significa asumir que un objeto tenga tales métodos, pero no que haya una interfaz como interfaz declarada. Muchos de los ejemplos de GoF son en Smalltalk, y Smalltalk no tenía interfaces.

**Santiago**: ¿Cuál es el bug más grande que te acuerdes?

**Angel**: Usando TDD ninguno. Me acuerdo uno que no es mío. Fue un bug histórico de un compilador de los años 80 (no recuerdo bien de qué), en el que autor (un ruso) refactorizó una rutina y lo hizo mal. Durante dos años nadie se dio cuenta porque nadie pasaba por ese lado. Y un día pasó alguien y fue un desastre. Eso es lo bueno de TDD. Nunca te va a dejar escribir algo que nadie usa.

**Santiago**: Hablaste de TDD. Los tests unitarios se basan en pequeñas aserciones y el uso de invariantes. Eso me lleva a la siguiente pregunta. ¿Es necesario la matemática u otras ciencias básicas para ser un buen programador?

**Angel**: No. Hay muchos programadores a los que no les gusta la matemática. Por ejemplo, el tema de invariantes apareció en un libro de Bertrand Meyer, "Construcción de Software orientado a objetos" donde él presentaba su lenguaje, Eiffel. En Eiffel es donde aparece ese concepto de la pre-condición y la post-condición y también los asserts y otras cosas. Lo que le faltaba a Eiffel eran los namespaces, porque a nadie se le había ocurrido en los años 80 la utilización de namespaces.

En esa época se movió mucho el tema de los lenguajes, porque el departamento de defensa de los Estados Unidos llamó a una licitación internacional para implementar un solo lenguaje en todos sus sistemas, que al final terminó ganando Ada de un profesor francés llamado Jean Ichbiah. El primer lenguaje en el que vi el tratamiento de excepciones fue en Ada, no recuerdo otro antes. Porque los militares querían saber que si pinchaba algo, explotase de una forma controlada.

Se cuenta que esa licitación (que era secreta), Niklaus Wirth perdió presentando el lenguaje Modula.

**Santiago**: Entonces no es necesaria la matemática, ¿qué hay de otras ciencias? ¿te sirvió alguna otra ciencia a la hora de programar?

**Angel**: Ojo, a mi la matemática me sirve. Lo que digo es que otros programadores pueden no necesitarla, pueden ser buenos programadores sin matemática.

Lo que me sirvió a mi es la capacidad de pensar ordenadamente y para mantener la concentración. En los 80 cuando iba a la facultad de ingeniería la carrera se llamaba Analista de Sistemas y había muchas mujeres, de hecho había mitad hombres y mitad mujeres. Pasa que era una carrera del punto de vista más organizacional, no había mucha programación. Era para armar análisis de sistemas en papel, organigramas, etc. Lo que vi ahí pasando los años, es que las mujeres se dedicaron más a la parte de análisis funcional y los hombres más a la programación. Siempre he observado eso. Y pienso que es en parte por el tema de la concentración. Los hombres tienen mayor poder de concentración, a diferencia de las mujeres que son más empáticas, tienen más facilidad para liderar grupos, etc. Sin ser sexista, son simplemente algunas diferencias que observo.

Sin embargo, en los últimos años gracias al TDD puedo hacer cosas sin la necesidad de concentrarme tanto. Puedo ir escribiendo tests chicos, hacer baby-steps, entrar al código, salir, volver a entrar.

**Santiago** Dado tu conocimiento, y tu experiencia. ¿Cómo lidiás con el día a día, con la gente que te pregunta cosas constantemente y atenta contra esa concentración?

**Angel**: Bueno, escribo posts. Jeje. Por eso escribo los posts, porque ya queda ahí. Hoy por ejemplo escribí uno sobre TDD basado en la experiencia de un proyecto, entonces lo discutí con la gente del proyecto y después lo pasé al post. De esa manera ya queda para la posteridad. Por eso también dejé de dar cursos. Lo que se pierde es la interacción con la gente, es como que estás en un pedestal, pero después con los meet-ups y las reuniones se genera esa interacción para conectarse más con la gente. Eso es algo que no se debería perder. Todo el mundo se reune, hasta los más capos. Es un tema que a veces se descuida, pero muchas veces termina siendo fundamental para el open-source. Porque los desarrolladores se terminan conociendo. Cuando la gente no se conoce, un mail mal interpretado, o una frase mal hecha puede generar fricción. Pero si ya te juntaste a tomar una cerveza, o compartiste una cena, podés mandar cualquier cosa y se recibe de otra forma.

**Santiago**: Hablaste bastante de TDD pero no mencionaste al BDD. ¿Qué opinión tenés?

**Angel**: Todavía no llegué. Me interesa, pero no lo necesito. La mayoría de la gente ni siquiera hace TDD, y para mis proyectos personales que estoy solo me alcanza con TDD. Las cosas se adoptan en la medida que la gente las quiera adoptar, no se puede imponer.

**Santiago**: Contanos un poco de Microsoft, cómo es su relación con el Open Source y demás.

**Angel**: Bueno, ya desde el 2001 permitieron bajo el ECMA que nazca el proyecto Mono. Veo que Oracle le hace problemas a Google por Java, y Microsoft se comprometió a no hacer ese tipo de cosas con C#. Por eso también tuvo esa aceptación C#.

La amenaza que tuvo Microsoft en estos años fue principalmente Linux, en entornos de servidores web, que principalmente son servidores Apache corriendo sobre Linux. Pero al resto de la empresa no lo afectó. Por lo que estuve leyendo había cierta preocupción de que Linux creciera, pero realmente la batalla del desktop ya la ganaron. Hay empresas, o entidades del gobieron que han tratado de pasar a Linux, pero después de un tiempo volvieron a Microsoft. No estoy en contra del Open Source, al contrario, lo apoyo, pero algunas veces pagar una licencia te cuesta más barato que implementar Open Source.

En los últimos años, la amenaza de Microsoft está en Apple y en Google. En Apple con el mobile, el iphone, ipad, etc. El mercado de tablets está impulsado por Apple, y ahora Microsoft está tratando de entrar. Y en Google con el browser, con la idea de tener un app store dentro del browser. Está el movimiento de que el browser sea el sistema operativo.

El otro tema que creo que Microsoft no se lo esperó, es el surgimiento del cloud computing. Ahí Amazon está liderando, sobretodo por el precio, porque tal vez en cuanto a funcionalidad Microsoft está cada vez mejor, pero no puede bajar los precios.

**Santiago**: Ya que mencionás el cloud computing. ¿Lo usás? ¿Qué te parece?

**Angel**: No, yo no lo uso. Estoy asistiendo a los meet-ups del AWS User Group de Buenos Aires, así que si tuviera que usarlo optaría la plataforma de Amazon. Por lo poco que vi me parece mucho más fácil y mantenible. Aparte ha seguido un crecimiento más orgánico que Azure. Actualmente Azure va por la tercer interfaz web, en cambio AWS, fue más estable. Jeff Bezos insistió e insistió con que todo lo que habían hecho lo podían llegar a reutilizar y vender, y pasó de vender libros a liderar el mercado del cloud computing. Es una gran visión de Bezos.

Finalmente, por lo que está luchando Microsoft es por "las tres pantallas". La pantalla desktop, la pantalla mobile, y la Tv. La Tv va a ser el próximo campo de batalla. Y Microsoft se ha orientado mucho a consumo.

**Santiago**: ¿Programás para moviles?

**Angel**: No, ni siquiera tengo teléfono, pero voy a tener que ponerme más con eso. Igual pienso que lo que más fuerza va a tomar son las tablets. Al ser cada vez más livianas y al haber internet por todos lados, es ahí hacia donde se va a mover el mercado. Y esa es la gran movida de Microsoft con Windows 8, que está siendo usado en desktop, pero el principal objetivo fueron las tablets. Y lo hicieron así para que todos programemos para la misma plataforma de forma fácil, para que haya sinergia.

Ahora en este proyecto estamos emulando windows 8 para hacer una aplicación web. La idea de windows 8 es que sea más horizontal. Hacer que los programadores se muevan a eso. Incluso .Net empieza a desaparecer y surge con más fuerza HTML5 y Javascript, abandonan Silverlight, etc. Windows 8 es un giro para Microsoft hoy día, como lo fue en su momento .Net.

**Santiago**: Contanos un poco más del MUG (Microsoft User Group).

**Angel**: Ahora voy a hacer una charla de TDD y va a haber una charla por el día del programador. Está bueno el grupo. El tema tal vez es la edad, no va tanta gente joven. Hay más programadores de la década del 90.

**Santiago**: ¿Cuál es tu opinión sobre el Open Source?

**Angel**: Todo debería ser Open Source para el desarrollo. Incluso Visual Studio debería ser gratis. Es el único IDE popular que no es gratis. Como desarrolladores somos parte de la cadena, no el final. Las empresas que viven de los desarrolladores terminaron desapareciendo, como el caso de Borland. Microsoft debería ver eso, que todo lo que obtienen como ingreso debería venir de licencias, de juegos, etc. Acá en Argentina mucho tiempo los juegos significaron un gran ingreso. Se pirateaba mucho todo, pero los juegos era lo único que se compraba.

Igual hablo de que sea gratuito, no Open Source. Tal vez un IDE cerrado, gratuito, que sea extensible es conveniente. Por ejemplo, ¿cuánta gente contribuye al core de Eclipse? No muchos. Pero sí hay muchos plugins.

Ya ha cambiado el modelo de negocio, se basa en licencias de software de servidores, o licencias tipo freemium, dónde algunos productos son gratuitos pero para acceder a más características se cobra, vender los servicios, etc. Microsoft eso lo hace bien, con SkyDrive, hotmail (ahora Outlook). Eso en gran parte fue movido por Google.

Ahí aparece algo interesante relacionado con Google. Yo pienso que toda esta movida post-burbuja apareció gracias al modelo de la publicidad de Google. Al poder hacer dinero Google con la publicidad permitió que surja la Web 2.0. Todos los bloggeros por ejemplo pudieron obtener ingresos gracias a eso. Incluso Facebook fue posible gracias a eso, porque también vende publicidad. Antes todos esos ingresos tenían que ser por venta de licencias a los usuarios. Antes, para poner una publicidad tenías pocas opciones. Por ejemplo, para poner una publicidad en Yahoo! tenías que llenar un formulario, enviarlo a Yahoo! y que te respondan a los 6 meses diciéndote que como tu sitio era en español, y ellos no tenían publicidad en español, no podías publicar. Y Google rompió con todo eso, hizo posible ese tipo de negocio con la publicidad en internet. Democratizó e hizo factible, sin fricciones el comercio de la publicidad en Internet.

**Santiago**: Hablame un poco de Inteligencia Artificial. ¿Qué opinión tenés?

**Angel**: Es un tema muy amplio. Viví el auge de los sistemas expertos, al final de los años 70 y comienzo de los 80. Ahí hubieron éxitos y fracasos, y después hubo una especie de otoño de la inteligencia artificial (recuerdo un paper hablando de esto). La IA tuvo mucha inversión durante la guerra fría, se desarrolló mucho durante esa época. Hubo un caso negativo, el de la quinta generación de Japón a mediado de los años 80 dónde una de las cosas que quería hacer era implantar IA en varios proyectos con prolog. Los japoneses siempre venían adoptando nuevas cosas y haciéndolas generalmente bien, gracias también a la intervención estatal que había. Pero con la Inteligencia Artificial fracasaron.

**Santiago**: ¿Cuál es tu lenguaje preferido?

**Angel**: No hay uno específico. Voy pasando por etapas. Por ahora C# y Javascript. Javascript me parece más flexible y con menos ceremonia que Ruby o Python. Tiene su parte áspera, pero si la evitás es muy flexible. Y si trabajás con TDD podés hacer un montón de cosas incrementalmente y no te cuesta programarlo.

**Santiago**: Que no tengas un lenguaje predilecto me lleva a otra pregunta. ¿Cuál es el estado de la computación hoy día? ¿Por qué no estamos lo suficientemente avanzados para que haya una opción perfecta?

**Angel**: Nunca va a haber "El" lenguaje. Fijate que pasaron muchas décadas desde los primeros lenguajes de los años 50, y todavía siguen estando. Sobreviven lenguajes viejos y surgen nuevos. Sobrevive Smalltalk, sobrevive Cobol. Y en el medio de todo eso surge Python o surge Ruby. Y ahora con Internet hay aún más sinergia. Porque cuando surgió Python o surgió Ruby era más difícil apalancarlos. Ruby por ejemplo fue incubado en la empresa donde trabajaba Matz, no fue una incubación "muy internet". Eso cambió ahora.

Lo que no veo ahora es un sistema operativo de ese tipo. La industria de los sistemas operativos se quedó más estancada. Android por ejemplo lo tuvo que impulsar Google, no salió de una Facultad, como el caso de Linus en Finlandia. Las interfaces gráficas son un problema en ese caso. En Linux es muy común tener GTK o alguna otra, pero tampoco surgieron muchas, porque cuesta mucho hacerlas. Entonces, al final una triunfa y el resto programa encima. En fin, es más fácil programar un lenguaje que todos los widgets de una interfaz gráfica.

Otra cosa que aparece nueva, como un nuevo concepto, son las "Application Store" donde un programador puede programar algo y ponerlo en la App Store de Android o de Apple, etc. Incluso te resuelven el problema monetario porque hasta lo venden por vos. Te permite entrar más fácilmente al mercado, no hace falta que tengas una empresa o algo parecido para entrar.

**Santiago**: ¿Qué es un programador? ¿Un Ingeniero, un Artesano o un Artista?

Es un ingeniero y un artesano. La ciencia se ocupa de lo que "es", el ingeniero se ocupa de crear lo que no está. La ingeniería hace puentes, la ciencia se ocupa de estudiar las montañas, las piedras, los animales, por ejemplo. Después el ingeniero se encarga de crear.

Pero la programación sigue siendo algo artesanal. El movimiento ágil se encarga de que uno esté orgulloso del concepto de "Craftsmanship", el ser un artesano. Tener el orgullo ese de armar la Catedral, de que hasta la piedra más chiquita sea algo que contribuye al todo, a lo que se está armando. Y eso va a continuar por varios años más.

Un tema a investigar que a mi me interesa es el de los Sistemas Distribuídos, sistemas que corran en varias máquinas a la vez. Las supercomputadoras no prendieron, lo que sí fue exitoso fue el "scale-out". Es más fácil poner varias computadoras comunes a trabajar en un problema que armar o comprar una supercomputadora. Me acuerdo de un caso de una universidad que había contratado miles de instancias de AWS para correr un proceso de investigación 8 horas y les costó más barato que hacerlo en una sola computadora. Los sistemas distribuídos están cada vez más presentes, porque incluso nuestro cerebro procesa en distribuído.

Me preguntabas por los libros hace un rato. Ahora recuerdo uno inspirador para esto que estamos hablando que es "La sociedad de la Mente", de Marvin Minsky. Donde va desglosando y dice que nuestra mente funciona con varios agentes. Esos agentes fueron apareciendo a lo largo de la evolución, y que no es "una sola mente". Entonces eso sería bueno investigar. En vez de hacer un sistema que piense, o un solo programa, empezar a hacer agentes que colaboren para resolver un problema y que colaboren entre ellos. Que se puedan programar y agregar más, y que la comunidad pueda colaborar con otros agentes.

**Santiago**: Hoy hablábamos del tipado estático como una de las mejores herramientas a la hora de comprobar la coherencia de nuestro código. Es raro no ver que mejores herramientas hayan progresado a lo largo de los años. ¿Ves en el futuro a la IA del lado del programador, ayudándonos a escribir mejor código, mejores programas?

**Angel**: Yo tengo un proyecto, que es el **AJGenesis** que trata de ser un sistema experto, es decir, de *hacer sistemas*. Yo le voy enseñando cómo hacer el sistema, y él va haciéndolo. Obviamente, todavía es muy trivial lo que hace. Pero sobrevivió al cambio de tecnología y sigue funcionando. Es un tema interesante a investigar, para que la programación la pueda hacer la propia máquina. Pero por ahora hay mucho de artesanía.

Hay profesiones que desaparecieron a lo largo de la historia, que fueron reemplazadas por la tecnología. Por ejemplo, en el siglo 19 había un mercado muy grande de motores pero terminó desapareciendo cuando apareció el mercado de los automotores. Hoy no ves muchos negocios que vendan motores, la mayoría vende autos. Tal vez dentro de unos años nadie se acuerde de las PCs y sean todas tablets, es una posibilidad.

**Santiago**: ¿Qué es necesario para que eso suceda?

**Angel**: Tal vez otros lenguajes, para ir levantando el nivel. Por ejemplo, Visual Basic en los años 90 elevó el nivel, o las expectativas. O sea, no tenías que programar los botones a bajo nivel sino te daba abstracciones gráficas. Pero nunca apareció algo mejor que eso. Hay algunos intentos mejores pero nunca prendió algo completamente. Nosotros seguimos programando como en los años 70, en un archivo de texto vacío. Debería buscarse algo mejor, pero la verdad no se qué va a pasar con eso. La gente prefiere código. Es más, en los últimos años se volvió más aún al código. Ya no se quieren las configuraciónes con XML y todas esas cosas, ahora se prefiere código.

**Santiago**: No se por qué, pero de pronto me acordé de Hibernate.

**Angel**: Bueno, por ejemplo, ahora en NHibernate hay una opción de configuración desde el código, porque eso es lo que quiere la gente. Se prefiere configurar por código, para usar mejor TDD y poder utilizar herramientas de refactoring, que depender de un mapeo XML. Incluso en la parte gráfica se da esto. Ya no se prefiere arrastrar un botón a escribir el código. Hay un artículo que habla de lo "Simple vs. lo Fácil". Tal vez lo más *fácil* es arrastrar el botón, pero después la complejidad crece y termina emergiendo.

Eso también pasa en algunos momentos con frameworks como Ruby on Rails o Django. En un momento llega a ser todo tan fácil que es difícil customizarlo. Tal vez querés agregar algo que el framework no lo tiene y tenés que empezar a ahondar a bajo nivel y la complejidad aumenta significativamente.

**Santiago**: Te cambio de tema. ¿Cuál es el rol de la universidad?

**Angel**: A mi la universidad me sirvió para aprender a pensar. En general acá la secundaria, salvo alguna técnica, tiene un nivel muy bajo. No solo lo digo yo, he preguntado en mis viajes y todos coinciden. Por eso existe también el Ciclo básico en la UBA, o los cursos de ingreso, es la forma de nivelar. A mi también me pasó eso, yo me tuve que esforzar mucho en la universidad porque en la secundaria no me exigieron.

Ese es uno de los roles de la facultad, tensar al alumno. Por eso yo no creo que deban sacarse las materias de ciencias básicas (siempre está latente ese debate), porque son materias formativas que sirven para tensarte la neurona.

**Santiago**: En la universidad, ¿C o Python? ¿Es preferible bajo nivel o alto nivel?

**Angel**: No se. Ahora ha cambiado un poco. Pero hace unos años yo vivía del curso de Java porque en la universidad no se daba, estaban siempre atrasados. Ahora con el tema de Internet ha cambiado un poco. Aparte los estudiantes cada vez entra a trabajar antes también, y se chocan con el mundo real. Entonces hay más presión sobre los profesores, porque si están atrasados los estudiantes reaccionan con el conocimiento que tienen. En el 2000, 2001, con la crisis los cursos tenían mucho éxito, porque los chicos para irse a trabajar al exterior necesitaban aprender cosas nuevas, no les alcanzaba para encontrar un trabajo con lo que aprendían en la universidad.

**Santiago**: Siguiendo con el tema. ¿Es preferible trabajar, estudiar, ambas a la vez?

**Angel**: Si se puede, es preferible hacer ambas de forma conjunta. Tal vez ahora la universidad está más cerca de la realidad y entonces se podría aprovechar un poco más el estudio. En mi tiempo me sirvió mucho hacer las dos. La universidad para pensar y el trabajo para estar al día.

**Santiago**: ¿Qué se necesita para ser un buen programador?

**Angel**: Estar abierto a aprender. Siempre vas a aprender algo, ya que todo cambia. Y cada vez es más necesario saber trabajar en equipo, tener las llamadas "soft skills". Ya no hay sistemas que los pueda llevar a cabo una sola persona. Es importante participar en proyectos Open Source, o publicar proyectos propios para ir practicando la parte de código y las relaciones.

La mitad de tu currículum debería estar en GitHub. Hoy si tuviese que tomar a un programador me fijo eso. Primero si tiene algunas Soft Skills básicas y después el código. O sea, que haya hecho algo, por más que no sea buen código. Que muestre interés en la programación, que no haya salido derecho de la universidad a buscar trabajo sin haber tirado una linea.

**Santiago**: Entonces, en resumen, ¿qué le recomendás a un programador nuevo para que arranque?

**Angel**: Como te dije antes, que aprenda un lenguaje de tipado estático y uno de tipado dinámico. Además que aproveche las facilidades actuales para leer código de otros y para relacionarse. Yo hace mucho que no me compro un libro por ejemplo, todo cambia muy rápido. Salvo los libros formativos tipo "The Art of Computer Programming" de Donald Knuth (que son pocos), si te comprás un libro sobre alguna tecnología en particular, en dos años ya no sirve más.

**Santiago**: Muchas gracias Angel.

**Angel**: Gracias a vos.
