# <FONT COLOR=#8B008B>Puerto de expansión I2C. La LCD de 2x16</font>

## <FONT COLOR=#007575>**Conceptos incluidos**</font>

<font color=#FF00FF><b><font size=5>

* Las comunicaciones I2C

</font color></b></font size>

## <FONT COLOR=#007575>**El bus I2C**</font>
Las  siglas I2C corresponden en realidad a I²C que tiene su origen en las iniciales del inglés Inter-Integrated Circuit (IIC = I²C) y que siginifican Circuito Inter-Integrado) y vamos a explicar un poco en que consiste este sistema de conexionado.

El bus conocido por las siglas I2C, IIC o I²C, es un bus serie de datos desarrollado en 1982 por Philips Semiconductors (hoy NXP Semiconductors, parte de Qualcomm). Se utiliza principalmente internamente para la comunicación entre diferentes partes de un circuito, por ejemplo, entre un controlador y circuitos periféricos integrados. Posteriormente fue adoptado progresivamente por otros fabricantes hasta convertirse en un estándar del mercado con miles de circuitos integrados de diferentes fabricantes.

I2C también se denomina TWI (Two Wired Interface) únicamente por motivos de licencia, denominación introducida por Atmel. No obstante, la patente caducó en 2006, por lo que actualmente no hay restricción sobre el uso del término I2C.

El bus I2C requiere únicamente dos cables o lineas de señal para su funcionamiento, uno para la señal de reloj (SCL, Serial Clock) y otro para el envío de datos (SDA, Serial Data). Ambas líneas precisan resistencias de pull-up hacia Vcc. Cualquier dispositivo conectado a estas líneas es de drenador o colector abierto (Open Collector), lo cual en combinación con las resistencias pull-up, crea un circuito Wired-AND. En la imagen siguiente vemos el diagrama básico de conexionado del bus con algunos ejemplos de dispositivos. La señal de reloj siempre es generada por el circuito que actúa como Master.

<center>

![Diagrama de conexión del bus I2C](../img/Tactividades/LCD/diagrama-IIC.png)

*Diagrama de conexión del bus I2C*

</center>

Para ser reconocido en el bus, cada dispositivo dispone de una dirección física, que se emplea para acceder a cada uno de ellos de forma individual. Esta dirección puede ser fijada por hardware, en cuyo caso se pueden modificar los últimos 3 bits mediante “jumpers” o microinterruptores (ejemplo de la matriz de 8x8), o por software.

En general, cada dispositivo conectado al bus debe tener una dirección única. Si tenemos varios dispositivos similares tendremos que cambiar la dirección o, en caso de no ser posible, implementar un bus secundario.

El bus I2C tiene una arquitectura de tipo master-slave, lo que indica que el master es el encargado de controlar al resto de dispositivos tipo slave con los que se comunica y que se comunican con el, teniendo siempre el master prioridad absoluta. El dispositivo master es el que inicia la comunicación con los slaves. Los slaves no pueden iniciar la comunicación (el master tiene que preguntarles), ni hablar entre si directamente.

El bus I2C debe ser por lo tanto síncrono, es decir debe existir una señal de reloj que controle las comunicaciones. Es el master el que proporciona la señal de reloj, que mantiene sincronizados a todos los dispositivos del bus. De esta forma, se elimina la necesidad de que cada dispositivo tenga su propio reloj, de tener que acordar una velocidad de transmisión y mecanismos para mantener la transmisión sincronizada como en UART o SPI. En la imagen vemos un cronograma ejemplo del funcionamiento del sistema.

<center>

![Cronograma trabajo bus I2C](../img/Tactividades/LCD/crono-iic.png)

*Cronograma trabajo bus I2C*

</center>

El protocolo de comunicación I2C sigue la siguiente secuencia:

* Primero, el master genera la señal de reloj del bus (SCL).
* Se inicia la comunicación por orden del master al establecer la condición de START, que se produce cuando SDA pasa de uno a cero y se mantiene en cero durante un tiempo.
* El master direcciona a los slaves.
* El master indica si se va a leer o escribir.
* El slave direccionado responde con una señal de conformidad ACK (acknowledge).
* Se transmite los datos byte a byte desde SDA al receptor. Por cada pulso desde SCL se transmite un bit de información.
* El destinatario de la información responde con una señal de conformidad ACK.
* Se acaba la comunicación cuando el master establece la condición de STOP, que se produce cuando SDA, por orden del master pasa de cero a uno y se mantiene en uno durante un tiempo.

