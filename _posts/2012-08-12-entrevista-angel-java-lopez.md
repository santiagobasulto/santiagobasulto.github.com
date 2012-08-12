---
layout: post
title: "Entrevista con Angel Java Lopez"
category: entrevistas
tags: programacion entrevistas programadores
published: false
---

<!--
00:25-07:00: ¿Cómo arrancaste? ¿Cómo era la computación y la programación en la época?*
07:00-09:00: ¿Cómo era la facultad en esa época?*
09:00-10:00: ¿Cuál fue el primer programa que escribiste?*
10:00-10:30: Revistas*
10:30-12:00: lenguajes en la facultad*
12:00-12:40: Mentores + Smalltalk*
12:40-13:30: Smalltalk*
14:40-16:50: Macs, apple. (¿Programaste para apple?)*
16:50-18:00: Visual basic vs C vs clipper (¿Cuáles eran los lenguajes más presentes?)*
	22:40-24:30: Turbo Pascal*
	24:30-25:00: Turbo C*
18:00-20:00: Hojas de cálculo. (Cambio de caracter a gráfico)*
20:30-20:50: Movimiento Unix en arg.*
20:50-21:30: Comienzo de la red en arg.*
25:00-26:05: ¿Cómo fue el comienzo de la era internet?*
26:05-29:55: Java*
	26:30-27:00: Apodo
	28:20-29:00: Sun
	29:10-: Solaris
29:55-: Libros y revistas*
37:30-39:50: Recomendaciones Programación. TDD. Tipado.
	40:20-41:00: TDD

39:50-40:20: Cómo arrancás a tirar código?
41:40-42:30: Legibilidad. i, j, k. Comentarios.
42:30-44:00: Leer código ajeno.
45:50-46:10: Bug.
46:10-: Equipo usa TDD?
47:12-: Cs básicas. Es necesario saber algo para usar invariantes?
	47:50-: Eiffel
	50:45- : Le sirve personalmente, pero no lo ve necesario.
51:00-: Diferencia entre hombres y mujeres.
-->


**Santiago**: ¿Cómo arrancaste con la programación?

**Angel**: Yo arranqué en la UBA, en la facultad de Ingeniería, si bien antes ya había arrancado en algunos institutos. En ese entonces no había computadoras personales, había que programar en papel. Eso era cerca del año 78.

**Santiago**: ¿Era el nacimiento de la computación en Argentina?

**Angel**: Acá sí. En otros lugares no. Por ejemplo, Microsoft ya había sido fundada. Pero acá no se sabía lo que era una computadora personal. Era todo Cobol, assembler de IBM 360, etc.

En el 80, cuando entré a la facultad de ingeniería se hacía todo con tarjetas perforadas, no tocabas la computadora. Había una IBM 360 que estaba en el cuarto piso encerrada. No había otras opciones (como comprar algo para tu casa, o en algún otro lado).

En el 81 un ayudante me convocó para una consultora y ahí arranqué a hacer más programación, y ahí vi empresas que tenían mini computadoras, o una computadora con varias terminales. En esa época empezaban a aparecer algunas micro coputadoras, que ocupaban el tamaño de una heladera de quiosco.

**Santiago**: ¿Cómo era programar en esa época?

**Angel**: Era difícil. Cuando mandabas a compilar algo te podías ir a tomar un café y volver y todavía no había terminado. Cada productor de hardware tenía su propio Sistema Operativo y su propio lenguaje. Eran principalmente mercados verticales, no estaba el concepto de un mercado horizontal.

Solamente en el ambiente académico había Unix, pero acá no había mucho. Habían varios proveedores, cada uno con su lenguaje y sistema operativo. Me acuerdo de *Ohio Scientific*, *Cromemco*, entre otras.

**Santiago**: ¿Qué clientes había?

**Angel**: De todo. Fábricas, gobierno, etc. Me acuerdo los sistemas de sueldos, que en aquel entonces cambió la forma de calcular el aguinaldo, que debía calcularse de forma proporcional a los meses que se habían trabajado, y hubo que cambiar todos los sistemas, porque antes no hacía falta guardar memoria de los sueldos anteriores. Con el cambio, empezó a ser necesario guardar la información de los sueldos. Usábamos diskettes, entonces la forma para calcularlo era: poner el diskette de Enero, apretar Enter, sacalo el diskette de Enero, poner el diskette de Febrero, apretá Enter, y así sucesivamente.

Había mucho cintas continuas, y era común pasear de un lado para el otro con las cintas. En esa época hicimos algunos sistemas para el gobierno militar, que después fueron exportados a Italia o Francia.

