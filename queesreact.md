<h1>¿Qué es React JS?</h1>
<img src="./IMG/react.png">
<h3>React o ReactJS es un marco de JavaScript que permite a los desarrolladores crear interfaces de usuario de forma rápida y eficiente mediante la inclusión de archivos Java en su HTML. Es una de las bibliotecas de Java más populares del mundo y es utilizada por enormes plataformas como Netflix, Airbnb e incluso Walmart.ReactJS y su biblioteca Java permiten a los desarrolladores de software crear diferentes interfaces de usuario a través de varios componentes diferentes que ayudan a construir y definir la estructura completa de su aplicación.

 

ReactJS actúa como una parte visible de su aplicación web, lo que significa que administra datos simples, con la esperanza de permitirle saber cómo se verá su aplicación para el público y los usuarios finales.

 

En otras palabras, ReactJS es una interfaz de desarrollo front-end. React lo ayuda a mantener la interfaz de usuario organizada como si fuera un árbol, donde las raíces son los componentes de inicio y las ramas son partes independientes de la aplicación, de esta manera, cuando se cargan nuevos datos, puede ubicar su ubicación y actualizarse automáticamente.

 

Beneficios de usar ReactJS
 

ReactJS es bien conocido entre los desarrolladores de software por dos razones: una, es una interfaz de usuario confiable desarrollada por Facebook, y dos, permite a los ingenieros de software crear aplicaciones web y móviles.Entre los beneficios de usar ReactJS están:
 

1. Cree aplicaciones web y móviles: los componentes ReactJS se pueden usar para desarrollar aplicaciones móviles que se ejecutarán en sistemas móviles Android e iOS casi como si fueran aplicaciones nativas.

 

2. Permite la codificación estable: con ReactJS puede realizar pequeños cambios en la estructura secundaria de su aplicación sin que dichos cambios afecten a los padres y al resto de la estructura. Esto permite una codificación estable y un rendimiento continuo.

 

3. Le permite reutilizar componentes antiguos: React les da a los ingenieros de software la libertad de reutilizar componentes y activos viejos del sistema para mejorar su aplicación web o móvil, permitiéndole desplegar varios objetos digitales diferentes.

Si está pensando en crear una aplicación de software web simple, ReactJS es la tecnología perfecta para usted.

 

"React te ayuda a crear interfaces de usuario interactivas de forma sencilla. Diseña vistas simples para cada estado en tu aplicación, y React se encargará de actualizar y renderizar de manera eficiente los componentes correctos cuando los datos cambien", explicaron los creadores de ReactJS en su website.

 

Lo mejor es que los ingenieros podrán "desarrollar nuevas características sin necesidad de volver a escribir el código existente". Así mismo, React permite interactuar con otras bibliotecas y frameworks para enriquecer los proyectos.
</h3>
<h1>Estructura del proyecto </h1>
<h2>
Es bastante usual que un proyecto de React conste de varias decenas (e incluso centenas) de archivos, por lo que tener una buena organización de los mismos es fundamental. React no nos dice ni nos obliga a ordernarlos de cierta manera, por lo que, en proyectos personales, tenemos que buscar un criterio con el que nos sintamos cómodas. Hay una sugerencia bastante conocidad en el ámbito que dice: mueve cosas hasta que se sientan bien.

De todas formas, hay un par de sugerencias a tener en cuenta. Los lineamientos principales o que deberíamos tener presentes son básicamente dos:

la estructura del proyecto debería informarmos inmediatamente de las cosas que contiene con solo mirarlo (esto se conoce como "screaming architectura").
no debería haber carpetas anidadas con muchos niveles de profundidad (es decir, muchas carpetas dentro de carpetas dentro de carpetas). Es preferible una estructura más horizontal (todo a un mismo nivel) que vertical (o jerárquica).
Todos los archivos con los que trabajemos van a ir dentro de la carpeta src. Dentro de esta, una estructura mínima podría tener las carpetas:

components
assets
styles
En components van a ir todos nuestros componentes, en assets aquellos archivos como ímagenes, íconos, fuentes, etc (podemos subdividirlos en categorías, y si tenemos muchas, subdivir estas) y en styles todos aquellos estilos genéricos que no pertenezcan a un componente en particular.

Dentro de components vamos a crear una carpeta por cada componente, con nombre en PascalCase, como el mismo nombre del componente, y dentro de esto vamos a crear al menos un archivo .js para el componente, y un archivo .scss para los estilos, también con el mismo nombre. Por ejemplo, si nuestro componente se llama Comment, nos quedaría:

src
components
Comment
Comment.js
Comment.scss
En primera instancia ponemos todos los componentes bajo la carpeta components, a un mismo nivel. En caso de que luego la cantidad de componentes empiece a crecer, podemos empezar a agruparlos dentro de subcarpetas. Básicamente, los criterios para agrupar componentes son dos:

Componentes de un mismo tipo: buttons, modals, popups, menus
Componentes que pertenezcan a una misma unidad o componente mayor: CommentText, CommentDate, CommentUsername, etc
Dentro de styles vamos a incluir archivos .scss que van a ser luego importados en los archivos .scss de los componentes. Estos archivos tienen por lo general estilos generales o variables que se utilizan en todo el proyecto. Como tienen que ser importados, son archivos parciales, por lo que tienen que comenzar su nombre con guión bajo. Es preferible tener varios archivos (por ejemplo, uno para variables de colores, otro para variables de fuentes, etc), a un único archivo gigante. A su vez, en el caso de tener varios, también podemos agruparlos en subcarpetas si lo consideramos necesario.

</h2>