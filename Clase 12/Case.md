<h1>Funciones de control de flujo (case)</h1>

<h3>La función "case" es similar a la función "if", sólo que se pueden establecer varias condiciones a cumplir.

Trabajemos con la tabla "libros" de una librería.

Queremos saber si la cantidad de libros de cada editorial es menor o mayor a 1, tipeamos:

 select editorial,
  if (count(*)>1,'Mas de 2','1') as 'cantidad'
  from libros
  group by editorial;
vemos los nombres de las editoriales y una columna "cantidad" que especifica si hay más o menos de uno. Podemos obtener la misma salida usando un "case":

 select editorial,
  case count(*)
   when 1 then 1
   else 'mas de 1' end as 'cantidad'
  from libros
  group by editorial;
Por cada valor hay un "when" y un "then"; si encuentra un valor coincidente en algún "when" ejecuta el "then" correspondiente a ese "when", si no encuentra ninguna coincidencia, se ejecuta el "else", si no hay parte "else" retorna "null". Finalmente se coloca "end" para indicar que el "case" ha finalizado.

Entonces, la sintaxis es:

 case  
  when  then 
  ...
  else  end
Se puede obviar la parte "else":

 select editorial,
  case count(*)
   when 1 then 1
   end as 'cantidad'
  from libros
  group by editorial;
Con el "if" solamente podemos obtener dos salidas, cuando la condición resulta verdadera y cuando es falsa, si queremos más opciones podemos usar "case". Vamos a extender el "case" anterior para mostrar distintos mensajes:

 select editorial,
  case count(*)
   when 1 then 1
   when 2 then 2
   when 3 then 3
  else 'Más de 3' end as 'cantidad'
  from libros
  group by editorial;
Incluso podemos agregar una cláusula "order by" y ordenar la salida por la columna "cantidad":

 select editorial,
  case count(*)
   when 1 then 1
   when 2 then 2
   when 3 then 3
  else 'Más de 3' end as 'cantidad'
  from libros
  group by editorial
  order by cantidad;
La diferencia con "if" es que el "case" toma valores puntuales, no expresiones. La siguiente sentencia provocará un error:

 select editorial,
  case count(*)
   when 1 then 1
   when >1 then 'mas de 1'
  end as 'cantidad'
  from libros
  group by editorial;
Pero existe otra sintaxis de "case" que permite condiciones:

 case
  when  then 
  ...
  else 
 end
Veamos un ejemplo:

 select editorial,
  case
   when count(*)=1 then 1
   else 'mas de uno'
  end as cantidad
  from libros
  group by editorial;
Servidor de MySQL instalado en forma local.
Ingresemos al programa "Workbench" y ejecutemos el siguiente bloque de instrucciones SQL:

drop table if exists libros;

create table libros(
  codigo int unsigned auto_increment,
  titulo varchar(40) not null,
  autor varchar(30),
  editorial varchar(20),
  precio decimal(5,2) unsigned,
  cantidad smallint unsigned,
  primary key(codigo)
 );

insert into libros (titulo,autor,editorial,precio,cantidad)
  values('El aleph','Borges','Planeta',34.5,100);
insert into libros (titulo,autor,editorial,precio,cantidad)
  values('Alicia en el pais de las maravillas','Carroll L.','Paidos',20.7,50);
insert into libros (titulo,autor,editorial,precio,cantidad)
  values('harry Potter y la camara secreta',null,'Emece',35,500);
insert into libros (titulo,autor,editorial,precio,cantidad)
  values('Aprenda PHP','Molina Mario','Planeta',54,100);
insert into libros (titulo,autor,editorial,precio,cantidad)
  values('Harry Potter y la piedra filosofal',null,'Emece',38,500);
insert into libros (titulo,autor,editorial,precio,cantidad)
  values('Aprenda Java','Molina Mario','Planeta',55,100);
insert into libros (titulo,autor,editorial,precio,cantidad)
  values('Aprenda JavaScript','Molina Mario','Planeta',58,150);

select editorial,
  case count(*)
   when 1 then 1
   else 'mas de 1' end as 'cantidad'
  from libros
  group by editorial;

select editorial,
  case count(*)
   when 1 then 1
   end as 'cantidad'
  from libros
  group by editorial;

select editorial,
  case count(*)
   when 1 then 1
   when 2 then 2
   when 3 then 3
  else 'Más de 3' end as 'cantidad'
  from libros
  group by editorial;

select editorial,
  case count(*)
   when 1 then 1
   when 2 then 2
   when 3 then 3
  else 'Más de 3' end as 'cantidad'
  from libros
  group by editorial
  order by cantidad;

-- la estructura del case es incorrecto
select editorial,
  case count(*)
   when 1 then 1
   when >1 then 'mas de 1'
  end as 'cantidad'
  from libros
  group by editorial;

select editorial,
  case when count(*)=1 then 1
       else 'mas de 1'
  end as 'cantidad'
 from libros
 group by editorial;</h3>