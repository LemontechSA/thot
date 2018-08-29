## Data model design
**Design Question:** 

Un colegio necesita un sistema para administrar sus cursos. El sistema tiene que soportar que se ingresen varios cursos. Cada curso tendrá un profesor a cargo y una serie de alumnos inscritos. 

Cada profesor, así como cada alumno puede estar en más de un curso. Además cada curso tendrá una cantidad no determinada de pruebas, y el sistema debe permitir ingresar la nota para cada alumno en cada prueba. Todas las pruebas valen lo mismo.

### Data Model

![data model](https://raw.githubusercontent.com/LemontechSA/test-full-stack-angelo/angelo-calvo/theoretical/model.png?token=AHb1k6sIlbyySHD9yccwJLheoDxcba4lks5biZqpwA%3D%3D)

## Query Questions

### Resolución 1
**Question:** Escriba una Query que entregue la lista de alumnos para el curso "programación"

```sql
SELECT s.name, s.lastname FROM `students` AS s
INNER JOIN students_x_courses AS sc ON s.id = sc.student_id
LEFT JOIN courses AS c ON sc.course_id = c.id
WHERE c.name = 'programacion'
```

### Resolution 2
**Question:** Escriba una Query que calcule el promedio de notas de un alumno en un curso.

```sql
SELECT s.name, s.lastname, s.run, AVG(ca.calification) AS average FROM `students` AS s
INNER JOIN califications AS ca ON s.id = ca.student_id
LEFT JOIN tests AS t ON ca.test_id = t.id
LEFT JOIN courses AS co ON co.id = t.course_id
WHERE s.run=':run' AND co.code=':code'
```
Where: 

- :run is the student unique **run**
- :code is the unique code of course. 
 
This columns was included in the model because the name, can be repeat and cause problems to diferenciate an entity of other.

### Resolution 3
**Question:** Escriba una Query que entregue a los alumnos y el promedio que tiene en cada curso.
```sql

SELECT s.name, s.lastname, s.run, co.name, co.code, AVG(ca.calification) AS average FROM `students` AS s
INNER JOIN califications AS ca ON s.id = ca.student_id
LEFT JOIN tests AS t ON ca.test_id = t.id
LEFT JOIN courses AS co ON co.id = t.course_id
GROUP BY co.id
```

### Resolution 4
**Question:** Escriba una Query que lista a todos los alumnos con más de un curso con promedio rojo.

```sql
SELECT r.name, r.lastanme, r.run FROM
(SELECT s.name, s.lastname, s.run FROM `students` AS s
INNER JOIN califications AS ca ON s.id = ca.student_id
LEFT JOIN tests AS t ON ca.test_id = t.id
LEFT JOIN courses AS co ON co.id = t.course_id
GROUP BY co.id
HAVING AVG(ca.calification) < 4) AS r
HAVING COUNT(r.run) > 1
```
