
<h1> JOIN</h1>
<h3>hemos trabajado con una sola tabla, pero en general, se trabaja con varias tablas.

Para evitar la repetición de datos y ocupar menos espacio, se separa la información en varias tablas. Cada tabla tendrá parte de la información total que queremos registrar.

Por ejemplo, los datos de nuestra tabla "libros" podrían separarse en 2 tablas, una "libros" y otra "editoriales" que guardará la información de las editoriales. En nuestra tabla "libros" haremos referencia a la editorial colocando un código que la identifique. Veamos:

 create table libros(
  codigo int unsigned auto_increment,
  titulo varchar(40) not null,
  autor varchar(30) not null default 'Desconocido',
  codigoeditorial tinyint unsigned not null,
  precio decimal(5,2) unsigned,
  cantidad smallint unsigned default 0,
  primary key (codigo)
 );

 create table editoriales(
  codigo tinyint unsigned auto_increment,
  nombre varchar(20) not null,
  direccion varchar(30) not null,
  primary key(codigo)
 );
De este modo, evitamos almacenar tantas veces los nombres de las editoriales y su dirección en la tabla "libros" y guardamos el nombre y su dirección en la tabla "editoriales"; para indicar la editorial de cada libro agregamos un campo referente al código de la editorial en la tabla "libros" y en "editoriales".

Al recuperar los datos de los libros:

 select * from libros;
vemos que en el campo "codigoeditorial" aparece el código, pero no sabemos el nombre de la editorial. Para obtener los datos de cada libro, incluyendo el nombre de la editorial y su dirección, necesitamos consultar ambas tablas, traer información de las dos.

Cuando obtenemos información de más de una tabla decimos que hacemos un "join" (unión). Veamos un ejemplo:

 select * from libros
  join editoriales
  on libros.codigoeditorial=editoriales.codigo;
Analicemos la consulta anterior.

Indicamos el nombre de la tabla luego del "from" ("libros"), unimos esa tabla con "join" y el nombre de la otra tabla ("editoriales"), luego especificamos la condición para enlazarlas con "on", es decir, el campo por el cual se combinarán. "on" hace coincidir registros de las dos tablas basándose en el valor de algún campo, en este ejemplo, los códigos de las editoriales de ambas tablas, el campo "codigoeditorial" de "libros" y el campo "codigo" de "editoriales" son los que enlazarán ambas tablas.

Cuando se combina (join, unión) información de varias tablas, es necesario indicar qué registro de una tabla se combinará con qué registro de la otra tabla.

Si no especificamos por qué campo relacionamos ambas tablas, por ejemplo:

 select * from libros
  join editoriales;
el resultado es el producto cartesiano de ambas tablas (cada registro de la primera tabla se combina con cada registro de la segunda tabla), un "join" sin condición "on" genera un resultado en el que aparecen todas las combinaciones de los registros de ambas tablas. La información no sirve en este ejemplo.

Note que en la consulta

 select * from libros
  join editoriales
  on libros.codigoeditorial=editoriales.codigo;
al nombrar el campo usamos el nombre de la tabla también. Cuando las tablas referenciadas tienen campos con igual nombre, esto es necesario para evitar confusiones y ambiguedades al momento de referenciar un campo. En este ejemplo, si no especificamos "editoriales.codigo" y solamente tipeamos "codigo", MySQL no sabrá si nos referimos al campo "codigo" de "libros" o de "editoriales".

Si omitimos la referencia a las tablas al nombrar el campo "codigo" (nombre de campo que contienen ambas tablas):

 select * from libros
  join editoriales
  on codigoeditorial=codigo;
aparece un mensaje de error indicando que "codigo" es ambiguo.

Entonces, si en las tablas, los campos tienen el mismo nombre, debemos especificar a cuál tabla pertenece el campo al hacer referencia a él, para ello se antepone el nombre de la tabla al nombre del campo, separado por un punto (.).

Entonces, se nombra la primer tabla, se coloca "join" junto al nombre de la segunda tabla de la cual obtendremos información y se asocian los registros de ambas tablas usando un "on" que haga coincidir los valores de un campo en común en ambas tablas, que será el enlace.

Para simplificar la sentencia podemos usar un alias para cada tabla:

 select * from libros as l
  join editoriales as e
  on l.codigoeditorial=e.codigo;
Cada tabla tiene un alias y se referencian los campos usando el alias correspondiente. En este ejemplo, el uso de alias es para fines de simplificación, pero en algunas consultas es absolutamente necesario.

En la consulta anterior vemos que el código de la editorial aparece 2 veces, desde la tabla "libros" y "editoriales". Podemos solicitar que nos muestre algunos campos:

 select titulo,autor,nombre from libros as l
  join editoriales as e
  on l.codigoeditorial=e.codigo;
Al presentar los campos, en este caso, no es necesario aclarar a qué tabla pertenecen porque los campos solicitados no se repiten en ambas tablas, pero si solicitáramos el código del libro, debemos especificar de qué tabla porque el campo "codigo" se repite en ambas tablas ("libros" y "editoriales"):

 select l.codigo,titulo,autor,nombre from libros as l
  join editoriales as e
  on l.codigoeditorial=e.codigo;
Si obviamos la referencia a la tabla, la sentencia no se ejecuta y aparece un mensaje indicando que el campo "codigo" es ambiguo.

Servidor de MySQL instalado en forma local.
Ingresemos al programa "Workbench" y ejecutemos el siguiente bloque de instrucciones SQL:

drop table if exists libros, editoriales;

create table libros(
  codigo int unsigned auto_increment,
  titulo varchar(40) not null,
  autor varchar(30) not null default 'Desconocido',
  codigoeditorial tinyint unsigned not null,
  precio decimal(5,2) unsigned,
  cantidad smallint unsigned default 0,
  primary key (codigo)
 );

create table editoriales(
  codigo tinyint unsigned auto_increment,
  nombre varchar(20) not null,
  direccion varchar(30) not null,
  primary key(codigo)
 );

insert into editoriales (nombre,direccion) values('Paidos','Colon 190');
insert into editoriales (nombre,direccion) values('Emece','Rivadavia 765');
insert into editoriales (nombre,direccion) values('Planeta','General Paz 245'); 
insert into editoriales (nombre,direccion) values('Sudamericana','9 de Julio 1008');

insert into libros (titulo, autor,codigoeditorial,precio,cantidad)
  values('El Aleph','Borges',3,43.5,200);
insert into libros (titulo, autor,codigoeditorial,precio,cantidad)
  values('Alicia en el pais de las maravillas','Lewis Carroll',2,33.5,100);
insert into libros (titulo, autor,codigoeditorial,precio,cantidad)
  values('Aprenda PHP','Mario Perez',1,55.8,50);
insert into libros (titulo, autor,codigoeditorial,precio,cantidad)
  values('Java en 10 minutos','Juan Lopez',1,88,150);
insert into libros (titulo, autor,codigoeditorial,precio,cantidad)
  values('Alicia a traves del espejo','Lewis Carroll',1,15.5,80);
insert into libros (titulo, autor,codigoeditorial,precio,cantidad)
  values('Cervantes y el quijote','Borges- Bioy Casares',3,25.5,300);

select * from libros;

select * from libros
  join editoriales
  on libros.codigoeditorial=editoriales.codigo;

select * from libros
  join editoriales;

-- el codigo es ambiguo
select * from libros
  join editoriales
  on codigoeditorial=codigo;

select * from libros as l
  join editoriales as e
  on l.codigoeditorial=e.codigo;

select titulo,autor,nombre from libros as l
  join editoriales as e
  on l.codigoeditorial=e.codigo;

select l.codigo,titulo,autor,nombre from libros as l
  join editoriales as e
  on l.codigoeditorial=e.codigo;

-- el codigo es ambiguo
select codigo,titulo,autor,nombre from libros as l
  join editoriales as e
  on l.codigoeditorial=e.codigo;
  </h3>