Son muchos los dispositivos I2C que se pueden direccionar por este bus I2C, siendo lo más común en los dispositivos para I2C que utilicen direcciones de 7 bits, aunque existen dispositivos de 10 bits, pero es un caso raro. Una dirección de 7 bits implica que se pueden poner hasta 128 (27) dispositivos sobre un bus I2C. Hemos visto que las direcciones son de 8 bits y esto es porque el bit extra de los 7 de la dirección lo emplea el master para informar al slave si va a leer o escribir. Si el bit de lectura/escritura es cero, el dispositivo master está escribiendo en el slave. Si el bit es 1 el master está leyendo desde el slave. La dirección de 7 bit se coloca en los 7 bits más significativos del byte y el bit de lectura/escritura es el bit menos significativo.

## <FONT COLOR=#007575>La LCD 1602</font>
Una pantalla LCD (del ingés, Liquid Cristal Display) de 2 líneas de 16 caracteres tiene el aspecto y la distribución de pines que vemos en la imagen siguiente.

<center>

![LCD 2x16](../img/Tactividades/LCD/16x2.png)

*LCD 2x16*

</center>

Es evidente que deberíamos utilizar bastantes patillas de nuestra placa para su control. En la imagen siguiente se muestra el conexionado mínimo necesario en una pantalla de este tipo para una placa tipo UNO: 4 bits para datos y dos señales de control En (Enable) y Rs (Register select). La conexión RW la ponemos a GND. Además se debe añadir una resistencia ajustable o un potenciómetro para regular el contraste de la pantalla.

<center>

![Conexionado mínimo LCD 2x16](../img/Tactividades/LCD/Conex-LCD.png)

*Conexionado mínimo LCD 2x16*

</center>

Es preferible utilizar alguna de las que tienen el aspecto que vemos en la imagen siguiente:

<center>

![LCD 2x16 con módulo I2C](../img/Tactividades/LCD/16x2-i2c.png)

*LCD 2x16 con módulo I2C*

</center>

En realidad el conjunto que vemos en la imagen anterior no es mas que una LCD 2x16 a la que se ha incorporado un módulo adaptador de LCD a I2C. Este modulo está especialmente diseñado para poder soldarlo directamente a la LCD y convertirla así en un dispositivo I2C que además ya lleva incorporado el potenciómetro de ajuste de contraste en alguno de los casos.

Este tipo de pantalla requiere cuatro cables para establecer las conexiones, dos cables SDA (datos) y SCL (reloj) para el bus de comunicaciones I2C y los dos cables de alimentación VCC y GND.

La dirección I2C por defecto de este tipo de módulos puede ser 0x3F o en otros casos 0x27, e incluso hay modelos en los que se puede cambiar. Para un correcto control es muy importante identificar correctamente la dirección I2C de nuestro modulo pues de otra forma nuestro programa no funcionará correctamente.

Una LCD 1602 I2C es muy sencilla de controlar a partir de los bloques que nos proporciona ArduinoBlocks. En la imagen siguiente ponemos como ejemplo los bloques para imprimir un texto o variable en un par fila-columna determinado.

<center>

![Bloques para imprimir en un par fila-columna](../img/Tactividades/LCD/bloques-impresion-x-y.png)

*Bloques para imprimir en un par fila-columna*

</center>

 En la siguiente figura se muestra el sistema de distribución de filas y columnas.

<center>

![Sistema de coordenadas en una LCD 1602](../img/Tactividades/LCD/sistema-x-y.png)

*Sistema de coordenadas en una LCD 1602*

</center>

## <FONT COLOR=#007575>Escanear dispositivos I2C</font>
Si no conocemos la dirección especifica de nuestro módulo podemos utilizar un pequeño programa que llamaremos [Escaner-I2C](../programas/Escaner-I2C.abp) y que se encargará de identificar la dirección I2C y todos los dispositivos I2C conectados a nuestra placa. El bloque "Escanear dispositivos I2C..." está disponible en el menú I2C tal y como vemos en la imagen siguiente:

<center>

![Menu I2C](../img/Tactividades/LCD/menu-I2C.png)

*Menu I2C*

</center>

Un sencillo programa como el de la imagen siguiente nos permite ver los dispositivos I2C conectados y su dirección física asociada. El programa está disponible como [Escaner-I2C](./programas/Escaner-I2C.abp).

<center>

![Programa Escaner-I2C](../img/Tactividades/LCD/Escaner-I2C.png)

*Programa Escaner-I2C*

</center>

Si conectamos la consola el resultado de tener la autocaravana con una LCD I2C conectada debe ser similar al de la imagen siguiente:

<center>

![Consola para el programa Escaner-I2C](../img/Tactividades/LCD/Consola-Escaner-I2C.png)

*Consola para el programa Escaner-I2C*

</center>

En la figura siguiente tenemos el resultado que se muestra con el programa anterior cargado, conectar la consola y hacer reset. En este caso vemos los cinco dispositivos conectados a través de un hub.

