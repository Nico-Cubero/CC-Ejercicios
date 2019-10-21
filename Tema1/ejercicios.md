#	Tema 1. Arquitecturas software para la nube
##	Ejercicios desarrollados por Nicolás Cubero Torres.
####	Ejercicio 1. Buscar una aplicación de ejemplo, preferiblemente propia, y deducir qué patrón es el que usa. ¿Qué habría que hacer para evolucionar a un patrón tipo microservicios?
La aplicación que se va a tomar como referencia es el asistente conversacional **CProfessorBot** desarrollado como **Trabajo de Fin de Grado** durante el curso 18/19 en la **Universidad de Córdoba** y a la que se puede acceder en el siguiente [link](https://github.com/Nico-Cubero/C-ProfessorBot).

La aplicación desarrollada se centraba en la programación de un sistema servidor que interactuaba por medio de un asistente conversacional, chatbot o simplemente bot con los usuarios de esta plataforma de mensajería, haciendo uso de una API.

El sistema presenta una clara arquitectura en capas de naturaleza cliente-servidor en la que eran distinguibles las siguientes capas: la capa de presentación encargada de recibir y devolver la información al usuario por medio de mensajes de la plataformade mensajería, la capa de aplicación encargada de gestionar y coordinar el funcionamiento del sistema servidor y del resto de capas y la capa de acceso a datos encargada de almacenar, gestionar y presentar los datos que el sistema debe de almacenar al resto de capas.

Por su parte, esta arquitectura se podría hacer evolucionar a una arquitectura basada en microservicios separando cada uno de los módulos funcionales del sistema servidor (módulo de procesamiento del lenguaje natural, módulo de acceso a los datos, módulo de gestión del sistema y módulo de comunicación con la plataforma Telegram) en diferentes microservicios independientes de forma conveniente y haciendo uso de colas de mensajes para cada uno de ellos.

La comunicación entre los diferentes microservicios se llevaría a cabo por medio de mensajes, por otro lado, la reestructuración de la arquitectura en microservicios llevaría a la desaparición del módulo de gestión del sistema, sobre el cual se encontraba centralizado y el cual constituía un posible cuello de botella.

El sistema se encontraría centralizado sobre el módulo de comunicación con la plataforma de mensajería Telegram, el cual al recibir las diferentes peticiones de los usuarios, se comunicaría con el resto de microservicios mediante mensajes para solicitar diversos servicios a los mismos.

#### Ejercicio 2.En la aplicación que se ha usado como ejemplo en el ejercicio anterior, ¿podría usar diferentes lenguajes? ¿Qué almacenes de datos serían los más convenientes?

En la aplicación se podrían usar diferentes lenguaje de programación para implementar los diferentes microservicios siempre que para el paso de mensajes entre los microservicios se empleen mecanismos y/o protocolos de comunicación independientes del lenguaje de programación, como los protocolos HTTPS con REST o HTTP/HTTPS simple y AMQP.

Por otro lado, el sistema almacena datos de diferente naturaleza: Por un lado almacena datos de naturaleza estática, representado por información que no sufre grandes cambios a lo largo del tiempo y, en concreto se refiere a la información sobre los usuarios registrados (profesorado y alumno), información sobre los foros docentes, información teórica etc; mientras que, por otro lado, almacena información de naturaleza dinámica, como la información de los mensajes enviados y recibidos y cualquier otra información estadística recopilada sobre el uso del sistema por parte del alumnado.

Mientras que para los datos de naturaleza estática convendría usar un almacén de datos consistente en un sistema base de datos relacional, para los datos de tipo dinámico convendría usar algún tipo de base de datos no estructurada, en concreto, un sistema de base de datos de tipo documental como MongoDB  podría reflejar y manipular eficientemente esta información.
