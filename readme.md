# Actividad 32 - Postgresql Avanzado

En esta actividad trabajaremos con las diferentes queries desde el terminal de postgres.

Para desarrollar esta actividad, tendrán que anotar cada una de las queries que utilizaron en un archivo **txt**  o **md** y subir los archivos comprimidos en formato **zip** a la plataforma Empieza.

Deben también ingresar, al final de este archivo (txt), el nombre de los integrantes del grupo que participaron en el desarrollo de esta actividad.

Cada integrante debe subir el archivo a la plataforma.

## Ejercicio 1

Se busca desarrollar una aplicación llamada Pintagram. Esta aplicación debe permitir a los usuarios subir imágenes y que, a su vez, estas imágenes pertenezcan a ese usuario. Además los usuarios podrán darle like a las imágenes de otros usuarios. Cada una de las imágenes tendrá varios tags y cada uno de esos tags podrá referenciar a varias imágenes. En este ejercicio se tomarán en cuenta las consultas a 2 o más tablas y los constrains al momento de la creación de la tabla.

##Restricciones (constraints)

En esta parte del ejercicio se debe investigar como aplicar relgas a la base de datos para que se cumpla:

1. Un usuario solo puede darle like 1 vez a cada imagen.
2. Una imagen no puede tener tags repetidos.

#### Crear base de datos en base a los requerimientos indicados.

## Checkpoints
1. **Antes de empezar a crear la base de datos deben leer todas las instrucciones, modelar la base y generar un diagrama que tendrán que adjuntar a las respuestas de este ejecrcicio.**
2. Ingresar 2 imágenes por usuario.
3. Ingresar 3 likes por cada imagen.
4. Ingresar 8 tags.
5. Ingresar 3 tags por imagen.
6. Crear una consulta que muestre el nombre de la imagen y la cantidad de likes que tiene esa imagen.
7. Crear una consulta que muestre el nombre del usuario y los nombres de las fotos que le pertenecen.
8. Crear una consulta que muestre el nombre del tag y la cantidad de imagenes asociadas a ese tag.

RESPUESTAS:

#create database
CREATE DATABASE pintagram
\c pintagram

#create table users
CREATE TABLE users(user_id serial primary key UNIQUE, name varchar(64));

#open table
SELECT * FROM users;

#create table images
CREATE TABLE images(image_id serial primary key UNIQUE, image varchar(64), user_id INTEGER REFERENCES users(user_id));

#open table
SELECT * FROM images;

#create tags
CREATE TABLE tags(tag_id serial primary key UNIQUE, tag varchar(64));

#open table
SELECT * FROM tags;

#create images_tags
CREATE TABLE images_tags(image_id INTEGER REFERENCES images(image_id), tag_id INTEGER REFERENCES tags(tag_id), UNIQUE(image_id,tag_id));

#open table
SELECT * FROM images_tags;

#create images_likes
CREATE TABLE images_likes(user_id INTEGER REFERENCES users(user_id), image_id INTEGER REFERENCES images(image_id), UNIQUE(user_id, image_id));

#Ingresar 2 usuarios
INSERT INTO users(name) VALUES('Nancy');
INSERT INTO users(name) VALUES('Miguel');
INSERT INTO users(name) VALUES('Seba');

#Ingresar 2 imagenes por usuario
INSERT INTO images(image,user_id) VALUES('salgan de mi playa',2);
INSERT INTO images(image,user_id) VALUES('vacaciones',2);
INSERT INTO images(image,user_id) VALUES('vacaciones en la playa',1);
INSERT INTO images(image,user_id) VALUES('quiero ir a la playa',1);

#Ingresar 3 likes por cada imagenes
INSERT INTO images_likes(user_id,image_id) VALUES('1','1');
INSERT INTO images_likes(user_id,image_id) VALUES('2','1');
INSERT INTO images_likes(user_id,image_id) VALUES('3','1');

#Ingresar 8 tags
INSERT INTO tags(tag) VALUES('arte'),('computación');
INSERT INTO tags(tag) VALUES('deporte'),('salud'),('animales'),('tierra'),('sol'),('playa');

#Ingresar 3 tags por imagen
INSERT INTO images_tags(image_id,tag_id) VALUES(1,8),(1,7),(1,6);

#Crear una consulta que muestre el nombre de la imagen y la cantidad de likes que tiene esa imagen
#Crear una consulta que muestre el nombre del usuario y los nombres de las fotos que le pertenecen
#Crear una consulta que muestre el nombre del tag y la cantidad de imagenes asociadas a ese tag