Ya apartir del año 81 empezaron a llegar las primeras PCs, de la mano de IBM. Lo que hizo IBM bien en ese momento fue permitir la expansión del hardware de las PC con componentes de distintos fabricantes. Contrariamente a lo que hacían con sus Mainframes. En los mainframes no se podía cambiar nada sin romper la garantía, incluso si fabricabas algo podías ser demandado. IBM distribuía dos sistemas operativos, uno llamado UCSD Pascal, y el otro era PC-DOS. En el año 85 recuerdo haber booteado algún Xenix, que era una versión de Unix hecha por Microsoft, que eran como 12 diskettes y necesitabas cargarlos todos para bootear. Encima, las máquinas venían con una sola disketera, entonces necesitabas bootear con un diskette, sacarlo, y cargar otro diskette con el editor.

**Santiago**: ¿Cómo era el ambiente en la facultad en esa época?

**Angel**: En la facultad había bastante movimiento. Habían dos opciones, la UTN creo que apareció cerca del año 79. En la UBA la carrera era Analista de Sistemas. Era bastante variado, había materias en las que se programaba y en otras que no. Pero se hacía todo con tarjetas perforadas. No se usaban PCs en la universidad (aunque ya estuviesen en el mercado). Entonces dejabas tu trabajo con tarjetas peforadas el miércoles y al otro miércoles tenías el resultado. Un ejercicio como ordenar un vector te podía llevar un cuatrimestre. Lo más problemático de todo eso era perforar las tarjetas, porque había solo dos perforadoras en la facultad. Entonces había servicios alrededor de la facultad que las perforaban, porque en la facultad había colas de media cuadra para perforar.

Entonces en el 81, cuando me senté en una PC, que tenía un editor para mi solo, estuve dos días seguidos programando. Arranqué el viernes a la noche y me sacaron el lunes a la mañana. Estaba bárbaro, editabas en el mismo lugar. Eran editores de linea! pero para mi era fantástico. Veías las letras ahí en la pantalla fosforecente y podías compilar y probar en el momento.

En segundo año ya se arrancaba más de lleno con programación. El primer año era bastante filtro, era mucho assembler. En segundo ya se arrancaba con ALGOL W, y algunos otros lenguajes. Había uno interesante que se llamaba BCPL, que era bastante sencillo, y a su vez permitía implementar BCPL, en el mismo BCPL. Entonces se hacía muy fácil migrarlo a diferentes arquitecturas.

**Santiago**: ¿Cuál fue el primer programa que escribiste?

**Angel**: El primero lo hice en papel, era un programa para calcular una jugada de Jaque Mate en dos movidas en Cobol. Tardé como dos años en correrlo, porque no tenía forma de correrlo

**Santiago**: ¿Anduvo?

**Angel**: Más o menos, no tenía recursión Cobol en aquel entonces. Por eso lo hice solamente en dos jugadas.

Después ya arranqué con las cosas que hago hoy, escribir intérpretes de pequeños lenguajes, que me puso más canchero en la parte de programación.

**Santiago**: ¿Qué profesores/mentores recordás de aquella época?

**Angel**: Había mucha gente brillante. Recuerdo puntualmente al Ingeniero Guido Vasallo, que en programación 4 nos enseñó mucho de lenguajes. Todos los sábados a la mañana  me tomaba el 22 desde Quilmes Oeste, y me bajaba en la facultad. Entonces todos los sábados de 8 a 1 te daba un lenguaje diferente, por ejemplo un sábado veías Prolog, al otro Lisp, etc. Una vez me lo crucé en una clase y le pregunté qué lenguaje nuevo podía aprender, y él me sugirió Smalltalk.

El problema era que no pude usar mucho Smalltalk, como algunos Lisp, porque estaban orientados a terminales gráficas, y acá los monitores gráficos eran muy caros. Me acuerdo de las plaquetas Hércules, muy populares en la época, que eran gráficas monocromáticas, porque el color era muy caro. Incluso, las de "color", tenían solamente 4 colores. Entonces Smalltalk quedó medio relegado, por las posiblidades que teníamos.

**Santiago**: ¿Te acordas de las primeras Macs?

**Angel**: Sí, pero tampoco programábamos mucho en Macs. Eran muy caras. Las PCs eran mucho más baratas. Recuerdo cuando apareció la Lisa, que ya venía con Mouse, y tenían interfaz gráfica monocromática. También pasaba que en su tiempo, para poder desarrollar en Apple tenías que firmar un contrato y unos libros. En esa época la comunicación era más difícil. Contactar a alguien internacionalmente era muy difícil. Incluso después de pedir todos los permisos tampoco te aseguraban que lo puedas conseguir, entonces la mayoría programaba para PCs. Tampoco había mucho mercado. De todas formas recuerdo gente que programó algún sistema para restaurants en Mac, pero después terminó migrándolo a PCs porque tenían más mercado.

**Santiago**: ¿Cuáles eran los lenguajes dominantes de la época?

