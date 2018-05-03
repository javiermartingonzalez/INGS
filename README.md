### INGS

# Clonar un repositorio existente

En este apartado vamos a ver el proceso para obtener una copia de un repositorio Git existente, a modo de ejemplo vamos a utilizar un repositorio existente en GitHub,  esta tarea la podemos llevar  acabo mediante el comando es git clone.

El comando para clonar un repositorio existente es “clone” y no “checkout“, esta es una distinción importante con otros sistemas de control de versiones, ya que en lugar de obtener sólo una copia de trabajo, Git recibe una copia completa de casi todos los datos que tiene el servidor.

Cada versión de cada archivo para el historial del proyecto se despliega de forma predeterminada cuando ejecuta git clone, de hecho, si el disco del servidor se daña, se puede utilizar cualquiera de los clones de cualquier cliente para establecer el servidor de nuevo al estado en el que se encontraba cuando se clonó.

A continuación vamos a obtener desde GitHub el repositorio:

$ git clone https://github.com/javiermartingonzalez/INGS.git

# Recuperar un archivo o todo el repositorio a una versión anterior

Partimos de la base de que conoces qué es Git, que conoces lo básico y que en algún momento lo has utilizado para alguna tarea.Todos cometemos errores, pero herramientas como Git nos viene a solucionar algunos de esos errores y problemas en lo referente al código.

Imagina que modificas un archivo y parece que todo está bien, lo añades (git add) y realizas un “commit” de la modificación (git commit).

Después de eso decides que ese archivo necesita un “último ajuste” y finalmente el archivo queda completamente irreconocible y quizás no funcionando como esperabas. ¿Qué podemos hacer?

Podemos recuperar el archivo (prueba.txt en los ejemplos siguientes) al estado en el que estaba antes de la modificación, es decir al estado en el que estaba en el último “commit” para eso utiliza el comando git checkout al último commit conocido que en este caso está en HEAD:

$ git checkout HEAD prueba.txt

Pero si esa versión no es buena, o si quieres volver el archivo en cuestión no a esa versión si no a una anterior en el tiempo, primero deberemos comprobar en el registro log de ese directorio de git los “commits” realizados para poder escoger a la versión que deseamos. Echamos un vistazo a los logs con este comando:

$ git log --oneline

Lo que nos dará una salida “algo” similar a esta (con las lógicas diferencias de “commits”, etc…)

79a4e5f commit prueba
f449007 segundo commit
55df4c2 Primer commit del proyecto.

Imaginemos que queremos devolver el archivo prueba.txt a la versión como estaba en nuestro primer commit del proyecto. Para ello escribiremos el siguiente comando

$ git checkout 55df4c2 prueba.txt

Ahora la versión antigua del archivo ha sido restaurada en el directorio de trabajo. Puedes comprobar el estado del directorio de trabajo mediante el comando git status. No olvides que una vez restaurado el archivo, es necesario volver a añadir el archivo y volver a hacer un “commit” ya que el archivó cambió.

$ git add prueba.txt
$ git commit -m 'restaurar prueba.txt al estado del primer commit.'

Comprobemos en el log de Git que efectivamente todo ha ido como queríamos:

$ git log --oneline

d512580 restaurar prueba.txt al estado del primer commit.
79a4e5f commit prueba
f449007 segundo commit
55df4c2 Primer commit del proyecto.

También podemos llevar no sólo un archivo a un punto predeterminado, si no todos los archivos del repositorio, para ello escribimos:

$ git checkout 55df4c2

Al hacer esto, tu repositorio va atrás en el tiempo por completo, así que si ahora empiezas a trabajar sobre él podrías destruir tu futuro trabajo. Por defecto Git asume que no es eso lo que quieres hacer, así que separa donde se desarrolla el trabajo HEAD del proyecto y te deja empezar a trabajar, creando una nueva rama. Sin embargo en este caso solo se pide acceso a versiones anteriores, por lo tanto aquí finalizan las instrucciones sobre cómo moverse por los commit.