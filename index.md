2.1.Crear diagrama


Crea un diagrama utilizando MySQL Workbench de una base de datos de un e-commerce (tienda online) con las siguientes tablas:


•	Tabla Users


•	Tabla Products


•	Tabla Orders


•	Tabla Categories


Debe mostrar los tipos de relaciones entre cada tabla. *Recuerda que en el caso de una relación muchos a muchos necesitarás una tabla intermedia.
![foto](/Sin%20t%C3%ADtulo.png)


CREATE TABLE my_friki_space.cash(
id int auto_increment,
products_id int,
products_categories_id int,
orders_id int,
orders_users_id int,
PRIMARY KEY (id),
FOREIGN KEY (products_id) REFERENCES products(id),
FOREIGN KEY (orders_id) REFERENCES orders(id));


2.2. Ejecute las siguientes consultas SQL
A continuación, deberá realizar las siguientes consultas SQL:

2.2.1 INSERTAR DATOS


•	Inserte al menos 5 nuevos usuarios.


CREATE TABLE my_friki_space.users(
id int auto_increment,
dni VARCHAR(20),
first_name VARCHAR(45),
last_name VARCHAR(45),
client boolean,
phone int,
city VARCHAR(60),
PRIMARY KEY (id)
);

INSERT INTO my_friki_space.users (dni, first_name,
last_name, client,
phone, city) values ('29473817Y', 'Marco',
'Sanchis G', true, 647284637, 'Valencia'),
 ('37592758H', 'Angel',
'Herrera B', true, 638472957, 'Madrid'), ('583374628K', 'Carla',
'Amandia Q', true, 648275938, 'Madrid'), ('57294738W', 'Andrea',
'Alvarez T', false, 645836574, 'Malaga'), ('47582665Y', 'Juan',
'Maestre B', true, 65749372, 'Jaen');

Inserte al menos 5 nuevos productos.


CREATE TABLE my_friki_space.products(
id int auto_increment,
categories_id int,
name_product VARCHAR(100),
price DECIMAL (5,2),
stock int,

PRIMARY KEY (id),
FOREIGN KEY (categories_id) REFERENCES categories(id)
);
•	INSERT INTO my_friki_space.products ( categories_id, name_product,
price, stock) values ( 3, 'Figure of One Piece_luffy',
40.34, 102994), (3, 'Figure of One Piece_sabo',
60.21, 49384),(1, 'Manga of Jujutsu Kaisen',
14.21, 40060),(4, 'T shirt Levi Ackerman',
25.10, 583028),(2, 'Manga of Boku no hero',
15.32, 994);
•	Inserte al menos 5 nuevos pedidos(orders).
CREATE TABLE my_friki_space.orders(
id int auto_increment,
products VARCHAR(100),
amount int,
users_id int,

PRIMARY KEY (id),
FOREIGN KEY (users_id) REFERENCES users(id)
);

INSERT INTO my_friki_space.orders (
products, amount) values ('Figure of Tanjiro', 1),('Manga of One piece', 4),('T-shirt of Mario bros', 5),('Figure of Tanjiro', 3),('Figure of Sanji skypea', 6);
Inserte al menos 2 tipos de categorías.
CREATE TABLE my_friki_space.categories(
id INT auto_increment,
name_categorie VARCHAR(45),
stock int,
PRIMARY KEY (id)
);

INSERT INTO my_friki_space.categories ( name_categorie,
 stock) values ( 'Manga 1980-2000',
 102994),('Manga 2000-2022', 2938492), ( 'Figure',
 49504), ('t-shirt', 4005930);		
2.2.2 ACTUALIZAR DATOS


•	Cambiar el nombre de un producto. Para ello, genera una consulta que afecte solo a un determinado producto en función de su id.


UPDATE my_friki_space.products SET name_product = 'Figure of Ace' WHERE id =
2;


•	Cambiar el precio de un producto a 50€. Para ello, genera una consulta que afecte solo a un determinado producto en función de su  id.


