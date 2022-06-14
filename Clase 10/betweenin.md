<h1>Hemos visto los operadores relacionales:
</h1>
= (igual), <> (distinto), > (mayor), < (menor), >= (mayor o igual), <= (menor o igual), is null/is not null (si un valor es NULL o no).

Existen otros que simplifican algunas consultas:

Para recuperar de nuestra tabla "libros" los registros que tienen precio mayor o igual a 20 y menor o igual a 40, usamos 2 condiciones unidas por el operador lógico "and":

 select * from libros
  where precio>=20 and precio<=40;
Podemos usar "between":

 select * from libros
  where precio between 20 and 40;
"between" significa "entre". Averiguamos si el valor de un campo dado (precio) está entre los valores mínimo y máximo especificados (20 y 40 respectivamente).

Si agregamos el operador "not" antes de "between" el resultado se invierte.

Para recuperar los libros cuyo autor sea 'Paenza' o 'Borges' usamos 2 condiciones:

 select * from libros
  where autor='Borges' or autor='Paenza';
Podemos usar "in":

 select * from libros
  where autor in('Borges','Paenza');
Con "in" averiguamos si el valor de un campo dado (autor) está incluido en la lista de valores especificada (en este caso, 2 cadenas).

Para recuperar los libros cuyo autor no sea 'Paenza' ni 'Borges' usamos:

select * from libros where autor<>'Borges' and autor<>'Paenza';
También podemos usar "in" :

 select * from libros
  where autor not in ('Borges','Paenza');
Con "in" averiguamos si el valor del campo está incluido en la lista, con "not" antecediendo la condición, invertimos el resultado.

Servidor de MySQL instalado en forma local.
Ingresemos al programa "Workbench" y ejecutemos el siguiente bloque de instrucciones SQL para utilizar los operadores relacionales 'between' y 'in':

drop table if exists libros;

create table libros(
  codigo int unsigned auto_increment,
  titulo varchar(40),
  autor varchar(30),
  editorial varchar(15),
  precio decimal(5,2) unsigned,
  primary key(codigo)
 );

insert into libros (titulo,autor,editorial,precio)
  values('El aleph','Borges','Planeta',15.50);
insert into libros (titulo,autor,editorial,precio)
  values('Martin Fierro','Jose Hernandez','Emece',22.90);
insert into libros (titulo,autor,editorial,precio)
  values('Martin Fierro','Jose Hernandez','Planeta',39);
insert into libros (titulo,autor,editorial,precio)
  values('Aprenda PHP','Mario Molina','Emece',19.50);
insert into libros (titulo,autor,editorial,precio)
  values('Cervantes y el quijote','Borges','Paidos',35.40);
insert into libros (titulo,autor,editorial,precio)
  values('Matematica estas ahi', 'Paenza', 'Paidos',19);

select * from libros
  where precio>=20 and
  precio<=40;

select * from libros
  where precio between 20 and 40;

select * from libros
  where autor='Borges' or
  autor='Paenza';

select * from libros
  where autor in('Borges','Paenza');

select * from libros
  where autor<>'Borges' and
  autor<>'Paenza';

select * from libros
  where autor not in ('Borges','Paenza');