# Software Engineer Test

Este es un test pensado para demostrar las habilidades de los candidatos para integrar el __Área de Ingeniería__ de __Lemontech__.  Esta prueba esta pensada para desarrolladores _Full Stack Java + ROR_.

## Problema 1. `Teórico`

Un colegio necesita un sistema para administrar sus cursos. El sistema tiene que soportar que se ingresen varios cursos. Cada curso tendrá un profesor a cargo y una serie de alumnos inscritos. Cada profesor, así como cada alumno puede estar en más de un curso. Además cada curso tendrá una cantidad no determinada de pruebas, y el sistema debe permitir ingresar la nota para cada alumno en cada prueba. Todas las pruebas valen lo mismo.

### Modelo de datos

Escriba a continuación las tablas que utilizaría para resolver este problema con los campos y llaves de éstas. Intente hacer el modelo lo más robusto posible, pero sin incluir datos adicionales a los que se plantean acá.

### SQL
Considerando el enunciado anterior conteste las siguientes preguntas:

1. Escriba una Query que entregue la lista de alumnos para el curso "programación"
2. Escriba una Query que calcule el promedio de notas de un alumno en un curso.
3. Escriba una Query que entregue a los alumnos y el promedio que tiene en cada curso.
4. Escriba una Query que lista a todos los alumnos con más de un curso con promedio rojo.

## Problema 2. `Práctico`

Construir una aplicación web que permita analizar el porcentaje de similitud entre dos strings. Debe tener una interfaz de usuario que permita introducir las cadenas de caracteres a analizar, así como también recordar los resultados de los análisis realizados. El historial de búsqueda debe servir como un mecanismo para evitar realizar nuevamente la consulta de análisis a menos que el usuario expresamente lo solicite. El servicio de análisis de strings debe manejar al menos tres criterios de comparación. El servicio de similitud de strings debe estar construído en Java y la aplicación Rails debe comunicarse con él para obtener los resultados.

Cuentas con espacio suficiente para demostrar tu visión respecto a cómo organizar componentes en un pequeño servicio. Lemontech es una empresa de producto que siempre piensa en sus usuarios, por ende esperamos que la solución entregada vele por una experiencia de usuario coherente y simple.

Esperamos que escribas código de calidad. Una mala respuesta tiene la forma de una gran función o procedimiento, en donde existe un alto acoplamiento de código y es imposible testear algo más pequeño que el total de la operación del programa. Una buena respuesta está bien organizada, separada y cuenta con clases o funciones con tests y responsabilidad claramente definida. Lógicamente, se espera un buen coverage de testing. También será interesante conocer algún insight de análisis y diseño de la solución presentada.

### Instrucciones

Crear un branch a partir de la rama `master` con tu nombre y apellido, por ejemplo `john-doe` y termina con un Pull request de los cambios.

Para el desarrollo de la solución __se deben__ ocupar las siguientes tecnologias: __Spark Framework__, __Ruby on Rails__ y __React__.

Las aplicaciones de RoR y Spark deben estar en directorios separados, dentro de este mismo repositorio.

Se debe sobreescribir este README.md con las instrucciones para poder probar la aplicación.