UPDATE my_friki_space.products SET price = 50 WHERE id =
1;

2.2.3 OBTENER DATOS

•	Seleccione todos los productos con un precio superior a 20€.


SELECT * FROM my_friki_space.products WHERE price >20;


•	Muestre de forma descendente los productos.


SELECT * FROM my_friki_space.products ORDER BY price DESC;


•	Seleccione todos los productos y que muestre la categoría a la que pertenecen.


select * from my_friki_space.products 
INNER JOIN my_friki_space.categories 
on my_friki_space.products.categories_id = my_friki_space.categories.id;


Seleccione todos los usuarios y muestre sus pedidos.


select * from my_friki_space.users
INNER JOIN my_friki_space.orders
on my_friki_space.users.id = my_friki_space.orders.users_id;


•	Selecciona un producto por su id y que muestre la categoría a la que pertenece.


select * from my_friki_space.products
INNER JOIN my_friki_space.categories
on my_friki_space.categories.id = my_friki_space.products.categories_id
WHERE my_friki_space.products.id=2;


•	Seleccione a un usuario por su id y muestre los pedidos que tiene.


select * from my_friki_space.users
INNER JOIN my_friki_space.orders
on my_friki_space.users.id = my_friki_space.orders.users_id
WHERE my_friki_space.users.id=3;


3. Extra


3.1.1 BORRAR DATOS


⦁ Elimina un producto por su id.


DELETE FROM my_friki_space.products WHERE id = 3;


3.2 Actualizar diagrama


Crea una nueva tabla reviews y añadela al diagrama especifica también el tipo de relación.


CREATE TABLE my_friki_space.reviews(
id int auto_increment,
score_review int,
text_review TEXT (150),
user_id int,
product_id int,
PRIMARY KEY (id),
FOREIGN KEY (user_id) REFERENCES users(id),
FOREIGN KEY (product_id) REFERENCES products(id));


3.3. Ejecute las siguientes consultas SQL
A continuación, deberá realizar las siguientes consultas SQL:
3.3.1 INSERTAR DATOS


•	Inserte al menos 5 nuevas reviews.

INSERT INTO my_friki_space.reviews(score_review,
text_review, user_id, product_id) VALUES
(9,'figura de calidad, le gustó mucho a mi pareja', 3, 2),
(5,'no me gustó nada el nuevo manga', 3, 5),(9,'estaba deseando añadirla a mi colección', 3, 2),(7,'mi hijo quedó encantado con su nueva camiseta', 4, 4),(9,'mucho detalle en la figura, me encantó', 2, 1), (1,'figura dañada', 1, 2);
		
3.3.2 ACTUALIZAR DATOS


•	Cambia el contenido de una review


UPDATE my_friki_space.reviews SET text_review='después de leermelo entero, me ha convencido', score_review=7 WHERE id =2;

3.3.3 OBTENER DATOS


•	Seleccione todas las reviews.


SELECT * FROM my_friki_space.reviews;


•	Seleccione todos los productos con sus respectivas reviews.


SELECT * FROM my_friki_space.products
INNER JOIN my_friki_space.reviews ON products.id = reviews.product_id;


•	Muestre un producto con sus reviews.


SELECT * FROM my_friki_space.products
INNER JOIN my_friki_space.reviews ON products.id = reviews.product_id
WHERE products.id=4;


•	Muestre los productos junto a la categoría a la que pertenece y sus reviews.


SELECT * FROM my_friki_space.products
INNER JOIN my_friki_space.reviews ON products.id = reviews.product_id
INNER JOIN my_friki_space.categories ON categories.id = products.categories_id;


•	Seleccione un usuario y muestre sus pedidos junto a los productos que contiene cada pedido.

3.3.4 BORRAR DATOS

⦁ Elimina una review por su id.
DELETE FROM my_friki_space.reviews WHERE id=6;
