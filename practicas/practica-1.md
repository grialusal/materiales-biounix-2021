# Sesión I - Toma de contacto

Herramientas computacionales para bioinformática: UNIX, expresiones regulares y shell script

======================================

* * *

### 1. Configuración del entorno de trabajo.
    
Si no se configura bien el entorno de trabajo, se rendirá mucho menos en la realización de las prácticas. Primero hay que configurar el terminal. Para ello, hay que poner de acuerdo al programa de terminal que tenéis instalado en el aula de informática con la configuración que tiene el servidor donde se realizarán las prácticas.  
    
Antiguamente, los servidores eran accedidos mediante un dispositivo denominado terminal. Fundamentalmente constaban de un monitor y un teclado y la suficiente electrónica para recoger los caracteres tecleados y mostrar otros por la pantalla. Los caracteres recogidos se enviaban a través de una línea de conexión (normalmente serie) hasta el servidor y, la respuesta de este llegaba al terminal por la misma línea.  
    
Actualmente, el esquema es diferente. En lugar de un terminal se dispone de PCs de propósito general y un programa que emula el comportamiento de los antiguos terminales. La conexión en lugar de hacerse a través de una línea dedicada, se realiza por Internet y siguiendo un protocolo, que normalmente para conexiones de texto será SSH, la versión con transmisión codificada del viejo TELNET.  
      
