<h2>Una librería que tiene almacenados los datos de sus libros en una tabla llamada "libros" quiere donar a una institución 5 libros tomados al azar.

Para recuperar de una tabla registros aleatorios se puede utilizar la función "rand()" combinada con "order by" y "limit":

 select * from libros
  order by rand()
  limit 5;
Nos devuelve 5 registros tomados al azar de la tabla "libros".

Podemos ejecutar la sentencia anterior varias veces seguidas y veremos que los registros recuperados son diferentes en cada ocasión.

Servidor de MySQL instalado en forma local.
Ingresemos al programa "Workbench" y ejecutemos el siguiente bloque de instrucciones SQL:

drop table if exists libros;

create table libros(
  codigo int unsigned auto_increment,
  titulo varchar(40),
  autor varchar(30),
  editorial varchar(20),
  precio decimal(5,2) unsigned,
  primary key(codigo)
 );

insert into libros values(1,'El aleph','Borges','Planeta',23.5);
insert into libros values(2,'Cervantes y el quijote','Borges','Paidos',33.5);
insert into libros 
   values(3,'Alicia a traves del espejo','Lewis Carroll','Planeta',15);
insert into libros 
   values(4,'Alicia en el pais de las maravillas','Lewis Carroll','Planeta',18);
insert into libros values(5,'Martin Fierro','Jose Hernandez','Planeta',34.6);
insert into libros values(6,'Martin Fierro','Jose Hernandez','Emece',45);
insert into libros values(7,'Aprenda PHP','Mario Molina','Planeta',55);
insert into libros values(8,'Java en 10 minutos','Mario Molina','Planeta',45);
insert into libros values(9,'Matematica estas ahi','Paenza','Planeta',12.5);

select * from libros
  order by rand()
  limit 5;

select * from libros order by rand() limit 5;

select * from libros order by rand() limit 5;

select * from libros order by rand() limit 5; </h2>