<h1>IF - Funciones de control de flujo </h1>
<h3>Trabajamos con las tablas "libros" de una librería.

No nos interesa el precio exacto de cada libro, sino si el precio es menor o mayor a $50. Podemos utilizar estas sentencias:

 select titulo from libros
  where precio<50;

 select titulo from libros
  where precio >=50;
En la primera sentencia mostramos los libros con precio menor a 50 y en la segunda los demás.

También podemos usar la función "if".

"if" es una función a la cual se le envían 3 argumentos: el segundo y tercer argumento corresponden a los valores que retornará en caso que el primer argumento (una expresión de comparación) sea "verdadero" o "falso"; es decir, si el primer argumento es verdadero, retorna el segundo argumento, sino retorna el tercero.

Veamos el ejemplo:

 select titulo,
  if (precio>50,'caro','economico')
  from libros;
Si el precio del libro es mayor a 50 (primer argumento del "if"), coloca "caro" (segundo argumento del "if"), en caso contrario coloca "economico" (tercer argumento del "if").

Veamos otros ejemplos.

Queremos mostrar los nombres de los autores y la cantidad de libros de cada uno de ellos; para ello especificamos el nombre del campo a mostrar ("autor"), contamos los libros con "autor" conocido con la función "count()" y agrupamos por nombre de autor:

 select autor, count(*)
  from libros
  group by autor;
El resultado nos muestra cada autor y la cantidad de libros de cada uno de ellos. Si solamente queremos mostrar los autores que tienen más de 1 libro, es decir, la cantidad mayor a 1, podemos usar esta sentencia:

 select autor, count(*)
  from libros
  group by autor
  having count(*)>1;
Pero si no queremos la cantidad exacta sino solamente saber si cada autor tiene más de 1 libro, podemos usar "if":

 select autor,
  if (count(*)>1,'Más de 1','1')
  from libros
  group by autor;
Si la cantidad de libros de cada autor es mayor a 1 (primer argumento del "if"), coloca "Más de 1" (segundo argumento del "if"), en caso contrario coloca "1" (tercer argumento del "if").

Queremos saber si la cantidad de libros por editorial supera los 4 o no:

 select editorial,
  if (count(*)>4,'5 o más','menos de 5') as cantidad
  from libros
  group by editorial
  order by cantidad;
Si la cantidad de libros de cada editorial es mayor a 4 (primer argumento del "if"), coloca "5 o más" (segundo argumento del "if"), en caso contrario coloca "menos de 5" (tercer argumento del "if").

Servidor de MySQL instalado en forma local.
Ingresemos al programa "Workbench" y ejecutemos el siguiente bloque de instrucciones SQL:

drop table if exists libros;

create table libros(
  codigo int unsigned auto_increment,
  titulo varchar(40) not null,
  autor varchar(30),
  editorial varchar(30),
  precio decimal(5,2) unsigned,
  primary key (codigo)
 );

insert into libros (titulo, autor,editorial,precio)
  values('Alicia en el pais de las maravillas','Lewis Carroll','Paidos',50.5);
insert into libros (titulo, autor,editorial,precio)
  values('Alicia a traves del espejo','Lewis Carroll','Emece',25);
insert into libros (titulo, autor,editorial,precio) 
  values('El aleph','Borges','Paidos',15);
insert into libros (titulo, autor,editorial,precio)
  values('Matemática estas ahi','Paenza','Paidos',10);
insert into libros (titulo, autor,editorial)
  values('Antologia','Borges','Paidos');
insert into libros (titulo, editorial)
  values('El gato con botas','Paidos');
insert into libros (titulo, autor,editorial,precio)
  values('Martin Fierro','Jose Hernandez','Emece',90);

select titulo from libros
  where precio<50;

select titulo from libros
  where precio >=50;

select titulo,
  if(precio>50,'caro','economico')
  from libros;

select autor, count(*)
  from libros
  group by autor;

select autor, count(*)
  from libros
  group by autor
  having count(*)>1;

-- mostrar cada autor y un mensaje si tiene 1 o más de un libro
select autor,
  if (count(*)>1,'Más de 1','1')
  from libros
  group by autor;

select autor,
  if (count(*)>1,'Más de 1','1') as cantidad
  from libros
  group by autor
  order by cantidad;

select editorial,
  if (count(*)>4,'5 o más','menos de 5') as cantidad
  from libros
  group by editorial
  order by cantidad; </h3>

  <img src="../Arbi/preguntas-if.png ">