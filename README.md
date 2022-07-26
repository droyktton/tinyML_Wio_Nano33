# tinyML_Wio_Nano33
Un tutorial para empezar a programar las placas Wio Terminal and Nano 33 BLE Sense usando Edge Impulse

<!-----

You have some errors, warnings, or alerts. If you are using reckless mode, turn it off to see inline alerts.
* ERRORs: 0
* WARNINGs: 0
* ALERTS: 27

Conversion time: 6.541 seconds.


Using this Markdown file:

1. Paste this output into your source file.
2. See the notes and action items below regarding this conversion run.
3. Check the rendered output (headings, lists, code blocks, tables) for proper
   formatting and use a linkchecker before you publish this page.

Conversion notes:

* Docs to Markdown version 1.0β33
* Tue Jul 26 2022 14:45:51 GMT-0700 (PDT)
* Source doc: Edge Impulse with the Nano 33 BLE Sense y con Wio Terminal
* This document has images: check for >>>>>  gd2md-html alert:  inline image link in generated source and store images to your server. NOTE: Images in exported zip file from Google Docs may not appear in  the same order as they do in your doc. Please check the images!


WARNING:
You have 2 H1 headings. You may want to use the "H1 -> H2" option to demote all headings by one level.

----->


<p style="color: red; font-weight: bold">>>>>>  gd2md-html alert:  ERRORs: 0; WARNINGs: 1; ALERTS: 27.</p>
<ul style="color: red; font-weight: bold"><li>See top comment block for details on ERRORs and WARNINGs. <li>In the converted Markdown or HTML, search for inline alerts that start with >>>>>  gd2md-html alert:  for specific instances that need correction.</ul>

<p style="color: red; font-weight: bold">Links to alert messages:</p><a href="#gdcalert1">alert1</a>
<a href="#gdcalert2">alert2</a>
<a href="#gdcalert3">alert3</a>
<a href="#gdcalert4">alert4</a>
<a href="#gdcalert5">alert5</a>
<a href="#gdcalert6">alert6</a>
<a href="#gdcalert7">alert7</a>
<a href="#gdcalert8">alert8</a>
<a href="#gdcalert9">alert9</a>
<a href="#gdcalert10">alert10</a>
<a href="#gdcalert11">alert11</a>
<a href="#gdcalert12">alert12</a>
<a href="#gdcalert13">alert13</a>
<a href="#gdcalert14">alert14</a>
<a href="#gdcalert15">alert15</a>
<a href="#gdcalert16">alert16</a>
<a href="#gdcalert17">alert17</a>
<a href="#gdcalert18">alert18</a>
<a href="#gdcalert19">alert19</a>
<a href="#gdcalert20">alert20</a>
<a href="#gdcalert21">alert21</a>
<a href="#gdcalert22">alert22</a>
<a href="#gdcalert23">alert23</a>
<a href="#gdcalert24">alert24</a>
<a href="#gdcalert25">alert25</a>
<a href="#gdcalert26">alert26</a>
<a href="#gdcalert27">alert27</a>

<p style="color: red; font-weight: bold">>>>>> PLEASE check and correct alert issues and delete this message and the inline alerts.<hr></p>



# TinyML4D Academic Network


# Centro Atómico Bariloche - Argentina


# 

<p id="gdcalert1" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image1.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert2">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image1.png "image_tooltip")



# Primeros pasos con Edge-Impulse usando Arduino nano 33 BLE Sense y Wio Terminal D51R

Este es un tutorial en castellano que esperamos sirva de guía para comenzar a entrenar modelos con Edge-Impulse (EI) usando los distintos sensores que encontramos en las placas Arduino Nano 33 BLE Sense (Nano) y Wio Terminal D51R (Wio), para luego implementarlos para que funcionen local y autónomamente en estas mismas placas. Está basado en los muchos tutoriales que ya existen en inglés, y está complementado con comentarios basados en la experiencia propia.

