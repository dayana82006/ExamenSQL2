# ExamenSQL2

CREATE DATABASE sakilaCampus;

USE sakilaCampus;


CREATE TABLE pais(
	id_pais INT AUTO_INCREMENT PRIMARY KEY,
	nombre VARCHAR(50)
);
CREATE TABLE film_text(
 	film_id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR (255),
	description text
);
CREATE TABLE idioma(
	id_idioma INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR ( 50),
    ultima_actualizacion TIMESTAMP
);
 CREATE TABLE categoria(
	id_categoria INT PRIMARY KEY AUTO_INCREMENT ,
    nombre VARCHAR(25),
	ultima_actualizacion TIMESTAMP
);
CREATE TABLE actor(
	id_actor INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(50),
    apellidos VARCHAR(50),
    ultima_actualizacion TIMESTAMP
);
CREATE TABLE ciudad(
	id_ciudad INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(50),
	id_pais INT,
    ultima_actualizacion TIMESTAMP,
    FOREIGN KEY (id_pais) REFERENCES pais(id_pais)
);

CREATE TABLE direccion(
	id_direccion INT  AUTO_INCREMENT PRIMARY KEY,
    direccion VARCHAR(50),
    direccion2 VARCHAR(50),
    distrito VARCHAR (50),
    id_ciudad INT,
    codigo_postal VARCHAR (10),
    FOREIGN KEY (id_ciudad) REFERENCES ciudad(id_ciudad)
);
CREATE TABLE almacen(
	id_almacen INT,
    empleado_jefe  INT,
    id_direccion INT,
    ultima_actualizacion TIMESTAMP,
    FOREIGN KEY (id_direccion) REFERENCES direccion(id_direccion)
);
CREATE TABLE cliente (
	id_cliente INT AUTO_INCREMENT PRIMARY KEY,
    id_almacen INT,
    nombre VARCHAR(50),
    apellidos VARCHAR(50),
    email VARCHAR(50),
    id_direccion INT,
    activo TINYINT,
    fecha_creacion DATETIME,
  	ultima_actualizacion TIMESTAMP,
    FOREIGN KEY (id_direccion) REFERENCES direccion(id_direccion),
    FOREIGN KEY (id_almacen) REFERENCES almacen(id_almacen)
);
CREATE TABLE empleado(
	id_empleado  INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(50),
    apellidos VARCHAR(50),
    email VARCHAR(50),
    id_direccion INT,
    imagen BLOB,
    id_almacen INT,
    activo TINYINT,
    username VARCHAR(16),
    password VARCHAR(40),
    FOREIGN KEY (id_direccion) REFERENCES direccion (id_direccion),
    FOREIGN KEY (id_almacen) REFERENCES almacen (id_almacen)
);

CREATE TABLE pelicula(
	id_pelicula INT  AUTO_INCREMENT PRIMARY KEY,
    titulo VARCHAR(50),
    descripcion TEXT,
    anyo_lanzamiento YEAR,
    id_idioma INT,
    idioma_original INT,
    duracion_alquiler TINYINT,
    rental_rate DECIMAL(4,2),
    duracion SMALLINT,
	replacement_cost DECIMAL(5,2),
    clasificacion ENUM('G','PG','PG-13','R','NC-17'),
 	caracteristicas_especiales SET('Trailers','Commentaries','Deleted Scenes','Behind the Scenes'),
    ultima_actualizacion TIMESTAMP,
    FOREIGN KEY (id_idioma) REFERENCES idioma(id_idoma)
);

CREATE TABLE pelicula_categoria(
	id_pelicula INT,
    id_categoria INT,
    ultima_actualizacion TIMESTAMP,
    FOREIGN KEY (id_pelicula) REFERENCES pelicula(id_pelicula),
    FOREIGN KEY (id_categoria) REFERENCES categoria(id_categoria)
);

CREATE TABLE pelicula actor(
	id_autor INT,
    id _pelicula INT,
    FOREIGN KEY  (id_autor) REFERENCES autor(id_autor),
    FOREIGN KEY (id_pelicula) REFERENCES pelicula(id_pelicula)
);
CREATE TABLE inventario(
	id_inventario INT AUTO_INCREMENT PRIMARY KEY,
    id_pelicula INT,
    id_almacen INT,
    ultima_actualizacion TIMESTAMP,
    FOREIGN KEY (id_almacen) REFERENCES almacen(id_almacen),
    FOREIGN KEY (id_pelicula) REFERENCES pelicula(id_pelicula)
);

 CREATE TABLE alquiler(
     id_alquiler INT AUTO_INCREMENT PRIMARY KEY,
     fecha_alquiler DATETIME,
     id_inventario MEDIUMINT,
     id_cliente INT,
     fecha_devolucion DATETIME,
     id_empleado INT,
     ultima_actualizacion TIMESTAMP,
     FOREIGN KEY (id_inventario ) REFERENCES inventario(id_inventario),
     FOREIGN KEY (id_cliente) REFERENCES cliente(id_cliente),
     FOREIGN KEY (id_empleado) REFERENCES empleado(id_empleado)
 );
  CREATE TABLE pago(
	id_pago INT AUTO_INCREMENT PRIMARY KEY,
    id_cliente smallint,
    id_empleado tinyint,
    id_alquiler INT,
    total decimal(5,2),
    fecha_pago DATETIME,
    ultima_actualizacion TIMESTAMP,
     FOREIGN KEY (id_alquiler REFERENCES alquiler(id_alquiler),
     FOREIGN KEY (id_cliente REFERENCES cliente(id_cliente),
     FOREIGN KEY id_empleado REFERENCES empleado(id_empleado)
);

postada :no me gusta las bases de datos
