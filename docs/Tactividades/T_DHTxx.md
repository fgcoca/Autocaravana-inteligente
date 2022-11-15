# <FONT COLOR=#8B008B>Sensor de Temperatura y Humedad DHTxx</font>

## <FONT COLOR=#007575>**Conceptos incluidos**</font>

<font color=#FF00FF><b><font size=5>

* Estado de confort
* Textos

</font color></b></font size>

## <FONT COLOR=#007575>**DHTxx**</font>
El DHT11 es un modelo de sensor que permite realizar la medición simultánea de temperatura y humedad. Dispone de un procesador interno que es el encargado de realizar la medición entregando la información mediante una señal digital.

Se presenta en un encapsulado plástico típico de color azul. Sus principales características son:

* Rango de temperatura: 0 a 50ºC
* Precisión de la medida de temperatura: +/-2ºC
* Rango de humedad: 20 a 80%
* Precisión en la medida de humedad: +/-5%.
* Frecuencia de muestreo: 1 muestra por segundo (1 Hz)

El DHT11 es un sensor bastante limitado que podemos usar con fines de formación, pruebas, o en proyectos que realmente no requieran una medición precisa.

Si necesitamos mayor precisión y rango podemos recurrir al DHT22 que es de la misma familia y lo único que cambia es sus características y el precio. Sus características son:

* Rango de temperatura: -40 a 125ºC
* Precisión de la medida de temperatura: +/-0.5ºC
* Rango de humedad: 0 a 100%
* Precisión en la medida de humedad: +/-2 a 5%
* Frecuencia de muestreo: 2 muestras por segundo (2 Hz)

En la imagen siguiente vemos el aspecto de ambos sensores:

<center>

![Aspecto DHT11 y DHT22](../img/Tactividades/DHT/DHTxx.png)

*Aspecto DHT11 y DHT22*

</center>

## <FONT COLOR=#007575>Estado de confort</font>
En la web ARQUITECTURA & ENERGÍA podemos encontrar un artículo donde se nos explica con bastante profundad el tema del [corfort térmico](http://www.arquitecturayenergia.cl/home/el-confort-termico/).

Puede definirse confort térmico, o más propiamente comodidad higrotérmica, como la ausencia de malestar térmico. En fisiología, se dice que hay confort higrotérmico cuando no tienen que intervenir los mecanismos termorreguladores del cuerpo para una actividad sedentaria y con una indumentaria ligera. Esta situación puede registrarse mediante índices que no deben ser sobrepasados para que no se pongan en funcionamiento los sistemas termorreguladores (metabolismo, sudoración y otros).

En la imagen siguiente vemos los valores de temperatura y humedad que delimitan las zonas de confortabilidad.

<center>

![Confort térmico en función de temperatura y humedad](../img/Tactividades/DHT/zonas-confort.png)

*Confort térmico en función de temperatura y humedad*

</center>

Sobre el gráfico vamos a delimitar zonas de temperatura y humedad para establecer su color. Por motivos de simplicidad lo vamos a hacer delimitando zonas rectangulares, pero comprobamos que no cometemos grandes errores y para nuestro propósito nos sirve.

**1.- Zona Roja**: en la imagen siguiente tenemos delimitadas las zonas:

- Humedad Relativa: superior al 85% e inferior al 20%
- Temperatura: superior a 27ºC e inferior a 16ºC

<center>

![Delimitación color rojo zona de confort ](../img/Tactividades/DHT/Confort-rojo.png)

*Delimitación color rojo zona de confort*

</center>

**2.- Zona Amarilla**: en la imagen siguiente tenemos delimitadas las zonas:

- Humedad Relativa: entre el 20% y el 40% y entre el 65% y el 85%
- Temperatura: entre 16ºC y 18ºC y entre 24ºC y 27ºC

<center>

![Delimitación color amarillo zona de confort ](../img/Tactividades/DHT/Confort-amarillo.png)

*Delimitación color amarillo zona de confort*

</center>

**3.- Zona Verde, rojo y amarillo**: en la imagen siguiente tenemos delimitadas todas las zonas, correspondiendo a la verde los siguientes datos:

- Humedad Relativa: entre el 40% y el 65%
- Temperatura: entre 18ºC y 24ºC

<center>

![Delimitación colores zona de confort ](../img/Tactividades/DHT/Confort-todos.png)

*Delimitación colores zona de confort*

</center>

Con este enlace al archivo [colores-A10.svg](../img/Tactividades/DHT/colores-A10.svg) puedes descargarte el archivo vectorial, editarlo con [Inkscape](https://inkscape.org/) y ver como se han realizado estos gráficos.

## <FONT COLOR=#007575>Bloques de texto</font>
Haremos un recorrido por los bloques del menú 'Texto' para ver las posibilidades que se nos presentan. Estos bloques serán los que usemos para mostrar información en dispositivos como la LCD, el monitor serie y otros dispositivos.

<center>

![Bloques del menú Texto](../img/Tactividades/DHT/bloques_texto.png)

*Bloques del menú Texto*

</center>

En la imagen siguiente vemos una breve explicación  de estos bloques de texto.

<center>

![Bloques de texto descritos](../img/Tactividades/DHT/bloques_textoE.png)

*Bloques de texto descritos*

</center>

Respecto a los códigos ASCII existen en la red multitud de páginas donde lo explican de forma muy clara.