<center>

![Consola para el programa Escaner-I2C con 5 dispositivos](../img/Tactividades/LCD/Consola-Escaner-I2C-5.png)

*Consola para el programa Escaner-I2C con 5 dispositivos*

</center>

Otra opción para hacer un escáner I2C que no necesita el reset es el programa que vemos en la figura siguiente y que lleva al bucle la orden de escaneo que se va a ejecutar cada 10 segundos, aunque este tiempo puede ser otro cualquiera.

<center>

![Programa Escaner-I2C en el bucle con 5 dispositivos](../img/Tactividades/LCD/Escaner-I2C-bucle.png)

*Programa Escaner-I2C en el bucle con 5 dispositivos*

</center>

En la figura siguiente vemos el resultado en la consola y como coincide con el anterior.

<center>

![Consola para el programa Escaner-I2C en el bucle con 5 dispositivos](../img/Tactividades/LCD/Consola-Escaner-I2C-5-bucle.png)

*Consola para el programa Escaner-I2C en el bucle con 5 dispositivos*

</center>

## <FONT COLOR=#007575>Cambiar la dirección física del dispositivo I2C</font>
Esta tarea nos va a resultar especialmente útil si disponemos de LCDs I2C con una dirección fijada de fábrica y queremos conectar varias de ellas en nuestro proyecto.

* **LCD SIN micro interruptores**

La parte posterior de la LCD 1602 de Keyestudio tiene el aspecto de la imagen siguiente. Nos fijaremos especialmente en los tres grupos de agujeros enmarcados en rojo. Aunque en este caso no vienen nombrados los vamos a denominar A0, A1 y A2 de izquierda a derecha.

<center>

![Pads configuración dirección física en la parte posterior LCD I2C](../img/Tactividades/LCD/posterior.png)

*Pads configuración dirección física en la parte posterior LCD I2C*

</center>

La dirección por defecto de fábrica en este caso es la 0x27, pero se puede cambiar alterando la situación de conexionado de estos agujeros entre si según la tabla siguiente:

<center>

| A2 | A1 | A0 | Dirección |
|:|:|:|:|
| 0 | 0 | 0 | 0x27 |
| 0 | 0 | 1 | 0x26 |
| 0 | 1 | 0 | 0x25 |
| 0 | 1 | 1 | 0x24 |
| 1 | 0 | 0 | 0x23 |
| 1 | 0 | 1 | 0x22 |
| 1 | 1 | 0 | 0x21 |
| 1 | 1 | 1 | 0x20 |

</center>

Para establecer los unos de la tabla anterior basta con cortocircuitar los dos pads correspondientes. En la imagen siguiente se ha establecido la dirección física como 0x26.

<center>

![Dirección 0x26](../img/Tactividades/LCD/0x26.png)

*Dirección 0x26*

</center>

* **LCD CON micro interruptores**

La parte posterior de la LCD 1602 de Keyestudio con micro interruptores para cambiar su dirección física tiene el aspecto de la imagen siguiente. Nos fijaremos especialmente en el recuadro azul donde están los microinterruptores que permiten cambiar el estado del bit y encima de los mismo está la información de la dirección física que se asigna a cada combinación. La tabla es exactamente la misma que en el caso anterior.

<center>

![Configuración dirección física en la parte posterior LCD I2C con microinterruptores](../img/Tactividades/LCD/posterior-micro.png)

*Configuración dirección física en la parte posterior LCD I2C con microinterruptores*

</center>

## <FONT COLOR=#007575>Definición de símbolos en la LCD</font>
Dentro de los bloques del menú Visualización -> Pantalla LCD está el de "definir símbolo", que permite definir uno de los 8 símbolos personalizables que puede almacenar el micro de la pantalla LCD. El símbolo se define por un mapa de bits (unos y ceros indicando cada píxel del símbolo). Los símbolos tienen una resolución de 5x8 píxeles (blanco o negro).

En ArduinoBlocks disponemos de una herramienta que nos ayuda a definir nuestros propios símbolos y podemos acceder a ella desde herramientas o haciendo clic derecho sobre el bloque, desplegándose en cualquier caso un editor muy sencillo de usar y que vemos con un ejemplo en la imagen en la siguiente:

<center>

![Ejemplo de símbolo creado con el editor](../img/Tactividades/LCD/Editor-simbolos.png)

*Ejemplo de símbolo creado con el editor*

</center>

Para tener el símbolo disponible simplemente copiamos la cadena generada en el lugar correspondiente del bloque que vemos en la imagen siguiente.

<center>

![Bloque para la definición de símbolos](../img/Tactividades/LCD/bloque-simbolo.png)

*Bloque para la definición de símbolos*

</center>
