# ![logo](https://github.com/LemontechSA/test-fullstack-angelo-calvo/blob/develop/practical/thot-ui/src/assets/head-thot.png) Arquitectura de la app

## Acotación

Esta referencia la escribire en español para poder explayarme de mejor manera, por que a pesar que mi estilo es intentar escribir lo relacionado con software en ingles, podemos hacer la excepción en este caso.

## Planteamiento

Cuando enfrente el problema, lo primero que decidi hacer fue abordarla transformandola en problemas mas pequeños (Divide et impera). 

Debido a que la app necesita consumir servicios y desplegar, llegue a la conclusion que el problema se podia transformar en pequeñas entidades independientes que interactuan entre ellas si separaba el desarrollo en Java, React y RoR en 3 subunidades del sistema. 

De esta forma el cliente solo interactua con el frontend, el cual seria construido en React, que luego es el encargado de comunicarse a traves de servicios con una capa de backend intermedia (RoR), la que luego se comunicaria con otra capa de servicios puesta en una hipotetica unidad remota (Java Spark). 

Ademas existiria una base de datos para almacenar datos que serian usados por el backend intermedio para almacenar las consultas que ya se realizaron, asi evitando preguntar dos veces por la mismas comparación.

El esquema que planteo se veria se la siguiente forma

```bash
    _____
    |   |
    |___|
     _|_   __________                       Docker
      |              |                     Subsystem
     _|_             |  
                     |
         ___________\|/_____________
        |                           |                   
        |      1 **Frontend**       |
        |       React / Nginx       |
        |___________________________|                ________________
                    /|\                             |                |
                     |   REST API                   |   Servidor de  |
         ___________\|/_____________                |    Servicios   |
        |                           |   REST API    |                |
        |     2 **Backend**         |/______________|     3-Java     |
        |      Ruby on Rails        |\              |      Spark     |
        |___________________________|               |    Framework   |
                   /|\                              |                |
                    |                               |                |
                 __\|/___                           |                |
                |  4 DB  |                          |________________| 
                |  ____  |
                |  ____  |
                |  ____  |
                |________|

```
El sistema esta dividido en cuatro componentes de software independientes, los cuales seran desplegados en un sistema de contenedores que permita desplegarlos por separarado, teniendo cada uno de estos una dirección ip a la cual acceder. Para este fin usaremos **Docker**, sin embargo haremos links hacia puertos locales de nuestro pc para efectuar las pruebas de una forma mas comoda y evitar problemas que algunas plataformas MACOSX tiene con el driver bridge de Docker.

Los componentes presentados seran descritos a continuación.

- **Frontend:** La capa de frontend esta montada directamente sobre un servidor Nginx, el cual llevara archivos estaticos precompilados. Para este fin utilizaremos CRA con redux y el lenguaje Typescript. Toda la obtención de datos sera efectuada traves de REST usando la libreria Axios. A traves del frontend el usuario efectuara las peticiones de comparación hacia el backend el cual se encargara de gestionar las comparaciones.

- **Backend:** El backend sera el encargado de gestionar las peticiones de comparación. Como criteria tendremos que las peticiones se realizaran al servidor remoto siempre y cuando, estas no hallan sido calculadas previamente o que el usuario pida explicitamente el recalculo de la comparación. En este caso, todos los resultados de las comparaciones deben ser almacenados en una base de datos que nos permita obtenerlos antes de decidir si efectuar la petición en el servidor remoto, actuando de esta forma como un cache de los calculos efectuados por los usuarios independiente del orden en que se coloquen los string, esto quiere decir que la tupla a continuación obtiene los mismo resultados de computo.

        Fx(String1 & String2) = Fx(String2 & String1) 

  La capa de backend sera construida en RoR y puesta en un contenedor docker independiente del frontend, los cuales se comunicaran via REST.

- **Servidor de servicios:** El servidor de servicios (Llamado Siwa), actuara como un servidor de consulta remoto, el cual sera consumido por el backend escrito en RoR. Este servidor efectua operaciones de calculos en los strings y provee de información al backend en RoR, que no sabe calcular por si solo los porcentajes de similitud. 

   Las llamadas a este servidor solo seran efectuadas si las comparación no ha sido computada previamente, o el usuario pide explicitamente que fuerce el recalculo. Si el usuario, pide el recalculo y los resultados de la operacion cambian, estos seran desde ese momento los nuevos datos almacenados para la operación de comparación de esos strings. 

   Como algorithmos de comparación se utilizaran algoritmos para tratamiento de strings presentes en la literatura, los cuales se encuentran implementados en una libreria java llamada [Java String Similarity](https://github.com/tdebatty/java-string-similarity).

- **Base de datos:** La base de datos sera utilizada para almacenar los datos de las comparaciones efectuadas en el servidor de servicios, para asi evitar realizar comparaciones en el servidor, si los datos ya han sido calculados previamente. Para este fin se utilizara mariadb como motor de base de datos.

## Desarrollo

Como estrategia de desarrollo se parte por los mas general a los mas particular. En este caso se aborda desde la construcción del servidor de servicios hacia arriba, siendo el ultimo la ultima capa en construirse, la de frontend. 

Es importante decir que como estrategia de desarrollo usamos **TDD** para todo lo que es Backend y servidor de aplicaciones. Para este fin utilizamos JUnit y una libreria de despegar.com mas unas adaptaciones mias para correr multiples test con la ultima versión de Spark y en Ruby utilizamos Rspec.

Para efectuar la gestion de las tareas utilizamos la metodologia Kanban y para la estrategia de ramificación utilizamos Gitflow.

## Estrategia de deploy

Para enfrentar la estrategia de deploy, decidimos utilizar Docker-compose.
Las instrucciones para efectuar el deploy en producción y el montado de los componentes de desarrollo fue descrito en el README.md de la app Thot

## Palabras finales

Para finalizar, indico que se excluyeron a proposito algunos algoritmos foneticos como por ejemplo **Methaphone** o **Soundex**, ya que considero que si bien sirven para comparar similitudes de strings, son mas enfocados al area fonetica y no tanto de la comparación de caracteres. 

Tambmien el algoritmo de Levenshtein mejorado por peso de las letras o a veces llamado distancia de teclado, fue configurado con un set minimo de combinaciones de errores comunes en el teclado QWERTY español. 

El algoritmo puede ser mejorado agregando mas casos frente a un estudia estadistico de errores mas comunes al usar el teclado en español. Busque data estadistica que viera este tema al respecto, pero por temas de tiempo afirmo que quedo al debe con esto.

## ¿Porque estos nombres de app?

**Siwa** es un oasis en medio del desierto ubicado en egipto, lugar en donde se situaba el oraculo de Amon-Ra.

**Thot o Tot** Es el dios egipcio de la sabiduria, la escritura, la cultura y la musica. Al ser el dios egipcio de la escritura me parecio bien utilizar su nombre para nombrar a la aplicación.

## Agradecimientos

Gracias por las horas de diversion, me lo pase super.