No nos detenemos en los detalles técnicos de las placas, ni en los detalles de implementación y optimización de las redes neuronales. De hecho en todos los casos optamos por usar simples ejemplos de clasificación usando las configuraciones típicas y sugeridas por defecto. Sí nos detendremos en los detalles prácticos que se refieren a cómo conectar las placas y cargarles programas con el Arduino IDE así como también  y enlazarlas con Edge-Impulse para usarlas como unidades de adquisición de datos interactivas, y como dispositivos para hacer el “deployment” final, usando también Arduino IDE y la librería generada por EI. 


## Objetivos



1. Adquirir datos para entrenamiento y testeo con las placas Nano y Wio. 
2. Generar features y entrenar una red neuronal sencilla con ellos. 
3. Generar la librería de Tiny ML para la plataforma de Arduino IDE. 
4. Customizar mínimamente un código de ejemplo de la librería para comunicar  en tiempo real (visual o sonoramente) y/o registrar (en SD o en un dispositivo externo mediante cables, bluetooth o wifi) la clasificación en tiempo real, yendo más allá del típico ejemplo de monitor serial de Arduino IDE usando cable. 
5. Poner a prueba el dispositivo clasificando en forma local y en tiempo real en una prueba de campo.

      



## Requerimientos

Para avanzar con el tutorial supondremos que tenemos ya cuenta en Edge-Impulse y una mínima familiaridad con


     



* Las placas y sus partes.
* Los pasos para generar el procesamiento y entrenamiento de una red neuronal, usando por ejemplo sensores del teléfono celular. 
* El uso básico de Arduino IDE y su lenguaje de programación.


---


## Adquirir datos para Edge-Impulse con placas de desarrollo

Para adquirir es necesario instalar y correr dos scripts que nos permitirán enlazar nuestra placa, la Wio o la Nano u otra compatible, con EI, en la nube. 



