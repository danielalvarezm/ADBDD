CREATE TYPE Tipo_Direccion AS
( 
    Tipo_Via  VARCHAR(4),
    Nombre_Via  VARCHAR(100),
    Poblacion VARCHAR(50),
    CP VARCHAR(5),
    Provincia VARCHAR(50)
);


CREATE TYPE JefeProyecto AS
(
    Cod_JefeProyecto INTEGER,
    Nombre  VARCHAR(50),
    Direccion   Tipo_Direccion,
    Telefono VARCHAR(9),
    Dirige  REF Proyecto
);


CREATE TABLE T_Jefe_Proyecto OF JefeProyecto
(
    PRIMARY KEY (Cod_JefeProyecto),
    UNIQUE Nombre
);


CREATE TYPE Proyecto AS
(
    Cod_Proyecto   INTEGER,
    Nombre  VARCHAR(50),
    Dirigido_por REF JefeProyecto,
    Tiene_planos REF Plano
);


CREATE TABLE T_Proyecto OF Proyecto
(
    PRIMARY KEY (Cod_Proyecto),
    NOT NULL Dirigido
);


CREATE TYPE Plano AS
( 
    Cod_Plano  INTEGER,
    Fecha_entrega   DATE,
    Arquitectos VARCHAR(15)ARRAY[10],
    Dibujo_Plano BITMAP,
    Num_Figuras INTEGER,
    Tiene_Fig   REF Figura MULTISET
);

CREATE TABLE T_Plano OF Plano 
(
    PRIMARY KEY (Cod_Plano)
);


CREATE TYPE Figura AS 
(
    Cod_Figura  INTEGER,
    Nombre  VARCHAR(30),
    Color   VARCHAR(30),
    Plano_Pertenece  REF Plano,
    TRIGGER trigger_actualizar_figuras_after_insert RETURNS INTEGER
);

CREATE TRIGGER trigger_actualizar_figuras_after_insert FOR Figura
AFTER INSERT OR DELETE ON T_Figura
    BEGIN
        IF INSERT THEN
            UPDATE TABLE Plano WHERE Figuras.Nombre = Plano.Tiene_Fig SET Plano.Num_Figuras = Plano.Num_Figuras + 1;
        ELSE
            UPDATE TABLE Plano WHERE Figuras.Nombre = Plano.Tiene_Fig SET Plano.Num_Figuras = Plano.Num_Figuras - 1;
    END;


CREATE TABLE T_Figura OF Figura
(
    PRIMARY KEY (Cod_Figura),
    NOT NULL Plano_Pertenece
);


CREATE TYPE Poligon UNDER Figura AS 
(
    Num_Lineas  INTEGER,
    Tiene_Lineas REF Linea MULTISET
);


CREATE TABLE T_Poligono OF Poligono UNDER T_Figura;


CREATE TYPE Punto AS 
(
    Eje_x INTEGER,
    Eje_y INTEGER
);


CREATE TYPE Linea AS 
(
    Id_Linea    NUMBER,
    Tiene_Puntos    Punto ARRAY(2)
);

CREATE TABLE T_Linea OF Linea
(
    Id_Linea PRIMARY KEY
);

CREATE TYPE Arquitectos AS
(
    Cod_Arquitecto INTEGER,
    Nombre VARCHAR(30),
    Dirige  REF Plano
);

CREATE TABLE T_Arquitectos OF Arquitectos
(
    PRIMARY KEY Cod_Arquitecto
);
