<h1>Indice único (unique) </h1>
<h3>Veamos el otro tipo de índice, único. Un índice único se crea con "unique", los valores deben ser únicos y diferentes, aparece un mensaje de error si intentamos agregar un registro con un valor ya existente. Permite valores nulos y pueden definirse varios por tabla. Podemos darle un nombre, si no se lo damos, se coloca uno por defecto.

Vamos a trabajar con nuestra tabla "libros".

Crearemos dos índices únicos, uno por un solo campo y otro multicolumna:

 create table libros(
  codigo int unsigned auto_increment,
  titulo varchar(40) not null,
  autor varchar(30),
  editorial varchar(15),
  unique i_codigo(codigo),
  unique i_tituloeditorial (titulo,editorial)
 );
Luego de la definición de los campos colocamos "unique" seguido del nombre que le damos y entre paréntesis el o los campos por los cuales se indexará dicho índice.

"show index" muestra la estructura de los índices:

 show index from libros;
RESUMEN: Hay 3 tipos de índices con las siguientes características:


Tipo		Nombre			Palabra clave	Valores únicos	Acepta null	Cantidad por tabla
___________________________________________________________________________________________________________
clave primaria	PRIMARY			no		Si		No		1
común		darlo o por defecto	"index" o "key"	No		Si		varios
único		darlo o por defecto	"unique"	Si		Si		varios
Servidor de MySQL instalado en forma local.
Ingresemos al programa "Workbench" y ejecutemos el siguiente bloque de instrucciones SQL donde creamos dos índices únicos:

drop table if exists libros;

create table libros(
  codigo int unsigned auto_increment,
  titulo varchar(40) not null,
  autor varchar(30),
  editorial varchar(15),
  unique i_codigo (codigo),
  unique i_tituloeditorial (titulo,editorial)
);

show index from libros;
Genera una salida similar a esta:</h3>