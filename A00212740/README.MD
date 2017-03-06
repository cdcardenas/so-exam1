Universidad ICESI

Informe examen 1

Christian Cárdenas

A00212740

Repository URL: https://github.com/cdcardenas/so-exam1

Reposiory URL: https://github.com/ICESI-training/so-exam1/A00212740



#punto 1

los retos de cmd challenge son:

a. last lines/: imprimir las ultimas cinco lineas de access.log
solucion: este reto se puede resolver utilizando el comando tail e indicando el numero de lineas a imprimir en este caso seria
	
	tail -5 access.log

b. Hello world/ : imprime hello Word en la ventana de comandos

	echo Hello World

c. Current_working_directory/: imprime el directorio actual de trabajo, este reto se puede resolver usando unicamente el comando pwd que imprime en consola el directorio actual

	pwd

d.List_files/: lista los archivos en la carpeta actual, podemos usar el comando ls que me imprime todos los archivps del directorio actual y -l para que imprima 1 por linea

	ls -l

e.Print_file_contents/ : imprime el contenido del archivo léeme.txt

	cat leeme.txt

f. Simple_sort/: organiza los contenidos del archivo sort.txt

	sort sort.txt

g. search_for_files_containing_string/: imprime todos los archivos en el directorio actual que contengan la linea “500”

	grep -l 500 *

#Punto 2

Existen varias formas de hacer scripts automatizados en CentOS, la que se utilizó en este para este punto consiste en el uso de los comandos expect, esta función permite comunicarse con otros programas por medio de un “guion”, este guion funciona como si fuera el usuario el que estuviera interactuando con el SO, esto es especialmente útil cuando se quiere trabajar con rutinas que requieren entradas directas del usuario, como por ejemplo una conexión por SSH en la cual hay que loguearse en una maquina remota.
Para utilizar expect primero debemos instalarlo, por lo que usamos los comandos


	!/usr/bin/expect

	se conecta mediante ssh.

	spawn shh operativos@192.168.57.30

	-se hace uso de expect, el cual permite en combinacion con 	el comando send crear posibles rutinas de posibles 	salidas de la consola con el SO, de forma que se pueden 	automatizar la ejecuciÃ³n de scripts
	-se estan descargando Metamorfosis de Franz Kafka y Tom 	Sawyer de Mark Twain

	spawn ssh operativos 192.168.57.30

	expect "operativos@192.168.57.30's password:"

	send "operativos\r"

	expect "$"

	send "cd /tmp\r"

	expect "$"

	send "wget http://www.gutenberg.org/files/5200/5200.txt\r"

	expect "$"

	send "exit\r"

	expect eof

	spawn ssh operativos 192.168.57.40

	expect "operativos@192.168.57.40's password:"

	send "operativos\r"

	expect "$"

	send "cd /tmp\r"

	expect "$"

	send "wget http://www.gutenberg.org/files/74/74.txt\r"

	expect "$"

	send "exit\r"

	expect eof


#punto 3

Creación de un contenedor de debían mediante LXC y dar pruebas de su funcionamiento
Para poder instalar un contenedor LXC primero debemos instalar todas las librerías (interprete de perl y paquetes de debootstrap) necesarias para poder ejecutar sus dependencias por lo que es necesario ejecutar los comandos.

	yum install epel-release

	yum install debootstrap perl libvirt

Ahora si podemos instalar las plantillas de LXC para crear los contenedores que deseemos

	yum install lxc lxc-templates

Mediante el uso de los comandos status y start prodemos verificar si el proceso daemon de LXC se encuentra funcionando o no. En caso de que no lo este lo debemos activar

	systemctl status lxc.service

	systemctl start lxc.service

Ahora mediante el uso del comando #lxc-checkconfig podemos verificar el status del núcleo de virtualización.
Ahora debemos seleccionar la plantilla que queramos usar para crear el contenedor, podemos ver las plantillas disponibles mediante el uso del comando

		ls -alh /usr/share/lxc/templates
En nuestro caso vamos a instalar un contenedor de Debian por lo que lo crearemos mediante el comando

		lxc-create -n contenedorDChristian -t Debian

Una vez termine la creación del contenedor debemos iniciarlo 
		
		lxc-start -n contenedorDChristian -d

Finalmente, para acceder al contenedor usamos el comando

		lxc-console -n contenedorDChristian


#Referencias

Instalación de contenedor: lxc http://www.tecmint.com/install-create-run-lxc-linux-containers-on-centos/

Comando expect: https://www.lifewire.com/linus-unix-command-expect-2201096

Cmd challenge: https://cmdchallenge.com

