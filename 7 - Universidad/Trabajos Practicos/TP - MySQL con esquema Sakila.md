---
Categoria: Sistemas
Materia: Base de Datos 1
Fecha de Entrega:
Terminado: false
Tags:
  - "#Practico"
---

1) Mostrar nombre y apellido de los actores que participaron del film ‘GLASS DYING’ y no lo hicieron en el film 'AFRICAN EGG'

```SQL 
USE sakila;
SELECT a.first_name, a.last_name, film.title, a.actor_id
FROM actor AS a JOIN film_actor on (a.actor_id = film_actor.actor_id) JOIN film on (film_actor.film_id = film.film_id)
WHERE (film.title LIKE 'GLASS DYING' AND a.actor_id NOT IN (SELECT film_actor.actor_id FROM film_actor WHERE film_actor.film_id IN (SELECT film.film_id FROM film WHERE film.title LIKE 'AFRICAN EGG')));

```

2) Mostrar los films de categorías ‘Action’, ‘Music’ y ‘Sci-Fi’ en los que haya participado algún autor que también participó en un film de categoría ‘Documentary’ en lenguaje ‘English’.

```SQL


```