**Angel**: Habían muchos. Recuerdo la movida que hizo Microsoft. Porque en los inicios de Windows se programaba todo en C, pero al tiempo largaron Visual Basic. Visual Basic en los 90 llevó la programación gráfica a las masas. Programar en C era muy complicado, quedó relegado para hacer programas específicos que necesitaban mucha terminación.

Clipper apareció al final de los 80, con el Clipper Summer 87, que hacía mucho más fácil programar para DOS que en C u otro lenguaje. Fue muy popular pero le costó hacer el cambio a la programación gráfica, como le pasó a Lotus 1-2-3 y a Quattro Pro.

Es muy interesante la historia de Turbo Pascal. En los 80, Borland compra una empresa europea que distribuía un compilador de Pascal, y el fundador de esa empresa era Anders Hejlsberg, que ahora es el principal arquitecto de .Net. Entonces cuando Borland compra la empresa de Hejlsberg, él se suma y crean Turbo Pascal, que después pasa a Delphi, y Object Pascal, entre otros.
Lo interesante de Turbo Pascal era el IDE, con un muy buen editor y debugger, que tenía inspección de variables, step-by-step, etc, que no era común en la época.

También estaba el Turbo C, que yo lo usé bastante y era muy lindo. En ese momento ocurrió algo curioso. La curva de complejidad y los precios fueron bajando. Se podía comprar en la calle Viamonte el Turbo C por cien dólares. Hasta que apareció Windows y nuevamente subió el costo de todo.

**Santiago**: ¿Y Unix? ¿Qué te acordás de esos años?

**Angel**: Lo que pasaba acá en Argentina, en el año 85 más o menos, era que las computadoras seguían siendo muy caras. Era posible acceder a una PC, pero era una tecnología costosa. Las empresas que necesitaban cargar datos tenían que comprar varias PCs, y no era económico. Entonces hubo un tiempo en que surgió Unix, con la idea de tener varias terminales bobas adelante de una sola computadora que corría Unix. Pero curiosamente, entre el año 85 y el 86 explotó lo que se venía gestando, que era la Red. Apareció la plaqueta Lantastic, después apareció Novell, e hizo fácil agregar una plaqueta y conectar varias PCs, y tener computadoras más poderosas y más económicas.

Aparte era bastante difícil programar para Unix. Entonces, Unix tuvo su ventana, pero lo terminó tapando la PC y la red.

**Santiago**: ¿Qué te acordás de los comienzos de Internet?

**Angel**: Empecé a navegar por algunos BBSs como MPOnline. Desués apareció algún Netscape o algún Internet Explorer, que eran de 16 bits. Cuando tenías que bajar una imagen tenías que esperar que termine de cargar la imagen para que siga cargando la página, porque eran monothread.

Ahí era cuando conocí Java.

**Santiago**: Contanos un poco más de Java.

**Angel**: Comencé en el año 95. Fue muy importante Internet, porque te lo podías bajar y compilar gratis. En el año 97 escribí un libro para MP Ediciones de Java. Java prendió mucho, pero el problema era que Sun vendió más de lo que tenía que vender. Por ejemplo, JDBC apenas andaba en aquel entonces. Pero Sun lo vendió como un producto terminado para Enterprise, y no lo era. Aparte había algunos eventos raros, que te pasaban la gente felíz en el jardín con un perrito diciendo "Ahora voy a programar en Java". Una cosa muy marquetinera pero que no era la realidad de la programación. Entonces hubo gente acá, en la Universidad del Salvador que quisieron hacer cosas en Java, y ahí adquirió algo de mala fama, porque era muy básico todavía (por ejemplo, no existía Swing, era AWT). En parte porque Java apareció para hacer Applets, y Sun lo quiso posicionar para otro mercado, y todavía no estaba muy armado. Entonces ahí ellos reaccionan a final de los años 90 e imponen todo lo que es J2EE. Dijeron, "bueno, vamos a hacer Java para algo mejor, más para negocio, para empresas" pero todavía no habían transacciones. Por eso falló. Otra cosa que hicieron mal fue que se dedicaron a vender solaris, y a Java nunca lo tomaron en serio. Cuando organizaban eventos y demás era todo para Solaris, para Java no había nada. Recién a principios de este siglo Sun empieza a cambiar un poco y se da cuenta que tiene que atender a la comunidad.

**Santiago**: ¿Cómo nace el apodo?

**Angel**: Por el BBS. El BBS de MPOnline te ponía como usuario las iniciales de tu nombre y el apellido. Entonces me quedaba "ajlopez", y como yo en los foros escribía de Java, alguien me dijo, "Ah, vos sos Angel Java Lopez".

**Santiago**: ¿Qué libros considerás importante para un programador? ¿Cuáles recordás de aquella época?