1. [Edge Impulse CLI](https://docs.edgeimpulse.com/docs/cli-installation): 
2. Al instalar Node.js verificar que la versión instalada sea 14 o superior. apt-get en ubuntu puede instalar una inferior. Puede ser necesario instalar “curl” para seguir las instrucciones. 
3. $ curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash -
4. $ sudo apt-get install -y nodejs
5. $ node -v
6. En mi caso el último comando retorna v14.19.3.  Al hacer 
7. $ npm config get prefix
8. a mi me retorna “/usr/” en vez de “_/usr/local/_,” mencionado en el tutorial. De todas maneras hay que hacer
9. $ mkdir ~/.npm-global
10. $npm config set prefix '~/.npm-global'
11. $ echo 'export PATH=~/.npm-global/bin:$PATH' >> ~/.profile
12. No olvidar ponerlo en el path como está indicado. Para que tome efecto inmediatamente hacer
13. $ source ~/.profile” 
14. [Arduino CLI](https://arduino.github.io/arduino-cli/latest/): yo lo instale en mi $HOME/bin y me asegure que esté en el PATH (modificando el .bashrc o equivalente en linux). Por ejemplo haciendo 
15. $ echo 'export PATH=~/bin:$PATH' >> ~/.profile
16. $ source ~/.profile


---


# Placa nano 33 BLE Sense


## Material



* Computadora (laptop o desktop). 
* Plaquita Nano con su cable.
* Un teléfono celular con wifi y bluetooth.
* Conexión a internet.


## Familiarizarse con la placa usando Arduino IDE

Seguir todas las instrucciones del TinyML Kit Overview - HW and SW Installation & Test. 

Esto ya lo hicimos en la última clase del curso ICTP.

Instalar el board (un par de minutos)



* ArduinoTensorFlowLite (unos segundos, no confundir con otras libs..): soporte para la nano.
* TinyMLx (1 segundo): para hacer/probar ML.
* LSM9DS1 (1 segundo): para usar el IMU.
* ArduinoBLE (1 segundo): para comunicarnos vía bluetooth de baja energía con la placa.

Después de este paso uno debería poder compilar y correr todos los ejemplos del board nano 33 BLE y en particular los ejemplos de la librería  TinyMLx. _Lo más importante es que podemos modificar o extender esos ejemplos. _Así que propongo ejercicios...



* **Blink**: si compila pero no corre al hacer upload, verificar que el board sea la nano 33 BLE. Debería parpadear el led naranja de la izquierda, una vez por segundo. _Ejercicio_: cambiar el delay entre blinks a otra cosa, por ejemplo 10 segundos y verificar que funcione. O cambiar la proporción entre prendido y apagado.
* **Testing the microphone**: Si uno abre el serial monitor en vez del plotter, va a ver unas instrucciones. Si uno abre el plotter no se ven las instrucciones pero se puede mandar texto a la placa. El comando “click” deberia prender o pausar la medición. Si no funciona el “click” en el serial port, probar elegir “carriage return” o “both NL & CR” a la derecha. Sino, el boton negro de la derecha cumple la misma funcion de prender o pausar la medición. _Ejercicio_: Hacer que cuando una lectura supere los 100db, se pause la medición.
* **test_IMU:** Cargar y mirar los outputs en el serial monitor. Luego en el plotter, cambiando entre a, g, etc. _Ejercicio_: modificar el codigo para que además grafique el módulo cuadrado de la aceleración Ax^2+Ay^2+Az^2.
* **test_camara:** anda, pero lo que imprime en el serial monitor como single image capture, puede verse horrible, no solo por hexadecimal sino porque aparece como un solo chorizo de caracteres... al menos en mi linux. Copiar eso como dice el instructivo es imposible. Yo lo que hice es reformatear al output para que imprima en una columna y asi poder copiarlo y luego modificar el python para que lea eso. _Ejercicio_: hacer lo anterior, y probar el live streaming usando el código de processing.
* **LED via ble: **Este ejemplo permite prender un led vía bluetooth de baja energía. Para eso instalar “[LightBlue](https://play.google.com/store/apps/details?id=com.punchthrough.lightblueexplorer&hl=en&gl=US)” en el celular, para poder mandarle comandos a la placa desde ahí. _Ejercicio: _Modificar o aumentar el número de los comandos permitidos, y hacer que hagan otras cosas...

Notas: (1) si falla un ejemplo al hacer upload, chequear de no tener ningún serial monitor o plotter funcionando, si es así, cerrarlos y reintentar. También ayuda hacer doble click boton blanco (que diferencia hay con el boton negro?). (2) si uno modifica el código y quiere guardarlo tiene que cambiar de directorio, salir del de la librería. 

[https://docs.arduino.cc/tutorials/nano-33-ble-sense/edge-impulse](https://docs.arduino.cc/tutorials/nano-33-ble-sense/edge-impulse)


## Usar Edge Impulse con el celular

Sugiero hacer el ejemplo de clasificación usando el acelerómetro del celular.

Ejercicio: hacer el entrenamiento en (i) forma interactiva con EI, (ii) leyendo files previamente generados con el celu, y formateados adecuadamente.


## Conectar la placa nano 33 BLE a Edge Impulse

Flashear la plaquita con el último firmware. Los pasos son los siguientes



1. Bajar el último [Nano 33 BLE Sense board Edge Impulse firmware](https://cdn.edgeimpulse.com/firmware/arduino-nano-33-ble-sense.zip). Deszipear el archivo en alguna carpeta determinada en la computadora.
2. Apretar el botoncito blanco de la plaquita dos veces (no el del shield) y el led derecho titila lentamente...
3. Abrir el script flash que corresponda al sistema operativo que uno tenga (flash_windows.bat, flash_mac.command or flash_linux.sh).  En mi caso, que tengo Ubuntu, hice 

    **$ bash flash_linux.sh” **


    y todo anduvo bien (no hizo falta ser sudo).

4.  Hay que esperar a que se complete el proceso y luego apretar el boton de RESET, el blanco, una vez. Recordar que Una vez es para reiniciar, dos veces juntas es para que pare de hacer lo que está haciendo y preste atención...
5. En una terminal, lanzar el daemon para iniciar la comunicación,

        **$ edge-impulse-daemon --clean **


        Y si no está en el path, puede estar aquí, 


        **$ .npm-global/bin/edge-impulse-daemon --clean**

6. Seguir las instrucciones de pantalla para asociar la placa a una cuenta y a un proyecto de Edge Impulse (es necesario saber usuario y clave de la cuenta de Edge Impulse y el nombre del proyecto). No cerrar esta terminal ni Ctrl-C, ya que eso detiene la comunicación. Si todo sale bien, pasa esto:

    tmp$ edge-impulse-daemon --clean


    edge-impulse-daemon: command not found


    tmp$ 


    tmp$ 


    tmp$ ~/.npm-global/bin/edge-impulse-daemon --clean


    Edge Impulse serial daemon v1.14.12




    What is your user name or e-mail address (edgeimpulse.com)? xxxxxx@yyyyyy

    What is your password? [hidden]


<p id="gdcalert2" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: Definition term(s) &uarr;&uarr; missing definition? </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert3">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>







    Endpoints:


        Websocket: wss://remote-mgmt.edgeimpulse.com


        API:       https://studio.edgeimpulse.com/v1


        Ingestion: https://ingestion.edgeimpulse.com


    [SER] Connecting to /dev/ttyACM0


    [SER] Serial is connected, trying to read config...


    [SER] Clearing configuration


    [SER] Clearing configuration OK


    [SER] Retrieved configuration


    [SER] Device is running AT command version 1.6.0




    To which project do you want to connect this device? alejandro / minicursito-nano33BLE


<p id="gdcalert3" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: Definition term(s) &uarr;&uarr; missing definition? </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert4">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>







    Setting upload host in device... OK


    Configuring remote management settings... OK


    Configuring API key in device... OK


    Configuring HMAC key in device... OK


    [SER] Device is not connected to remote management API, will use daemon


    [WS ] Connecting to wss://remote-mgmt.edgeimpulse.com


    [WS ] Connected to wss://remote-mgmt.edgeimpulse.com




    What name do you want to give this device? D2:26:0E:25:DF:06


<p id="gdcalert4" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: Definition term(s) &uarr;&uarr; missing definition? </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert5">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>







    [WS ] Device "D2:26:0E:25:DF:06" is now connected to project "minicursito-nano33BLE"


        [WS ] Go to https://studio.edgeimpulse.com/studio/102859/acquisition/training to build your machine learning model!


        NO CERRAR ESTA TERMINAL. Fijense que en el medio pregunta el email y la clave asociados a EI, asi que tenerlas listas. Además pregunta a que proyecto uno quiere asociar la placa, asi que tener uno armado con un nombre reconocible.... 

7. Una vez en el proyecto asociado para este ejercicio, elegir en EI, “accelerometer data”, y ya estaríamos listos para adquirir, generar features, preparar el impulse, entrenar. Lo que ya hicimos varias veces, pero en vez de usar el teléfono para adquirir, usamos la plaquita. La diferencia es que ahora, en “collect data” en vez del mobile-phone usaremos la “fully supported development board”. Si todo salió bien con el daemon, en “devices” deberíamos tener

    

<p id="gdcalert5" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image2.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert6">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image2.png "image_tooltip")



    Si es así, ya estamos listos para adquirir datos con la Nano y mandarlos a la nube de EI.


Ejercicio:

Entrenemos una RN para que separe vibración vertical, label “VERTICAL”, de vibraciones horizontales, label “HORIZONTAL”.  

Vamos a  **DATA ACQUISITION **(MINICURSITO-NANO33BLE) y dejamos los settings por default. 

Solo cambiamos el label a “VERTICAL” por ej, y “Start Sampling” (y empezamos a transpirar). Luego repetimos con “HORIZONTAL”. Asi hasta tener muchos datos.

Luego quizás convenga mandar algunas muestras de cada tipo a test set.

En “impulse design” yo elegí lo típico 



<p id="gdcalert6" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image3.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert7">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image3.png "image_tooltip")


  

Save, y pasar a generar features, una por una. Mirar el grafico...

Ir a NN Classifier, y entrenar. Demora un ratito...

Luego ir a Anomaly Detection y entrenar... Si falla darle a “Select suggested axes” y train de nuevo. Demora un ratito...

It a “Live classification” y agitar de distintas formas la nano33BLE a ver que tal clasifica. 

Ir a “model testing” para ver que tan bien clasifica los test samples, así como los testing samples que acabamos de generar en la “live classification”.

Si todo anda bien podemos ir al deployment!!!

Es decir, generar un ejecutable o un código que podamos probar y modificar usando nuestra propia red neuronal ya entrenada. Ya no necesitamos más EI. Ahora es tomar datos, clasificarlos y ver cómo comunicar ese resultado.. Muchas posibilidades: serial con cable o con bluetooth, o bien prender leds, o hacer un ruidito... lo que venga. 


## Deployment

Vamos a deployment. Aquí hay muchas posibilidades. Una es crear un firmware, que es un ejecutable listo para poner en la plaquita, pero esto no nos da mucha flexibilidad. Mejor generar un código que podamos leer, modificar, compilar y correr. Es decir, crear una librería en algún lenguaje....



<p id="gdcalert7" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image4.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert8">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image4.png "image_tooltip")
 

Una librería en C++ podría andar para ejecutarla por ejemplo en la compu, y darle de comer archivos con datos sensados, o sensar datos con la compu. O incluso ponerla en una placa que no sea de Arduino.

Ejercicio: Hacer el deployment en el celu. Es decir, clasificar con el celu con la red entrenada con la nano33BLE!

Pero como lo que nos interesa es programar rápido y para la nano, lo mas facil es crear una libreria Arduino, asi que le damos a esa opcion. Elegimos ARDUINO y le damos al botón Build. Eso genera un zip que guardamos.

Abrimos el ArduinoIDE ahora y seguimos estas instrucciones



<p id="gdcalert8" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image5.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert9">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image5.png "image_tooltip")


Una vez instalada, podemos cargar un ejemplo que usa nuestra librería recién generada, como dice la ayuda de arriba. Podemos compilar la aplicación de acelerómetro, tarda un minuto mas o menos. Y luego la cargamos a la nano33BLE. 

Nota: Si no funciona la carga recordar cortar el daemon que se comunica con EI. Quizás hacer doble click en el botón de reset. Reintentar.

Si anda, ir a serial monitor, y empezar a agitar la plaquita, a ver si clasifica, en vivo! 

_Ejercicio:_



* Mirar el código, entender que hace cada parte...
* Modificar el código para que cuando la vibración sea VERTICAL parpadee el led builtin.
* Modificar el código para que transmita la clasificación por bluetooth. 
    * Estudiar [https://www.arduino.cc/reference/en/libraries/arduinoble/](https://www.arduino.cc/reference/en/libraries/arduinoble/) y agregarle al programa de clasificacion con acelerometro la comunicacion bluetooth de baja energia (esto es un deseo, no lo hice todavia)..


---


# Placa Wio terminal D51R


## Preparación

Para empezar vamos a seguir [estos pasos](https://wiki.seeedstudio.com/Wio-Terminal-Getting-Started/), que describimos y comentamos a continuación.

Para que el Arduino IDE encuentre las librerías necesarias para programar la Wio es necesario agregar en preferences [este URL](https://files.seeedstudio.com/arduino/package_seeeduino_boards_index.json) en el menú “File->Preferences” (o su equivalente en castellano), como se muestra en la captura de pantalla.



<p id="gdcalert9" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image6.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert10">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image6.png "image_tooltip")


Luego es necesario cerrar y volver a abrir Arduino IDE

Para usar la Wio debemos primero agregar en el Arduino IDE el board "Seeeduino Wio Terminal", en el menú “Tools->Board->Boards Manager”. En la búsqueda podemos poner “wio terminal” y clickear en “Install” el paquete “Seeed SAMD Board, version 1.8.3” (o la última versión que encontremos), como muestra la captura de pantalla.



<p id="gdcalert10" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image7.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert11">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image7.png "image_tooltip")


La instalación puede llevar unos minutos.

Para ver que la placa funcione correctamente es recomendable probar algún ejemplo que figura en el menú “Files->Examples->Seeed_xxxxx”. o cualquier ejemplo genérico (que anda en cualquier placa, empezando por los más simples, como “Blink”. Para la Wio hay otros ejemplos donde se usa su versátil pantalla.



---
Nota: 

Habrán notado que la Wio tiene precargado un lindo jueguito, que se parece al del  dinosaurio saltando obstáculos que aparece en el browser cuando no hay internet. Cuando 

carguen cualquier otro programa perderán ese juego, que se llama “jumper”. Para recuperarlo, lo  pueden encontrar [aquí](https://github.com/Seeed-Studio/Seeed_Arduino_Sketchbook/tree/master/examples/jumper).


---

 



---
Nota:

Al entrenar este processing block, que parece muy conveniente, no se como adaptarlo para que funcione en la wio (tira un error al compilar)



<p id="gdcalert11" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image8.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert12">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image8.png "image_tooltip")


por eso uso solamente spectral features.


---


## Adquirir datos con la Wio

Básicamente vamos a seguir [estos pasos](https://wiki.seeedstudio.com/Wio-Terminal-TinyML-EI-1/).

Lo primero que hay que hacer es poner la placa en modo “bootloader” y cargarle un firmware. Para ponerla en ese modo deslizamos dos veces seguidas y rápidamente el botón del costado de la Wio. El led azul debe parpadear lentamente... Entonces van a notar que se monta automáticamente una carpeta llamada “Arduino” (como si fuera un pendrive), con estos contenidos



<p id="gdcalert12" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image9.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert13">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image9.png "image_tooltip")


Luego uno debe ir a [este sitio](https://github.com/Seeed-Studio/Seeed_Arduino_edgeimpulse/releases/tag/1.4.0), obtener este archivo 



<p id="gdcalert13" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image10.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert14">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image10.png "image_tooltip")


y moverlo a la carpeta “Arduino”. Luego de eso, _automágicamente_ se cierra la carpeta Arduino.

Luego, si no lo hicieron ya para la Nano es necesario tener instalados:



17. [Edge Impulse CLI](https://docs.edgeimpulse.com/docs/cli-installation): Las instrucciones que siguen a “If it returns _/usr/local/_,” las tuve que seguir aunque a mi en realidad me retornaba “/usr/”
18. [Arduino CLI](https://arduino.github.io/arduino-cli/latest/): yo lo instale en mi $HOME/bin y me asegure que esté en el PATH (modificando el bashrc o equivalente en linux).

Ahora sí, podemos lanzar el daemon que enlaza con Edge-Impulse, como hicimos antes con la Nano. Si es la primera vez que vamos a lanzarlo debemos tener preparado usuario y contraseña de la cuenta en Edge-Impulse. En la línea de comandos tipear

$ edge-impulse-daemon

y si todo sale bien, se debería ver algo como lo siguiente (las primeras líneas contienen la parte interactiva con la identificación de usuario y contraseña, y la elección de proyecto al cual enlazarse, el nombre que le queremos poner al dispositivo, etc), 

 

<p id="gdcalert14" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image11.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert15">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image11.png "image_tooltip")


Si todo salió bien, ya podemos ir a Edge-Impulse a corroborar que sea un dispositivo conocido. Aparecerá con el nombre que decidimos ponerle, en nuestro caso simplemente “Wio”:



<p id="gdcalert15" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image12.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert16">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image12.png "image_tooltip")


Es importante no cerrar la terminal donde lanzamos el daemon, para seguir enlazados con EI y empezar a adquirir los datos de entrenamiento y test.

Luego, seguimos los pasos conocidos, como crear el impulse, entrenar, testear y finalmente hacer deployment en Arduino IDE, que termina con mensaje como este:



<p id="gdcalert16" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image13.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert17">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image13.png "image_tooltip")


indicando el nombre de la librería, y como cargar el ZIP de la misma en el Arduino IDE.

Podemos ya cerrar la terminal o hacer “Ctrl-C” en la misma para detener el daemon de edge-impulse-daemon, ya que no necesitamos más EI.


## Arduino IDE con la Wio

Para empezar abrimos Arduino-IDE y chequeamos la selección del puerto donde está la Wio. Luego de cargar la librería en “Sketch->Include Library->Add .ZIP Library”, ya podemos 

ya podemos acceder a los ejemplos de la librería recién instalada, en “File->Examples”. 

En nuestro caso están bajo el menú “Segundo_ejercicio_con_Wio_Terminal_Inferencing”. 

Como la red neuronal fue preparada para trabajar con datos del acelerómetro abrimos el ejemplo “nano_33_ble_accelerometer”. Como el nombre lo indica, en realidad el código no fue confeccionado para la Wio sino para la Nano, y de hecho no va a compilar para la Wio. 

Por suerte solo hacen falta unas pocas modificaciones. La principal es la referida al IMU. 

También de paso podemos aprovechar para que la pantalla muestre de alguna manera y localmente la clasificación en tiempo real, así como lo hace el Serial Monitor.  Vamos a hacer eso entonces.

Para usar el acelerómetro en la Wio necesitamos LIS3DHTR.h, que lo conseguimos en el “Library Manager” como muestra la captura de pantalla.



<p id="gdcalert17" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image14.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert18">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image14.png "image_tooltip")


En el código hacemos esto



<p id="gdcalert18" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image15.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert19">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image15.png "image_tooltip")


Es decir, reemplazamos el header del IMU de la Nano por el header del IMU de la Wio, agregamos un header para usar la pantalla de la Wio, y lo que sigue es la declaración de dos objetos, uno para acceder al IMU y otro a la pantalla, respectivamente.

La función setup() debe ser modificada para inicializar el IMU de la Wio, después de comentar las líneas que inicializan la IMU de la Nano,



<p id="gdcalert19" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image16.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert20">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image16.png "image_tooltip")


La pantalla también tiene que ser inicializada en la función setup(), cosa que podemos hacer así:



<p id="gdcalert20" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image17.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert21">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image17.png "image_tooltip")


Con eso ya estamos listos. Podemos compilar el código y si todo sale bien cargarlo a la Wio y abrir el Serial Monitor para ver la clasificación en vivo. Pero antes de eso vamos a modificar un poco más el código para mostrar en pantalla la clasificación de alguna forma. 

Por ejemplo, si uno quiere que cuando el resultado “0” de la clasificación tenga un peso mayor a 0.8 se ponga la pantalla en verde y aparezca un texto que diga “Activa” en el medio, uno puede agregar, después de estas líneas del ejemplo



<p id="gdcalert21" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image18.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert22">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image18.png "image_tooltip")


lo siguiente



<p id="gdcalert22" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image19.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert23">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image19.png "image_tooltip")


Esto pone la pantalla en verde, elige un font para el texto, lo escribe en alguna posición dada, esperamos un poco para que se vea, y luego uno podría poner de nuevo la pantalla en blano o no (como está ahora comentado). Y poner otro texto avisando que vamos a medir de nuevo para realizar la siguiente clasificación. Uno podría agregar un bloque del mismo estilo para cada posible resultado de la clasificación. En nuestro caso conceptual, solo tenemos dos estados, “Activo” o “Inactivo”, así que solo hace falta agregar otro bloque parecido, cambiando “result.classification[0]” por “result.classification[1]” y los colores y textos acordemente. 

Listo, compilamos y cargamos el programa, y podemos ver algo como esto


## Comunicación usando BLE

Para usar BLE en la Wio Terminal vamos a seguir [este tutorial](https://wiki.seeedstudio.com/Wio-Terminal-Bluetooth-Overview/).

Primero tenemos que actualizar el firmware, siguiendo [estos pasos](https://wiki.seeedstudio.com/Wio-Terminal-Network-Overview/#update-the-wireless-core-firmware). Para eso descargamos la [última versión de github](https://github.com/Seeed-Studio/ambd_flash_tool) y entramos al directorio recién descargado

$ cd ambd_flash_tool

Primero borramos el antiguo firmware

$ python3 ambd_flash_tool.py erase

Esto puede demorar unos minutos... Luego cargamos el nuevo firmware

$ python3 ambd_flash_tool.py flash

Luego ya podemos instalar todas las librerías de comunicación WiFi y BLE que necesitaremos.



<p id="gdcalert23" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image20.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert24">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image20.png "image_tooltip")


Y para bluetooth harán falta otras más. 



<p id="gdcalert24" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image21.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert25">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image21.png "image_tooltip")


Aqui una captura de las de BLE, en el “Library Manager”



<p id="gdcalert25" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image22.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert26">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image22.png "image_tooltip")


Es importante también asegurarse en el “Board Manager” de tener la última versión del board Wio



<p id="gdcalert26" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image23.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert27">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image23.png "image_tooltip")



### Ejemplo “Wio Terminal Bluetooth”

Para probar si BLE funciona correctamente podemos probar el ejemplo que viene con la Wio, “WioTerminal_WebBluetooth”, que esta en Examples -> Seeed Arduino skectchbook -> WioTerminal_WebBluetooth. El ejemplo hace que la Wio actúe como BLE server (hay otros ejemplos para hacerla actual como BLE client).  

Compilarlo y cargar WioTerminal_WebBluetooth y abrir el Serial Monitor. En el Serial Monitor solo saldrá “start advertising” porque el programa instruye a la Wio a no medir nada hasta que alguien se conecte vía bluetooth a la red que es creada por la Wio llamada “Accelerometer”. Una vez conectados, ya podemos leer datos via BLE usando otro dispositivo con Bluetooth. Podemos usar por ejemplo una laptop con Linux y “[bluetoothctl](https://budimir.cc/2020/02/27/ble-on-linux-with-bluetoothctl/)” de [blueZ](http://www.bluez.org/) o más sencillamente “LightBlue” en el teléfono celular (disponibles en Google Play o App Store), u otros programas similares. Con estas aplicaciones podemos conectarnos a la red “Accelerometer” (ese es el nombre que está fijado en el programa y que debería aparecer cuando escanemos) y explorar los servicios y características que estos servers BLE brindan. Podremos identificar las brindadas por Wio comparando por ejemplo las UUID del código de Arduino y las leídas en el teléfono.  

Inmediatamente después de conectarnos con el teléfono veremos que en el Serial Monitor del Arduino IDE aparecen las aceleraciones en los tres ejes X,Y,Z, porque así está especificado en el programa: empezar a medir si hay un dispositivo apareado y conectado.

Para obtener esas mismas aceleraciones a demanda via BLE, en LightBlue veremos que hay mucha información sobre el dispositivo y más abajo figuran los servicios y características que ofrece. En este ejemplo solo aparece una, que es “Readable, Writable”. Apretamos la flechita y entramos a esa característica. Aparece más información, y más abajo, podemos apretar el botón de “READ AGAIN”. Por default el valor sale en hexadecimal, pero podemos cambiarlo más arriba a “UTF-8 String”. Leemos de nuevo, y ahora ya se debería ver como en el serial monitor. La diferencia es que los valores por BLE son a demanda, para economizar energía. Uno también podría modificar el ejemplo para que sean notificaciones cuando se detecten ciertos eventos, como cambios bruscos de algo, etc. 


### Comunicar clasificación EI via BLE

Con el anterior ejemplo estamos listos para modificar nuestro código de detección de movimiento. Para eso haremos que la Wio terminal funcione como server BLE para notificaciones de cambio de estado.

Para que anden las notificaciones hay que usar #include &lt;BLE2902.h>


---

Para visitar la tortuga el 16/6/2022



1. Instalar [LightBlue](https://play.google.com/store/apps/details?id=com.punchthrough.lightblueexplorer&hl=en&gl=US) en el celu.
2. Instalar estas en Arduino IDE



<p id="gdcalert27" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image24.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert28">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image24.png "image_tooltip")
      



3. Agregar ambos ZIPs como librerías en Arduino IDE
4. Agregar el zip como librería.
5. Abrir, compilar y cargar el programa “tortuga_wio.ino” que les envio.
6. Abrir LightBlue
7. Conectar a “Tortuga Wio”
8. Abrir la última característica, la que dice “Readable, Writeable, Notify”
9. Setear Data Format a “UTF-8 String”
10. Apretar “Read Again”, que se ve?
11. Mover la Wio, y apretar de nuevo “Read Again”, que se ve? 
12. Ahora apretar “Subscribe” y mover y dejar quieta la Wio, que ocurre?

OPCIONAL



13. Instalar librerías para [usar la SD](https://wiki.seeedstudio.com/Wio-Terminal-FS-Overview/)**<code>.</code></strong> Bajar los dos Seeed_Arduino_FS.zip y Seeed_Arduino_SFUD.zip y  el ZIP y agregarlo. Para bajarlos van al boton  “Code” de github.
14. En Written Values escribir cualquier cosa y mirar la TFT 
15. En Written Values escribir de nuevo cualquier cosa y mirar la TFT 
