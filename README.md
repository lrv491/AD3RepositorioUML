# AD-3. Diagramas UML

## Autora

- **Lucía Ramírez Verdú**
- Usuario de GitHub: **lrv491**
- Correo de UNIR: <lucia.ramirez491@comunidadunir.net>

---

## Repositorio

- Url del Repositorio: <https://github.com/lrv491/AD3RepositorioUML>

---

## Torneo eSports

Este proyecto se trata de diseñar y desarrollar un sistema de gestión de torneos de eSports.

Este proyecto forma parte de la tercera actividad de la asignatura Entornos de Desarrollo de 1DAM.

### Índice

1. [Análisis del Problema y Requisitos del Sistema](#análisis-del-problema-y-requisitos-del-sistema)

2. [Identificación de los casos de uso y elaboración del diagrama](#identificación-de-los-casos-de-uso-y-elaboración-del-diagrama)

3. [Identificación de clases y relaciones](#identificación-de-clases-y-relaciones)

4. [Creación del diagrama de clases UML](#creación-del-diagrama-de-clases-uml)

5. [Conclusión](#conclusión)

### Análisis del Problema y Requisitos del Sistema

**¿Quiénes son los actores que interactúan con el sistema y sus acciones?**

- ***Jugador***
    Es quien participa en las partidas de los equipos. Está en constante contacto con el juego.
- ***Mánager***
    Es quien registra a los equipos y a sus jugadores en los torneos.
- ***Espectador***
    Es quien visualiza, dentro de la partida, el *pov* (point of view) de cada jugador. Esto hace que sea más dinámico para los seguidores del torneo.
- ***Árbitro***
    Es quien visualiza la partida para que no se realicen acciones ilegales como el uso de *exploits* siendo uso de *bugs* o *glitches*, uso inapropiado del hardware, uso de software de terceros no autorizados... Podría parar la partida, repetir rondas, quitar pausas tácticas, cambiar el resultado de rondas y partidas.
- ***Administrador***
    Puede desempeñar las mismas funciones que cualquier otro actor pero con más permisos, es decir, son los que toman la última decisión referente a añadir jugadores, añadir equipos, modificar resultados...

### Identificación de los casos de uso y elaboración del diagrama

En este apartado, se realizan los casos de uso correspondientes para el sistema.

#### Gestión de Equipos y jugadores

En este caso de uso, he identificado dos actores, siendo Mánager y Administrador.

El **Mánager** se encarga de registrar al equipo, que en el sistema incluiría comprobar si el equipo existe, no añadirlo.

También, añade jugadores, incluiría comprobar si el jugador existe no se añadiría, si existiera pero con otro equipo o sin equipo, se esperaría a la confirmación del **Administrador** para poder actualizar el estado del jugador. Por ende, también se comprobaría si el equipo existe.

Además, consulta equipos que se extiende en consultar jugadores, pero no es necesario consultar un equipo para consultar a un jugador ya que lo puede realizar directamente.

El **Administrador** puede realizar todo lo anterior, añadiendo confirmaciones o rechazazos de registros de equipos y jugadores por diversos motivos como pueden ser que ya estén inscritos en el torneo, que la información sea incorrecta, que no puedan participar por anteriores baneos de equipos o jugadores...

![Diagrama de Caso de Uso](https://github.com/lrv491/AD3RepositorioUML/blob/main/Diagramas/DiagramaDeCasoDeUso.jpg?raw=true)

### Identificación de clases y relaciones

Observando los posibles casos de uso de la actividad, he podido identificar siete clases. Una clase interfaz, una clase de control y cinco entidades.

#### VistaTorneo

##### Métodos de VistaTorneo

Son métodos públicos que sirven para mostrar la información de los Equipos, Torneos, Jugadores, Partidas y Resultados, con sus variantes.

    + mostrarEquipos():List<Equipo>
    + mostrarTorneo(): List<Torneo>
    + mostrarJugadores(): List<Jugador>
    + mostrarJugadores(Equipo): List<Jugador>
    + mostrarPartidas(): List<Partida>
    + mostrarPartidas(Torneo): List<Partida>
    + mostrarPartidas(Equipo): List<Partida>
    + mostrarResultados(): List<Resultado>
    + mostrarResultados(Equipo): List<Resultado>

Esta Clase se relaciona directamente con la Clase de control ControlTorneo, en java sería que ControlTorneo implementa VistaTorneo.

#### ControlTorneo

##### Atributos de ControlTorneo

Los atributos de ControlTorneo incluye una lista por cada entidad con la que se relaciona, siendo atributos privados.

    -equipos:List<Equipo>
    -torneos:List<Torneo>
    -jugadores:List<Jugador>
    -resultados:List<Resultado>

##### Métodos de ControlTorno

Los métodos de ControlTorneo corresponden al acrónimo *CRUD* que se utiliza para realizar las funciones de Crear (*Create*), Leer (*Read*), Actualizar (*Update*) y Borrar (*Delete*). Por cada entidad con la que se relaciona hay uno de cada. Pongo el ejemplo de una de ellas:

    + buscarTodos():List<Equipo>
    + buscarUno(int): Equipo
    + insertar(Equipo):int
    + eliminar(int): int
    + actualizar(Equipo):int

Esta clase de control se relaciona con Equipo, Jugador, Partida, Torneo y Resultado. En java sería como la clase de implementación del patrón DAO.

#### Equipo

##### Atributos de Equipo

    -idEquipo:int
    -nombreEquipo:String

##### Métodos de Equipo

Los métodos de Equipo son los necesarios para la manipulación de objetos en Java

    + setIdEquipo(int): void
    + setNombreEquipo(String):void
    + getIdEquipo():int
    + getNombreEquipo():String
    + toString():String
    + equals(Equipo):boolean
    + hashCode():int

Esta clase se relaciona con la clase Jugador, un equipo puede tener mínimo un jugador pero muchos jugadores como máximo ya que hay que contar con  jugadores, coach, assistant coach, performance coach...

También, se relaciona con la clase Partida, un equipo puede estar en muchas partidas o en ninguna, ya sea porque nunca haya participado pero esté dentro del sistema.

Por último, se relaciona con la clase Toneo, un equipo puede estar en muchos torneos o en ninguno, ya sea porque en ese torneo no haya participado pero siga estando el equipo en el sistema

#### Jugador

##### Atributos de Jugador

    -idJugador:int
    -nombreArtistico:String
    -nombre:String
    -apellido:String
    -fNaci:Date
    -equipo:Equipo

##### Métodos de Jugador

Los métodos de Jugador son los necesarios para la manipulación de objetos en Java

    + setIdJugador(int): void
    + setNombreArtistico(String):void
    + setNombre(String):void
    + setApellido(String):void
    + setFNaci(Date):void
    + setEquipo(Equipo):void
    + getIdJugador():int
    + getNombreArtistico():String
    + getNombre():String
    + getApellido():String
    + getFNaci():String
    + getEquipo():Equipo
    + toString():String
    + equals(Jugador):boolean
    + hashCode():int

Esta clase se relaciona con la clase Equipo, un jugador puede estar en un equipo o en ninguno, ya que puede ser un jugador que se añadió al sistema porque estaba en un equipo, pero lo echaron al tiempo y no pudo entrar en otro equipo.

#### Torneo

##### Atributos de Torneo

    -idTorneo:int
    -nombreTorneo:String
    -fechaIni:Date
    -fechaFin:Date

##### Métodos de Torneo

Los métodos de Torneo son los necesarios para la manipulación de objetos en Java

    + setIdTorneo(int): void
    + setNombreTorneo(String):void
    + setFechaIni(Date):void
    + setFechaFin(Date):void
    + getIdTorneo():int
    + getNombreTorneo():String
    + getFechaIni():Date
    + getFechaFin():Date
    + toString():String
    + equals(Torneo):boolean
    + hashCode():int

Esta clase se relaciona con la clase Equipo, un torneo puede tener mínimo un equipo o tener muchos, puesto que para que haya un torneo, tiene que tener al menos un equipo.

También, se relaciona con la clase Partida, un torneo tiene que tener mínimo una partida o muchas.

#### Partida

##### Atributos de Partida

    -idPartida:int
    -equipo1:Equipo
    -equipo2:Equipo
    -torneo:Torneo
    -fecha:Date

##### Métodos de Partida

Los métodos de Partida son los necesarios para la manipulación de objetos en Java.

    + setIdPartida(int): void
    + setEquipo1(Equipo):void
    + setEquipo2(Equipo):void
    + setTorneo(Torneo):void
    + setFecha(Date):void
    + getIdPartida():int
    + getEquipo1():Equipo
    + getEquipo2():Equipo
    + getTorneo():Torneo
    + getFecha():Date
    + toString():String
    + equals(Partida):boolean
    + hashCode():int

Esta clase se relaciona con la clase Equipo, una partida tiene que tener dos equipos siempre, puesto que para que haya un enfrentamiento y vayan ascendiendo en el torneo, necesitan que se enfrenten dos equipos únicamente.

También, se relaciona con la clase Resultado, una partida si o si tiene que tener siempre un resultado.

#### Resulatdo

##### Atributos de Resultado

    -idResultado:int
    -ganador:Equipo
    -marcador:String
    -duracion:Date
    -partida:Partida

##### Métodos de Resultado

Los métodos de Resultado son los necesarios para la manipulación de objetos en Java.

    + setIdResultado(int): void
    + setGanador(Equipo):void
    + setMarcador(String):void
    + setDuracion(Date):void
    + setPartida(Partida):void
    + getIdResultado():int
    + getMarcador():String
    + getGanador():Equipo
    + getDuracion():Date
    + getPartida():Partida
    + toString():String
    + equals(Resultado):boolean
    + hashCode():int

Esta clase se relaciona con la clase Partida, para haber un resulatdo, tiene que haber una partida.

### Creación del diagrama de clases UML

Como se puede ver en la imagen, he utilizado dependencia, asociación, agregación y composición.

![Diagrama de Clases](https://github.com/lrv491/AD3RepositorioUML/blob/main/Diagramas/DiagramaDeClases.jpg?raw=true)

### Conclusión

A la hora de realizar este proyecto, me sentí un poco desbordada ya que con los conocimientos que teníamos, veía complicado el tema de las clases de control y las interfaces. No entendía como se debían de relacionar en el diagrama y sinceramente, no he conseguido entenderlo.

Para relacionarlo, me he basado en los esquemas del patrón DAO que damos en la clase de programación. Si lo he comprendido bien, la clase control es como si fuera la implementación de la interfaz en el modelo de negocio por cada una de las Clases del javabean.

A pesar de lo anterior, siento que he aprendido realizando la práctica, sobre todo, con prueba y error, y volviendo a mirar los diagramas días después para detectar fallos.
