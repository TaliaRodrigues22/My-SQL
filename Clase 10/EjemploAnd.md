<h1>Operadores Lógicos (and - or - not)</h1>

Problema:
Trabajamos con la tabla "libros" de una librería.

Eliminamos la tabla, si existe.

Creamos la tabla con la siguiente estructura:

 create table libros(
  codigo int unsigned  auto_increment,
  titulo varchar(40),
  autor varchar(30),
  editorial varchar(15),
  precio decimal(5,2),
  primary key(codigo)
 );

 <span>
Ingresamos algunos registros:
</span> 
<hr>
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
  <hr>
Vamos a recuperar registros estableciendo 2 condiciones, necesitamos los operadores lógicos.

Para recuperar todos los registros cuyo autor sea igual a "Borges" y cuyo precio no supere los 20 pesos, tipeamos:

 select * from libros
  where autor='Borges' and
  precio<=20;
Muestra un registro, porque sólo uno cumple con ambas condiciones.

Seleccionamos los libros cuyo autor sea "Paenza" y/o cuya editorial sea "Planeta":

 select * from libros
  where autor='Paenza' or
  editorial='Planeta';
Muestra 3 registros, 1 de ellos cumple con la primera condición, 1 con la segunda y 1 con ambas.

Queremos ver los libros cuyo autor sea "Borges" o cuya editorial sea "Planeta":

 select * from libros
  where (autor='Borges') xor
  (editorial='Planeta');
Muestra 2 registros, 1 cumple con la primera condición y 1 con la segunda. Los registros que cumplen con ambas condiciones no fueron seleccionados porque usamos el operador "xor".

Establecemos la condición que la editorial sea igual a "Planeta", y recuperamos con un "select" los libros que no cumplan la condición:

 select * from libros
  where not (editorial='Planeta');
Muestra 4 registros que NO cumplen con la condición.

Los paréntesis sirven para establecer el orden de prioridad de evaluación de las condiciones.

Analicemos los siguientes ejemplos, estas sentencias devuelven resultados distintos:

 select * from libros
  where (autor='Borges') or
  (editorial='Paidos' and precio<20);
 select * from libros
  where (autor='Borges' or editorial='Paidos')
  and (precio<20);
En el primer caso selecciona primero los libros de "Paidos" con precio<20 y también los de "Borges", sin considerar el precio.

En el segundo caso selecciona los libros de "Borges" y/o "Paidos", si tienen precio<20.

El libro con código 5, no aparece en la segunda consulta porque el precio no es <20; si en la primera porque la condición referida al precio afecta a los libros de "Paidos".