**Angel**: En aquella época venían muchas revistas. Sobre todo compraba la "Computer Language" que era americana, "Doctor Dobb" que era muy buena, y estaba la "Byte" que tenía bastante información sobre programación, sobre todo de hardware, aunque yo lo de hardware no lo veía tanto. Había una también que se llamaba "Tech Journal" donde había muchos temas comerciales, pero también de programación de PCs.

Había una consulta en linea que se llamaba "Dialog", que era como una base de datos a la que le podías hacer consultas, y algunos nodos de las universidades tenían conexión con Dialog, ahí, por abajo, ya había internet, o algo parecido. Aunque era solamente para académicos.

Los libros eran difíciles de conseguir. Las librerías trabajaban solamente libros en español. No existía Cúspide, y El Ateneo no traía cosas en inglés ni a pedido. Había una librería en Tucumán, cerca de 9 de Julio, en un primer piso, que se llamaba American Books, ahí se podían ir a buscar libros en inglés o pedirlos, pero tardaban 6 meses. Entre los libros que recuerdo habían varios tecnológicos, tipo Turbo C, Turbo Pascal, apareció al final de los 80 uno para programar en Windows. Había uno muy interesante que se llamaba "Programmers at work", que la traducción era "Programadores en acción" y también otro en español que es "Fuego en el valle", que era toda la historia de la movida de la PC. Cómo se creo el primer chip, como pasaron de 4 bits a 8 bits, etc.

Lo que me quedó de ese libro es que mucha de esa gente se habían conocido en lo que se llamaban los clubes "Homebrew", que eran clubes de aficionados que empezaban a intercambiar cosas. Todo eso me gustó, y cuando acá en el año 95 apaerció el club Byte, el MUG y todo lo demás, fue cuando yo me prendí. Antes del 95 no había ese tipo de grupos.

**Santiago**: ¿Qué usas para programar? ¿Qué le recomendarías a cualquier programador?

**Angel**: TDD. Cualquier tipo de código de producción tiene que estar hecho con TDD. Después recomiendo siempre aprender dos tipos de lenguaje. Uno de tipado estático, tipo Java o C#, y uno de tipado dinámico, tipo Ruby, Python o Javascript. El IDE ya no es tan importante. Tal vez sí para los de tipado estático, pero hay mucha gente que sigue usando Vim.

Si haces TDD, el mismo TDD te va creando baby steps y no tenés que estar con cuatro ojos mirando todo lo que pasa en el programa. Lo que es útil de algunos IDEs es la completación de código, aunque en algunos lenguajes no se puede completar todo. Ninja IDE tiene autocompletado, que deduce de los imports, eso está bueno.

Cuanto más grande el sistema, y por lo tanto más complejo, más recomiendo TDD. O sea, ¿cómo se come un elefante? Pedacito a pedacito. Si no hacés TDD caes en la falacia de querer hacer arquitectura de algo complejo, cuando no es necesario.

**Santiago**: ¿Usás debugger?

**Angel**: No, con TDD casi no uso debugger. A lo mejor necesitás el debugger las primeras veces porque no sabés cómo funciona algo, pero después cuando te ponés canchero, a las dos semanas ya no necesitás debugger.

**Santiago**: ¿Cómo arrancás con los programas? ¿Te sentás con una hoja de papel una hora a planearlo, o vas directo al código?

**Angel**: Generlamente arranco a tirar código. Puede ser que alguna vez cuando desayuno escribo algo, pero sino me pongo a tirar código.

**Santiago**: ¿Y la legibilidad? ¿Preferís comentarios, variables y métodos largos, etc? ¿Usás `i`, `l`?

**Angel**: Arranco con `i`, `l` y después refactoreo. Pongo esos nombres para que ande, para que quede en verde, y después hago refactoring. Ahora, para un for `k=1` dejo `k`. Practicamente no uso comentarios. Si uso comentarios es porque algo raro hice. El nombre de la función, tiene que ser lo bastante chico para que se entienda. Tal vez tengo algún comentario por clase. Pero hasta el nombre de la clase tiene que ser autodescriptivo.

**Santiago** ¿Lees código de otros?

**Angel**: Sí, porque a veces te pasan un proyecto y tenés que hacer code review. Enseguida te das cuenta cuando lo hicieron con TDD. Si no lo hicieron con TDD quedan muchas cosas, como yo las llamo, *convoluted*, o sea, están puestas por arquitectura, por patrones, pero a lo mejor no se necesitaban.

Cuando aprendes patrones, no te tenés que olvidar que los patrones tienen un contexto. No hay que poner todos los patrones solo porque aparecen en los libros. Prefiero codificar sin patrones al principio, y después aplicarlos a medida que son necesarios. Usarlos porque son necesarios, no solo porque se me ocurre usarlos.

**Santiago**: ¿Leiste "Patrones de Diseño", de GoF?

**Angel**:


