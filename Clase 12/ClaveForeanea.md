<h1>Clave foránea</h1>
<h3>Un campo que se usa para establecer un "join" (unión) con otra tabla en la cual es clave primaria, se denomina "clave ajena o foránea".

En el ejemplo de la librería en que utilizamos las tablas "libros" y "editoriales" con los campos:

 libros: codigo (clave primaria), titulo, autor, codigoeditorial, precio, cantidad y
 editoriales: codigo (clave primaria), nombre.
el campo "codigoeditorial" de "libros" es una clave foránea, se emplea para enlazar la tabla "libros" con "editoriales" y es clave primaria en "editoriales" con el nombre "codigo".

Cuando alteramos una tabla, debemos tener cuidado con las claves foráneas. Si modificamos el tipo, longitud o atributos de una clave foránea, ésta puede quedar inhabilitada para hacer los enlaces.

Las claves foráneas y las claves primarias deben ser del mismo tipo para poder enlazarse. Si modificamos una, debemos modificar la otra para que los valores se correspondan.

Servidor de MySQL instalado en forma local.
Ingresemos al programa "Workbench" y ejecutemos el siguiente bloque de instrucciones SQL:

drop table libros, editoriales;

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
  primary key(codigo)
 );

insert into editoriales values(2,'Emece');
insert into editoriales values(15,'Planeta');
insert into editoriales values(23,'Paidos');

insert into libros values(1,'El aleph','Borges',23,4.55,10);
insert into libros values(2,'Alicia en el pais de las maravillas','Lewis Carroll',2,11.55,2);
insert into libros values(3,'Martin Fierro','Jose Hernandez',15,7.12,4);

-- en las versiones nuevas de MySQL no lo permite
alter table libros
  modify codigoeditorial char(1);

select * from libros;

select l.titulo,e.nombre
  from libros as l
  join editoriales as e
  on l.codigoeditorial=e.codigo;

-- en las versiones nuevas de MySQL no lo permite
alter table editoriales
  modify codigo char(1);</h3>