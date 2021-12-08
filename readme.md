```sql
--1.crear db

CREATE DATABASE blog
    WITH 
    OWNER = postgres
    ENCODING = 'UTF8'
    CONNECTION LIMIT = -1;


--2.crear tablas

create table usuario(
    id_usuario serial PRIMARY KEY,
    email varchar(50)
);

create table POST(
	id_post serial primary key,
	id_usuario_fkp int references usuario(id_usuario),
	titulo varchar (50),
	fecha date
);

create table comentario(
	id_comentario serial primary key,
	id_post_fkc int references post(id_post),
	id_usuario_fkc int references usuario(id_usuario),
	texto varchar(50),
	fecha date
);

--3.insertar datos

insert into usuario(email)
values ('usuario01@gmail.com'),
('usuario02@gmail.com'),
('usuario03@gmail.com'),
('usuario04@gmail.com'),
('usuario05@gmail.com'),
('usuario06@gmail.com'),
('usuario07@gmail.com'),
('usuario08@gmail.com'),
('usuario09@gmail.com');

insert into post (id_usuario_fkp,titulo,fecha)
values(1,'post 1: esto es malo ', '20200629')
(5,'post 2: esto es malo ', '20200620'),
(1,'post 3: esto es excelente ', '2020530'),
(9,'post 4: esto es bueno ', '20200509'),
(7,'post 5: esto es bueno ', '20200710'),
(5,'post 6: esto es excelente ', '20200718'),
(8,'post 7: esto es excelente ', '20200707'),
(5,'post 8: esto es excelente ', '20200514'),
(2,'post 9: esto es bueno ', '20200508'),
(6,'post 10: esto es bueno ', '20200602')
(4,'post 11: esto es bueno ', '20200505'),
(9,'post 12: esto es malo ', '20200723'),
(5,'post 13: esto es excelente ', '20200530'),
(8,'post 14: esto es excelente ', '20200501'),
(7,'post 15: esto es malo ', '20200617');

insert into comentario (id_usuario_fkc,id_post_fkc
,texto,fecha)
values
(3,6,'este es el comentario 1','20200708'),
(4,2,'este es el comentario 2','20200607'),
(6,4,'este es el comentario 3','20200616'),
(2,13,'este es el comentario 4','20200615'),
(6,6,'este es el comentario 5','20200514'),
(3,3,'este es el comentario 6','20200708'),
(6,1,'este es el comentario 7','20200522'),
(6,7,'este es el comentario 8','20200709'),
(8,13,'este es el comentario 9','20200630'),
(8,6,'este es el comentario 10','20200619'),
(5,1,'este es el comentario 11','20200509'),
(8,15,'este es el comentario 12','20200617')
(1,9,'este es el comentario 13','20200501'),
(2,5,'este es el comentario 14','20200531'),
(4,3,'este es el comentario 15','20200628');


--4. seleccionar correo,id y titulo de los post publicados por el usuario 5

select usuario.email, usuario.id_usuario, post.titulo
from usuario 
inner join post 
on usuario.id_usuario = post.id_usuario_fkp
where usuario.id_usuario = 5;


--5. Listar el correo, id y el detalle de todos los comentarios que no hayan sido realizados por el usuario con email usuario06@hotmail.com.

select *
from usuario 
inner join comentario 
on usuario.id_usuario = comentario.id_usuario_fkc
where usuario.email != 'usuario06@gmail.com';

--6. listar usuario que no han publicado ningun post 

select * from usuario 
left join post 
on usuario.id_usuario = post.id_usuario_fkp
where post.titulo is NULL;

--7.listar post con sus comentarios

select post.titulo, comentario.texto
from comentario
right join post 
on comentario.id_post_fkc = post.id_post;


--8.listar usuario que hayan publicado post en junio

select * from usuario 
inner join post 
on usuario.id_usuario = post.id_usuario_fkp
where post.fecha between '20200601' and '20200630';


```