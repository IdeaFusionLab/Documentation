# Documentación
[![GitHub release](https://img.shields.io/github/release/IdeaFusionLab/Documentation.svg)]()
[![GitHub last commit](https://img.shields.io/github/last-commit/IdeaFusionLab/Documentation.svg)]()
[![GitHub issues](https://img.shields.io/github/issues/IdeaFusionLab/Documentation.svg)]()
[![GitHub stars](https://img.shields.io/github/stars/IdeaFusionLab/Documentation.svg)]()
[![GitHub forks](https://img.shields.io/github/forks/IdeaFusionLab/Documentation.svg)](https://github.com/IdeaFusionLab/Documentation/network)
[![GitHub license](https://img.shields.io/github/license/IdeaFusionLab/Documentation.svg)](https://github.com/IdeaFusionLab/Documentation/blob/master/LICENSE)  

## Índice    
1. [Introducción](#id1)
2. [Configuración de bots en servidor](#id2)
3. [ArbusYT](#id3)
4. [ArbusGPT](#id4)
5. [Arbus-Lore](#id5)
6. [License](#idLicense)

 <br/>

## Introducción<a name="id1"></a>  
La finalidad de este documento es detallar las diferentes soluciones implementadas en la organización **IdeaFusionLab**, tanto a nivel técnico como funcional. Al igual que ayudas técnicas de nivel general.
 <br/>

## Configuración de bots en servidor<a name="id2"></a>  
Para registrar un nuevo bot en el servidor deberemos seguir diferentes pasos. Cada uno entrará al servidor con su propio usuario, y una vez dentro podremos ver una carpeta llamada "bots" en la ruta `/home/bots`.

**Clonar el repositorio**  
Dentro de esta carpeta estarán las diferentes soluciones de todos los bots. Para añadir uno nuevo, haremos un git clone del repositorio: `git clone https://github.com/IdeaFusionLab/NuevoBot`.

**Instalar los requerimientos**  
Una vez clonado el repositorio, deberemos entrar en su carpeta e instalar los requerimientos. En el clonado, el bot deberá tener un fichero que se llame requirements.txt o parecido.  
Por lo que en la carpeta del bot ejecutamos: `pip3 install -r requirements.txt`.

**Fichero .env**  
Debemos tener en cuenta que el fichero .env con los tokens, no se suben a los repositorios por seguridad, pero deberemos añadírselo para que los lean en el servidor. Por lo que podemos creárselo con el comando nano, por ejemplo dentro de la carpeta del bot, o subirlo desde Filezilla, por ejemplo.  

Una vez subido el fichero, deberemos ejecutar dentro de la carpeta del proyecto: `source .env`.

 **Probar que funciona**  
Podemos ejecutar el bot para ver que funciona y que los requerimientos junto con el fichero .env se han instalado correctamente. Para ello se ejecuta el comando `python3 bot.py`. 

**NOTA:** Esto te bloqueará la terminal. Puedes hacer Ctrl + C para cerrar el proceso y volver a hacer login. Pero también puedes ejecutar el comando de la siguiente manera y que se ejecute en segundo plano: `python3 bot.py &`. Y luego patar el proceso con `kill PID_del_proceso`.

**Mantener el bot siempre activo**
Para mantener el bot siempre activo deberemos crear un fichero en la ruta `/etc/systemd/system/`. El fichero se llamará `discord-bot.service`. siguiendo la nomenclatura de los ya existentes:  

![Nomenclatura de servicios](https://raw.githubusercontent.com/IdeaFusionLab/Documentation/develop/images/servicios.png)  

Puedes crear el fichero con el comando nano. La plantilla del fichero será esta:  

![Plantilla de servicios](https://raw.githubusercontent.com/IdeaFusionLab/Documentation/develop/images/plantillaServicio.png)   

Y aquí un ejemplo de uno ya configurado:  

![Plantilla de ArbusYT service](https://raw.githubusercontent.com/IdeaFusionLab/Documentation/develop/images/servicioYT.png) 

Se deberán cambiar los siguientes campos:  
- **Description:** Descripción genérica de lo que realiza el servicio. En este caso ejecutar un bot.
- **User:** Será el PID del usuario que ejecute el bot, tendrá que ser uno con permisos de admin. 1001 es el usuario kamikeys y tiene permisos suficientes.
- **ExecStart:** Se deberá cambiar solo la segunda parte, donde será la ruta del fichero .py del bot. Por ejemplo: `/home/bots/botsDiscord/ArbusYT/ArbusYT.py`

Una vez guardamos el fichero, lo habilitamos con: `sudo systemctl enable discord-bot.service`. 
Y lo ejecutamos con: `sudo systemctl start discord-bot.service`.

**Actualizar el servicio**
Si necesitamos actualizar el fichero del servicio, deberemos recargarlo con: `sudo systemctl daemon-reload`.

**Ver errores de los servicios**
Si el servicio no se ejecuta correctamente o después de los pasos anteriores, el bot no funciona como debería. Podemos ver los posibles fallos ejecutando en el server el siguiente comando: `sudo journalctl -u nombre-del-servicio.service`.

Podemos ver los demonios activos con el siguiente comando: `systemctl list-units --type=service --all`.
 <br/>

## ArbusYT<a name="id3"></a>  
[ArbusYT](https://github.com/IdeaFusionLab/ArbusYT)
 <br/>

## ArbusGPT<a name="id4"></a>  
[ArbusGPT](https://github.com/IdeaFusionLab/ArbusGPT)
 <br/>

## Arbus-Lore<a name="id5"></a>  
[Arbus-Lore](https://github.com/IdeaFusionLab/Arbus-Lore)
 <br/>

## License<a name="idLicense"></a>  
TO BE DEFINED
