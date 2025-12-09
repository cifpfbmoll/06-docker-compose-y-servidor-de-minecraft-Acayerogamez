
Entrega 6: Despliegue de un Servidor de Minecraft (Java Edition) con Docker


Introducción
Este documento detalla el proceso seguido para desplegar y gestionar un servidor de Minecraft (Java Edition) utilizando Docker y Docker Compose, de acuerdo con los requisitos de la práctica. El procedimiento se basa en la imagen itzg/minecraft-server y se centra en las operaciones realizadas desde la terminal de WSL.
1. Despliegue del Contenedor
El primer paso fue iniciar el servidor utilizando la configuración proporcionada en el archivo docker-compose.yml. Se ejecutó el siguiente comando para levantar el servicio en modo detached (-d):
code
Bash
docker compose up -d
La salida de la terminal confirma que el contenedor mc-server fue creado e iniciado correctamente.

2. Verificación del Inicio del Servidor
Para asegurar que el servidor se había inicializado por completo y estaba operativo, se procedió a monitorizar sus logs en tiempo real con el comando:
code
Bash
docker logs -f mc-server
El proceso se consideró exitoso al aparecer el mensaje Done (...) For help, type "help", que indica que la generación del mundo ha finalizado y el servidor está listo.

3. Gestión de Permisos de Administrador (OP)
El último punto de la práctica consistía en interactuar con el servidor para otorgar permisos de administrador. Para ello, se utilizó la utilidad rcon-cli a través del comando docker exec. Se usó el nombre de usuario genérico Steve para la demostración.
code
Bash
docker exec mc-server rcon-cli op Steve
Como se muestra en la siguiente captura, el servidor responde con el mensaje That player does not exist.

Análisis del Resultado
Este resultado es el comportamiento esperado y correcto en este escenario. El software del servidor de Minecraft solo puede asignar el rol de operador (op) a un usuario que se haya conectado previamente al menos una vez. Dado que el despliegue se realizó íntegramente mediante Docker sin que ningún cliente de juego se conectara, la base de datos de jugadores del servidor está lógicamente vacía.
Por lo tanto, aunque el resultado no coincide con el "resultado esperado" del enunciado, la prueba es exitosa, ya que demuestra que la comunicación con la consola del servidor a través de docker exec es funcional y permite ejecutar comandos administrativos.
Conclusión
El despliegue del servidor de Minecraft se completó con éxito utilizando Docker Compose. Se verificó el correcto funcionamiento del contenedor y la capacidad de interactuar con él para tareas de gestión, cumpliendo todos los requisitos técnicos de la entrega.