Programas para PC emuladores de los distintos modelos de terminales existen muchos. Debéis usar aquel que más os guste y que mejor sepáis configurar. Si usas Windows, el más famoso es [PuTTY (SSH)](https://www.putty.org/), aunque desde hace ya un tiempo, Windows da la opción de instalar un cliente SSH. 
    
      
Si usáis Linux o MacOS, no necesitáis ningún programa externo. Os basta con abrir un terminal y poner:
    
	ssh nombredeusuario@cpg3.der.usal.es
    
La huella digital que os debe poner la primera vez que os conectéis es:
    
    `37:4c:31:84:02:97:81:f9:5d:7d:4b:23:01:fd:4c:01`
    
Verificar esta huella sirve para evitar ataques al protocolo de seguridad encriptado de SSH.  
      
De trabajar en Linux o MacOS (ambos sistemas UNIX), tenéis además la ventaja de que las órdenes que veamos las podéis probar en el servidor o en el propio Linux. Además, lo mejor es que os instaléis un Linux del mismo tipo que hay en las aulas (Ubuntu). 
      
CPG3 usa la codificación utf-8 para tratar con los caracteres propios del español (ñ, acentos, aperturas de interrogación y exclamación, etc.), muy probablemente la misma que usáis en vuestros equipos. Si veis caracteres extraños en el terminal, aseguráos que la codificación de vuestro terminal es UTF-8: "Preferencias", "Codificación", "UTF-8".  
      
    
### 2. Conexión con el servidor.
    
El servidor que usaremos para hacer las prácticas se llama en Internet `cpg3.der.usal.es`. En el programa emulador que uséis, o en el propio ssh, debéis indicar el nombre del servidor, como se indicó en el apartado anterior, para conectaros. Teclead en el sitio apropiado `cpg3.der.usal.es`. Si no podéis conectaros desde casa, probad con la dirección IP de  caso: `212.128.140.52`.  
                
    
    Teclead ahora vuestro login, intro, y contraseña, y pulsad la tecla `enter` (⏎)
        
    
### 3. ¿Quién soy? ¿Dónde estoy?
    
Una vez os habéis conectado correctamente al servidor, CPG3 os va a recibir con un mensaje parecido a este:
    
	Linux cpg3 4.9.0-12-amd64 #1 SMP Debian 4.9.210-1+deb9u1 (2020-06-07) x86_64

	The programs included with the Debian GNU/Linux system are free software;
	the exact distribution terms for each program are described in the
	individual files in /usr/share/doc/*/copyright.
	
	Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
	permitted by applicable law.
	Last login: Mon Jan 10 10:28:15 2021 from 212.128.183.122
	
	abenito@cpg3:~$
    
En la primera línea, el servidor se presenta y nos dice la versión del sistema operativo que tiene instalada (`Debian 4.9.210-1+deb9u1 (2020-06-07) x86_64`, en el caso del ejemplo). También os muestra la licencia de uso de los programas que tiene instalados, indicandoós que es software libre. Os avisa de que, como es sabido, los programas vienen sin garantía. Así que si rompéis algo no podréis pasarle la factura al bueno de Stallman :) 

Finalmente, os dice cuándo fue la última vez que os conectasteis y desde qué ordenador. En la siguiente, el servidor se presenta y nos dice la versión del sistema operativo que tiene instalada. 
      
Acto seguido, se queda esperando a que le demos órdenes y nos lo indica mediante el _prompt_ o indicador. Vuestro indicador quizás sea distinto del que sale en el ejemplo. Esto se puede configurar y aprenderéis cómo hacerlo más adelante.  
      
Sin embargo, vosotros os encontráis como quien se despierta en una isla desierta y no recuerda cómo llegó allí, ni siquiera recuerda quién es. Pues se lo preguntamos al servidor:
    
	abenito@cpg3:~$ whoami
	abenito
	abenito@cpg3:~$
    
Teclead la orden toda junta, en minúsculas y os pondrá quiénes sois, esto es, vuestro identificador de usuario dentro de la máquina. A continuación, el servidor se queda esperando a que le deis más órdenes.  
      
Si os equivocáis al teclear y aún no habéis pulsado Intro, basta con que rectifiquéis con la tecla de retroceso, como es costumbre. Incluso podéis usar las flechas del cursor. Si ya habéis pulsado Intro, podéis revisar y cambiar las órdenes anteriores con las flechas de arriba y abajo.  
      
Los usuarios de UNIX se agrupan en grupos para poder organizarse mejor. Preguntemos cuál es nuestro grupo:
    
	abenito@cpg3:~$ groups
	abenito sudo staff
    
Cada usuario, y cada grupo, tiene un número identificador propio, algo así como su DNI:
    
	abenito@cpg3:~$ id
	uid=1003(abenito) gid=1003(abenito) grupos=1003(abenito),27(sudo),50(staff)
    
Vemos que el identificador del usuario `abenito` en esta máquina es el 1003 y el del grupo `staff` es el 50.  
      
Una vez hemos resuelto esta importante cuestión epistemológica, pasemos a ver dónde estamos:
    
	abenito@cpg3:~$ hostname
	cpg3
    
Bueno, esto no es una sorpresa...ya sabíamos que estábamos en CPG3. Pero, ¿en qué lugar dentro de CPG3 exactamente?
    
	abenito@cpg3:~$ pwd
	/home/abenito
    
`pwd` significa _print working directory_. El servidor organiza su espacio en disco en un árbol de ficheros y directorios, unas dentro de otras, formando lo que se denomina el _sistema de ficheros_.
      
    
![Sistema de ficheros](sistema-ficheros.jpg)
    
      
Una ruta (o _path_) nos permite localizar un fichero o directorio concreto dentro del sistema se ficheros. Así, la ruta `/home/abenito` nos dice que nos encontramos en una carpeta (o directorio) llamada `abenito` que se encuentra dentro de otra llamada `home`, que a su vez está dentro de la carpeta principal o _directorio raíz_. En UNIX no existen las letras de las unidades, por lo que las rutas no las contienen. El directorio de trabajo es aquel directorio (o carpeta) en el que estamos situados en este momento.  
      
Existen dos tipos de rutas:
    
*   _Absolutas_: comienzan con el símbolo "`/`" y localizan el fichero o directorio a partir del directorio raíz.
*   _Relativas_: no comienzan con el símbolo "`/`" y localizan el fichero o directorio a partir del directorio de trabajo actual.
    
      
La orden `pwd` nos ha dado una ruta absoluta. Existen dos abreviaturas que pueden incluirse como si fueran un directorio dentro de una ruta. Son:
    *   _._ (punto): equivale al directorio actual
    *   _.._ (dos puntos seguidos): equivale al directorio _padre_ del directorio actual, esto es, al directorio que lo contiene
  

### 4. ¿Quién está conmigo?
    
Para saber si hay alguien más trabajando en el servidor, usamos la orden `who`:
    
	abenito@cpg3:~$ who
	alejandro pts/17       2021-01-10 11:22 (212.128.183.13)
	abenito  pts/15       2021-01-10 10:38 (172.28.3.46)
	abenito  pts/16       2021-01-10 11:04 (212.128.183.13)
    
Bueno, no hay mucha gente, salvo un misterioso `alejandro` que está conectado desde la misma máquina que el que escribe (`abenito`). ¿Quién será? :) 

En clase, podréis observar la lista de las personas que se encuentran en esos momentos conectados y el nombre del ordenador desde dónde se conectan. Podéis cotillear un poco más usando la orden `finger`: 
    
	abenito@cpg3:~$ finger
	Login      Name       Tty      Idle  Login Time   Office     Office Phone
	abenito    ""         pts/15     47  Jan 10 10:38 (172.28.3.46)
	abenito    ""         pts/16         Jan 10 11:04 (212.128.183.13)
	alejandro  ""         pts/17      2  Jan 10 11:22 (212.128.183.13)
    
La orden `finger` nos da el nombre de usuario, el nombre real (si se proporcionó en el momento en el que se creó el usuario), el identificador del terminal, el tiempo en minutos que lleva inactivo el usuario, cuándo se conectó y desde dónde.  
      
Además, si añadimos un nombre, nos dará información acerca de las cuentas que coincidan con ese nombre:
    
	abenito@cpg3:~$ finger alejandro
	Login: alejandro      			Name: ""
	Directory: /home/alejandro          	Shell: /bin/bash
	On since Mon Jan 10 11:22 (CET) on pts/17 from 212.128.183.13
	   5 minutes 6 seconds idle
	No mail.
	No Plan.
    
Una vez conocemos quién está con nosotros en el servidor, podemos intentar comunicarnos con estas personas. En estos tiempos de pandemia, quizás sea una buena idea usar este método alternativo. Para ello, disponéis de la orden `write`. Como estoy solo en el servidor, reproduzco aquí una conversación entre mis dos usuarios, con sesiones abiertas en dos ventanas distintas. Como he podido comprobar a lo largo de mi vida, esto de hablar con tu otro yo está muy mal visto, así que vosotras podéis probarlo con una compañera de clase. 
    
	abenito@cpg3:~$ who
	alejandro pts/17       2021-01-10 11:22 (212.128.183.13)
	abenito  pts/15       2021-01-10 10:38 (172.28.3.46)
	abenito  pts/16       2021-01-10 11:04 (212.128.183.13)
    
Escribimos a nuestro otro yo (el situado en el terminal `pts/17` en el ejemplo):
    
	abenito@cpg3:~$ write alejandro pts/17
	Hola...
	Hace tiempo que no hablamos...
    **<CTRL-C>**
    
En vuestro caso no hace falta que pongáis el terminal de la persona a la que queráis mandar el mensaje. El mensaje puede tener todas las líneas que queráis. Para que el ordenador sepa que habéis acabado, pulsad al inicio de la línea las teclas `CTRL` y `C`. Esto es lo que recibió mi otro yo:
    
	Message from abenito@cpg3 on pts/16 at 11:36 ...
	Hola...
	Hace tiempo que no hablamos...
	EOF
    
Este mensaje aparece de golpe en el terminal de la otra persona, por lo que, a veces, puede resultar molesto. Le podemos decir al servidor que no queremos que nos molesten con mensajes, mediante la orden `mesg n`. Si, más tarde, deseamos volver a permitirlos, teclearemos `mesg y`.  
      
Existe otra orden que permite a dos usuario escribirse interactivamente (al modo del un chat). Se llama `talk`, pero no suele estar activada por defecto en los servidores de hoy en día (tampoco en CPG3).
   
### 5. ¿Qué puedo hacer?
    
Hay infinidad de órdenes que podemos pedir al sistema que ejecute. Vamos a centrarnos en una para ir sintiendo el modo en que se trabaja en una máquina UNIX. La orden elegida es de las más usadas: `ls`. Adelante con ella:

	abenito@cpg3:~$ ls
	certs		      home.tar.gz	 jupyterhub_config.py	   materiales-bio-python     ps1	 visualization-curriculum
	cpg3.der.usal.es.ssl  informatica-i	 jupyterhub_config.py.bak  materiales-informatica-i  python-bio
	genomes		      informatica-i-old  jupyterhub.log		   notebooks		     sorteo


La orden `ls` muestra el contenido (ficheros y directorios) del directorio de trabajo. Aquí guardo muchas cosas, como seguro que vosotros también. Al menos, deberíais ver vuestros trabajos de la asignatura de programación. Si en vuestro directorio no hubiera nada, `ls`, como es costumbre en UNIX, no imprimirá nada. Si todo va bien, no se avisa de ningún modo al usuario. Algunas diferencias entre el tratamiento de ficheros en UNIX y Windows (algunas ya comentadas) son las siguientes:
    
1.  El separador en las rutas es "/" en UNIX y "\\" en Windows
2.  UNIX sí que distingue entre mayúsculas y minúsculas en el nombre de directorios y ficheros
3.  Si el nombre de un fichero o directorio empieza por "." (un punto), el fichero o directorio es _oculto_ y no aparecerá en los listados hechos con `ls` por defecto
    
      
Los ficheros ocultos existen solo para organizarnos mejor. De hecho, es muy fácil verlos. Lo hacemos con `ls -a` (all):
    
	abenito@cpg3:~$ ls -a
	.	       .cache		     home.tar.gz	 jupyterhub_config.py	   .nano	       python-bio
	..	       .cargo		     informatica-i	 jupyterhub_config.py.bak  .nbgrader.log       sorteo
	.bash_history  certs		     informatica-i-old	 jupyterhub.log		   .node_repl_history  .sqlite_history
	.bash_logout   .config		     .ipynb_checkpoints  .local			   notebooks	       .ssh
	.bash_profile  cpg3.der.usal.es.ssl  .ipython		 materiales-bio-python	   .profile	       visualization-curriculum
	.bashrc        genomes		     .jupyter		 materiales-informatica-i  ps1		       .wget-hsts
    
Seguro que ahora sí que os sale algún fichero... El hecho de añadir opciones, como en este caso `-a`, a las órdenes de UNIX, es muy típico. Estas opciones hacen que el comportamiento de la orden varíe un poco.  
      
Podemos pedir a `ls` que nos muestre un fichero o directorio concreto. Si es un fichero, lo muestra tal cual:
    
	abenito@cpg3:~$ ls home.tar.gz
	home.tar.gz
    
Si es un directorio, nos muestra su contenido:
    
	abenito@cpg3:~$ ls materiales-bio-python/
	data  ejercicios  labs	LICENSE  README.md  soluciones
    
Y si es algo desconocido, se produce un error:
    
	abenito@cpg3:~$ ls noexiste
	ls: no se puede acceder a 'noexiste': No existe el fichero o el directorio
    
Las rutas que se indican pueden ser absolutas o relativas.  
      
Movámonos un poco. Para movernos (cambiar el directorio de trabajo), se usa la orden `cd`, que son las siglas de _change directory_:
    
	abenito@cpg3:~$ pwd
	/home/abenito
	abenito@cpg3:~$ cd ..
	abenito@cpg3:/home$ pwd
	/home
    
Nos hemos movido al directorio padre del directorio de conexión con los dos puntos (`..`). Podríamos haber conseguido el mismo efecto con `cd /home`  
      
Curioseemos... ¿qué más usuarios habrá?
    

	abenito@cpg3:/home$ ls
	abenito       alejandro    arqcarmel	 giselcp	    jorgeruizramirez	      laudupri		   msandreu   seqview_user
	adrianambroa  alumnos.tar  carlosp	 grader-python-bio  josanc		      lauraalvarezalvarez  rafalopez  theron
	agarmar       amptoboso    elenanavarro  gualtierolugato    jupyterhub_cookie_secret  lihuengd		   rodri      verogmartos
	alba	      anaromero    eval_user	 jibri		    jupyterhub.sqlite	      lost+found	   sagoji
    
Vosotros, en vuestra cuenta, veréis qué otros alumnos hay (al menos, sus directorios de conexión) existen. Si nos perdemos, podemos volver a nuestro directorio de conexión (a _nuestra casa_), simplemente tecleando `cd`:
    
    abenito@cpg3:/home$ cd
	abenito@cpg3:~$
    
Probad a crear un directorio nuevo en vuestra cuenta. La orden es `mkdir`:
    
	abenito@cpg3:~$ mkdir PRUEBA
	abenito@cpg3:~$ ls
	certs			  materiales-bio-python
	cpg3.der.usal.es.ssl	  materiales-informatica-i
	genomes			  notebooks
	home.tar.gz		  PRUEBA
	informatica-i		  ps1
	informatica-i-old	  python-bio
	jupyterhub_config.py	  sorteo
	jupyterhub_config.py.bak  visualization-curriculum
	jupyterhub.log
	abenito@cpg3:~$ cd PRUEBA/
	abenito@cpg3:~/PRUEBA$ ls
	abenito@cpg3:~/PRUEBA$ cd ..
    
Si no os gusta cómo os ha quedado, lo borráis con `rmdir`, pero recordad que debe estar completamente vacío, incluso de ficheros ocultos:
    
    abenito@cpg3:~$ rmdir PRUEBA
    
### 6. Ejercicio
    
    Desde vuestro directorio de conexión, tratad de moveros a los siguientes directorios, adivinad a dónde habéis llegado y comprobadlo con `pwd`:
    1.  `/usr/bin`
    2.  `usr/bin`
    3.  `..`
    4.  `/usr/./bin`
    5.  `/usr/.bin`
    6.  `./.././..`
    7.  `/./.././..`
   
### 7. ¿Qué hay de lo mío?
    
Si se os pasa por la cabeza intentar curiosear en los ficheros de otro usuario, la cosa no es tan fácil. Veamos el directorio de conexión del usuario alejandro. `finger` nos viene al pelo:
    
	abenito@cpg3:~$ finger alejandro
	Login: alejandro      			Name: ""
	Directory: /home/alejandro          	Shell: /bin/bash
	On since Mon Jan 10 11:22 (CET) on pts/17 from 212.128.183.13
	   47 seconds idle
	No mail.
	No Plan.
    
Su directorio de conexión aparece a continuación de la etiqueta `Directory`: `/home/alejandro`. Vamos a intentar entrar en él:
    
    abenito@cpg3:~$ cd /home/alejandro/
	-bash: cd: /home/alejandro/: Permiso denegado
    
¡Vaya! El servidor que no tenemos permisos...¡una pena! En un servidor UNIX, los dueños de ficheros y directorios deciden quiénes pueden hacer qué cosas con ellos. Podemos ver los permisos que tiene un fichero o directorio con la opción `-l` de la orden `ls`:
    
    abenito@cpg3:~$ ls -l /home/alejandro/
	ls: no se puede abrir el directorio '/home/alejandro/': Permiso denegado
    
Pero no nos da permiso porque `ls`, al ser un directorio, trata de ver lo que hay dentro y no tenemos permisos. Debemos pedirle que nos dé la información del propio directorio y no de su contenido. Lo logramos con la opción `-d`:
    
    abenito@cpg3:~$ ls -ld /home/alejandro/
	drwxr-x--- 9 alejandro alejandro 4096 nov 17 11:56 /home/alejandro/
    
    `ls` nos da mucha información del fichero/directorio:
    
1.  El primer carácter nos dice qué tipo de objeto es. "`d`" significa que es un directorio, "`-`", que es un fichero. Y hay más tipos, que iréis aprendiendo.
2.  Los nueve siguientes caracteres nos muestra los permisos que tiene el objeto. Se dividen en tres partes, de tres caracteres cada una:
	1.  Los tres primeros son los permisos que tiene el dueño del fichero
	2.  Los tres siguientes muestran los permisos que tiene el grupo al que pertenece el fichero
	3.  Los tres últimos son los permisos que tienen el resto de usuarios
        
Cada una de las tres letras, indican un tipo de permiso. Un guion (`-`) quiere decir que no se tiene permiso. El significado de las letras depende del tipo de objeto. Para los __ficheros__:
        
- `r`: permiso para leer el fichero (_read_)
- `w`: permiso para escribir en el fichero (_write_)
- `x`: permiso para ejecutar el fichero (_execute_)
        
Sin embargo, si se trata de un __directorio__, el significado es:
        
- `r`: permiso para ver qué ficheros hay dentro del directorio
- `w`: permiso para borrar o renombrar o mover los ficheros que hay dentro del directorio
- `x`: permiso para moverse al directorio con la orden `cd` que hemos visto
        
Como vemos, el usuario `alejandro` es un tanto celoso de su privacidad. Se deja a sí mismo hacer todo (`rwx`), a los miembros del grupo `alejandro` leer y moverse al directorio (`r-x`) y a los demás, nada de nada (`---`).

3.  El significado del siguiente número (24), lo veremos más adelante
4.  A continuación, viene el nombre del propietario del fichero (alejandro)
5.  Después, el grupo al que pertenece el fichero (alejandro)
6.  El número que viene a continuación, es el tamaño en bytes que tiene el fichero o directorio
7.  Acto seguido aparece la fecha en que se modificó el contenido del fichero o directorio
8.  Finalmente, el nombre del fichero o directorio
    
Está claro el porqué no podíamos acceder a él. Solamente si el dueño nos da permiso, podremos acceder. ¿Cómo se puede hacer esto? Veamos una orden relacionada con la propiedad en UNIX.  
      
Vamos a crear un directorio de prueba y vamos a cambiarle sus permisos. Primero lo creamos y vemos qué permisos tiene:
    
	abenito@cpg3:~$ cd
	abenito@cpg3:~$ mkdir PRUEBA
	abenito@cpg3:~$ ls -ld PRUEBA/
	drwxr-xr-x 2 abenito abenito 4096 ene 10 12:32 PRUEBA/
    
Vemos que, si no hacemos nada, tenemos todos los permisos en nuestro nuevo directorio. Tanto los usuarios de nuestro grupo como los demás pueden acceder y ver el contenido del directorio, pero no borrar ni renombrar sus ficheros. Para cambiar los permisos del fichero se usa la orden `chmod`. En su primer parámetro pondremos (codificados) los permisos que queremos que tenga el fichero y el segundo parámetro es el nombre del fichero o directorio. El código es muy fácil. Consta de tres cifras, una para cada grupo de permisos (dueño, grupo y demás). Las cifras se calculan mediante una suma:
    
    1.  Partimos de cero
    2.  Sumamos cuatro, si queremos dar el permiso `r`
    3.  Sumamos dos, si queremos dar el permiso `w`
    4.  Finalmente, sumamos uno, si queremos dar el permiso `x`
    
Cambiemos los permisos de nuestro flamante directorio PRUEBA. Como somos muy generosos, nos vamos a quitar todos los permisos, vamos a dejar los permisos que tiene el grupo y vamos a dar todos los permisos a los demás. Siguiendo el procedimiento indicado más arriba, la primera cifra es 0 (ningún permiso), la segunda es 5 (permisos `r` y `x`) y la tercera es 7 (todos los permisos). Hagámoslo:
    
    abenito@cpg3:~$ chmod 057 PRUEBA
	abenito@cpg3:~$ ls -ld PRUEBA/
	d---r-xrwx 2 abenito abenito 4096 ene 10 12:32 PRUEBA/
    
Vamos a intentar ahora entrar en \*nuestro\* directorio:
    
    abenito@cpg3:~$ cd PRUEBA/
	-bash: cd: PRUEBA/: Permiso denegado
    
La verdad, tener un directorio así no es muy útil. Así que lo borramos con `rmdir`.
      
    
En realidad, si somos algo más técnicos deberíamos decir que los permisos son un campo de bits que, cuando se expresa en octal (base 8), hace que la última cifra trate de los permisos de los otros, la penúltima de los permisos del grupo y la antepenúltima de los permisos del dueño del fichero o directorio.  
      
Hay otra sintaxis más flexible de la misma orden `chmod` para cambiar los permisos. Si estáis interesados, podéis consultar la documentación de la propia orden. Algún ejemplo:
	- Dar permiso de ejecución a todos: a+x 
	- Quitar permiso de ejecución a todos: a-x
	- Dar permiso de lectura al grupo: g+r
	- Dar permiso de escritura al propietario: o+w
      
Existen órdenes en UNIX para cambiar el dueño (_regalar_) un fichero (`chown`) y el grupo al que pertenece un fichero (`chgrp`), pero por seguridad suelen estar restringidas a usuarios "normales". 
      
Existe tradicionalmente un usuario de UNIX, cuyo nombre es _root_, que puede hacer de todo. En el servidor puede también cambiar usuarios y grupos y puede saltarse todos los permisos que tengan los ficheros y directorios. El nombre de root proviene de que su directorio de conexión es tradicionalmente el directorio raíz (`/`). Si os esforzáis y aprendéis bien a administrar sistemas, algún día vosotras también llegaréis a ser root. 
      
El mecanismo de permisos de UNIX muchas veces se queda corto. Por ejemplo, podríais querer dejar entrar y ver los ficheros de vuestro directorio de conexión a un compañero. En la configuración clásica de UNIX no podéis. Si estáis interesadas en una mayor flexibilidad en la cesión de permisos, debe consultar las [_listas de control de acceso_] (https://es.linux-console.net/?p=1110), aunque no es un mecanismo igualmente estandarizado en todos los tipos de UNIX.
    
    
### Hacer ejercicio 1
   

### Limpiando
Si llega un momento en el que os agobiáis al ver tantos caracteres en el terminal, podéis encontrar el Zen de nuevo usando la orden `clear`. ¡Mano de santo!

### ¿Quién me puede ayudar?
    
Son tantas las órdenes de UNIX y tantas sus opciones que es improbable que nadie las controle todas. ¿Cómo puedo pedir ayuda al sistema? Existe una orden que nos ofrece documentación acerca de cualquier otra orden. Se llama `man`. Para asustarnos un poco, veamos el inicio de la página de manual de `ls`:
    
	abenito@cpg3:~$ man ls
	LS(1)

	NOMBRE
       ls, dir, vdir - listan los contenidos de directorios

	SINOPSIS
       ls [opciones] [fichero...]
       dir [fichero...]
       vdir [fichero...]

       Opciones de POSIX: [-CFRacdilqrtu1]

       Opciones  de  GNU  (en  la  forma  más  corta):  [-1abcdfghiklmnopqrstuvwxABCDFGHLNQRSUX]  [-w  cols]  [-T cols] [-I patrón] [--full-time] [--show-control-chars]
       [--block-size=tamaño] [--format={long,verbose,commas,across,vertical,single-column}] [--sort={none,time,size,extension}] [--time={atime,access,use,ctime,status}]
       [--color[={none,auto,always}]] [--help] [--version] [--]
    **\--More--(2%)**
    
Podéis contar hasta 31 opciones. Las páginas de manual de UNIX tienen fama de ser muy completas. Están organizadas en secciones, de las cuales, la primera es la que nos interesa. En ella se encuentras las órdenes que vamos a ver.  
      
A veces, el problema es que no recordamos cómo se llama la orden que hacía según qué cosa. Una opción de `man`, `-k` nos permite hacer una búsqueda por términos. Imagina que no te acuerdas de la orden que se usa para cambiar el propietario de un fichero:
    
	abenito@cpg3:~$ man -k owner
	cargo-owner (1)      - Manage the owners of a crate on the registry
	chgrp (1)            - change group ownership
	chown (1)            - change file owner and group
	chown (2)            - change ownership of a file
	chown32 (2)          - change ownership of a file
	dpkg-statoverride (1) - override ownership and mode of files
	faked (1)            - daemon that remembers fake ownership/permissions of files manipulated by fakeroot processes.
	faked-sysv (1)       - daemon that remembers fake ownership/permissions of files manipulated by fakeroot processes.
	faked-tcp (1)        - daemon that remembers fake ownership/permissions of files manipulated by fakeroot processes.
	fchown (2)           - change ownership of a file
	fchown32 (2)         - change ownership of a file
	fchownat (2)         - change ownership of a file
	lchown (2)           - change ownership of a file
	lchown32 (2)         - change ownership of a file
	lspgpot (1)          - extracts the ownertrust values from PGP keyrings and list them in GnuPG ownertrust format.
	ownership (8)        - Compaq ownership tag retriever
	quot (8)             - summarize filesystem ownership
	std::adopt_lock_t (3cxx) - Assume the calling thread has already obtained mutex ownership and manage it.
	std::defer_lock_t (3cxx) - Do not acquire ownership of the mutex.
	std::owner_less (3cxx) - (unknown subject)
	std::try_to_lock_t (3cxx) - Try to acquire ownership of the mutex without blocking.
	XGetSelectionOwner (3) - manipulate window selection
	XSetSelectionOwner (3) - manipulate window selection
	XtDisownSelection (3) - set selection owner
	XtOwnSelection (3)   - set selection owner
	XtOwnSelectionIncremental (3) - set selection owner
	    
Ahí aparece la orden que buscamos, en la sección 1 del manual: `chown`. Se puede limitar la sección de manual donde se busque. Para más detalles, consultad la página de manual de la propia orden `man`.

### Hacer ejercicio 1

### 10. Edición de ficheros


Una de las tareas más habituales que realizaréis en el servidor es la edición de ficheros. Bien sea porque queréis cambiar un fichero de configuración, bien sea porque estáis programando en el servidor, bien por otra razón. Cuando querráis editar un fichero, no os vale cualquier editor de textos. Por ejemplo, si hacéis vuestro programa favorito con Word, el fichero resultante no se leerá en `nano` u otras herramientas. El formato .doc no es un formato de texto plano, es decir, se han incluido dentro del fichero códigos de formato para el tipo de letra, configuración del documento y demás. Necesitáis un editor de textos que no dé formato adicional a los ficheros que genere.

Una solución que siempre os va a funcionar cuando querráis editar un fichero del servidor consiste en tres sencillos pasos:

1. 	Descargar el fichero a vuestro ordenador local
2. 	Editarlo con vuestro editor favorito, de Linux o Windows
3. 	Volverlo a subir, una vez editado, al servidor

Aunque sencillo, el método explicado arriba no es muy recomendable, sobre todo para trabajo frecuente. Es muy fácil que se os olvide el tercer paso y, o bien perdáis información, o bien estéis trabajando en el servidor con una versión vieja del fichero, os falle por eso y no os deis cuenta.

Podéis utilizar el editor de textos gráfico que más os guste (Bloc de notas, TextEdit, gedit...), pero es importante que al menos aprendáis a manejar `nano`, que es un editor de textos orientado al shell y que está disponible en la mayoría de sistema UNIX (al menos lo está en CPG3/Debian).

El editor se puede invocar con `nano nombredefichero`.

### Hacer ejercicio 2

    
### 11. Ya está bien, ¿no?
    
Esta sesión de trabajo ha sido extensa, aunque no muy difícil y ya toca a su fin. Es muy conveniente que, si no os ha dado tiempo en clase, la completéis en casa.
      
Para salir del servidor, debéis hacerlo ordenadamente. Teclead para ello la orden `exit`.
    
### 12. Y esto, ¿lo puedo trabajar en casa?
    
Como mejor se aprende a manejar con soltura la interfaz de texto de UNIX es con la práctica. Es muy recomendable que os instaléis una versión de Linux en vuestro ordenador. Tratad de que coincida en el tipo con la que tenéis en clase, para facilitaros el manejo. Elegid, pues, una versión de Ubuntu ([http://www.ubuntu.com/](http://www.ubuntu.com/)). Si usáis Windows/Mac y no sois tan intrépidos como para arriesgaros a hacer una instalación final de Ubuntu en vuestros sistemas, os recomiendo usar VirtualBox para instalarla en una máquina virtual. Podéis seguir [este tutorial](https://osl.ugr.es/2020/09/29/como-instalar-ubuntu-en-virtual-box/).
      
Una vez la tengáis instalada, podéis practicar abriendo una sesión de terminal. Las órdenes del servidor y las de vuestro Linux serán muy similares, si no prácticamente iguales. Podéis incluso establecer vuestro locale al español y tener las páginas de manual en la lengua de Cervantes.  
      
Esta distribución de Linux funciona mediante paquetes de programas que podéis instalar sin más que tener conexión a internet. Desde vuestro terminal, para instalar el paquete de páginas de manual en español, no tenéis más que teclear:
    
	yo@miordenador\\:~$ sudo apt-get install manpages-es
    
Metéis vuestra contraseña, esperáis a que se descarguen e instalen y... ya está.  
      
Podéis descargaros de este modo toda una serie de paquetes: editores de texto, compiladores, juegos, navegadores, ... Todo ello gratis y legalmente. Linux (nombre cariñoso con el que conocemos al sistema GNU/Linux) y las aplicaciones que se distribuyen con él es _software libre_. Como hemos visto, esto significa que estos programas han sido desarrollados de un modo altruista por personas conectadas a través de Internet y ofrecidos a los demás. ¡Qué bueno!
      
    
### Órdenes de la shell vistas en esta sesión:
    
`whoami`: muestra el nombre del usuario
    
`groups`: imprime los grupos a los que pertenece el usuario
    
`id`: muestra los identificadores del usuario y del grupo
    
`hostname`: da el nombre del servidor
    
`pwd`: imprime el directorio de trabajo
    
`who`: muestra los usuarios que se encuentran conectados
    
`finger`: da información acerca del usuario
    
`write`: permite enviar mensajes a otro usuario
    
`mesg`: visualiza o permite cambiar el estado de recepción de los mensajes
    
`talk`: chat interactivo entre dos usuarios (no suele estar disponible)
    
`ls`: muestra el contenido de un directorio
    
`cd`: cambia el directorio de trabajo
    
`mkdir`: crea un nuevo directorio
    
`rmdir`: borra un directorio, que debe estar vacío
    
`chmod`: cambia los permisos de un fichero o directorio
    
`chown`: cambia el propietario de un fichero o directorio
    
`chgrp`: cambia el grupo al que pertenece el fichero
    
`man`: muestra la página de manual de una orden
    
`locale`: imprime los locales disponibles o la configuración actual
    
`exit`: nos desconecta del servidor
    
     
    
      
      

      
      