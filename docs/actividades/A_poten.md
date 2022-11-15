# <FONT COLOR=#8B008B>Actividades con el potenciómetro</font>

## <FONT COLOR=#007575>**Actividad A025**</font>

### <FONT COLOR=#AA0000>1. consola</font>
Vamos a guardar los datos leídos del potenciómetro en una variable y mostrarlos a través de la consola serie. El programa final queda como vemos en la figura siguiente y lo tenemos disponible en el enlace [Actividad MH-A025. Consola](../programas/MH-A025_1.abp).

<center>

![Solución A025. Consola](../img/actividades/A025_1.png)

*Solución A025. Consola*

</center>

Si cargamos el programa en nuestra placa y posteriormente activamos la consola y conectamos ArduinoBlocks con nuestro ordenador podemos ver un resultado similar al de la imagen siguiente que se corresponde con variaciones de extremo a extremo del potenciómetro.

<center>

![Aspecto de la consola](../img/actividades/A025_1C.png)

*Aspecto de la consola*

</center>

### <FONT COLOR=#AA0000>2. Mapeo de datos</font>
Vamos a modificar el programa de la parte 1 del reto para mapear los datos antes de enviarlos a la consola serie. El programa final queda como vemos en la figura siguiente y lo tenemos disponible en el enlace [Actividad MH-A025. Mapeo de datos](../programas/MH-A025_2.abp).

<center>

![Solución A025. Mapeo de datos](../img/actividades/A025_2.png)

*Solución A025. Mapeo de datos*

</center>

La consola mostrará un resultado similar al de la imagen siguiente que se corresponde con variaciones de extremo a extremo del potenciómetro.

<center>

![Aspecto de la consola](../img/actividades/A025_2C.png)

*Aspecto de la consola*

</center>

### <FONT COLOR=#AA0000>3. Serial plotter</font>
Vamos ahora a mapear y mostrar los datos leídos del potenciómetro en el Serial Plotter. El programa final queda como vemos en la figura siguiente y lo tenemos disponible en el enlace [Actividad MH-A025. Serial plotter](../programas/MH-A025_3.abp).

<center>

![Solución A025. Serial plotter](../img/actividades/A025_3.png)

*Solución A025. Mapeo de datos*

</center>

Si activamos el Serial Plotter y vamos variando el potenciometro veremos el resultado en el mismo, obteniendo algo similar a la imagen siguiente:

<center>

![Aspecto del serial plotter](../img/actividades/A025_3SP.png)

*Aspecto del serial plotter*

</center>

### <FONT COLOR=#AA0000>4. Datalogger</font>
Vamos ahora a activar el "comecocos" o datalogger, dejarlo unos instantes que registre datos, pararlo, guardar el archivo y abrirlo desde la hoja de cálculo LibreOffice Calc para ver los resultados. El programa final es el mismo que el de la actividad anterior. En la animación siguiente vemos el proceso de puesta en marcha y parada del datalogger. En el enlace tenemos el archivo CSV generado [Archivo CSV](../programas/A025_4.csv).

<center>

![Solución A025. Datalogger](../img/actividades/A025_4D.gif)

*Solución A025. Datalogger*

</center>

En la figura siguiente vemos el resultado de cargar ese archivo en Calc. Se ha añadido una gráfica para observar como es totalmente similar a la que vemos en el datalogger. Los datos y la gráfica se han dejado tal cual son de inicio y no se ha entrado en mas detalles de edición de los mismos.

<center>

![Archivo CSV en Calc](../img/actividades/A025_4CSV.png)

*Archivo CSV en Calc*

</center>

## <FONT COLOR=#007575>Propuestas</font>

* Repetir la actividad A025 configurando el bloque potenciómetro en porcentaje.
* Realizar un control de los faros de la autocaravana mediante el potenciómetro dividiendo el rango total en 8 partes tal y como vemos en la tabla siguiente:

<center>

| Color | Rango | R | G | B |
|---|:|:|:|:|
| Rojo | 0 a 127 | 255 | 0 | 0 |
| Verde | 128 a 255 | 0 | 255 | 0 |
| Azul | 256 a 384 | 0 | 0 | 255 |
| Amarillo | 385 a 512 | 255 | 255 | 0 |
| Cian | 513 a 640 | 0 | 255 | 255 |
| Magenta | 641 a 768 | 255 | 0 | 255 |
| Blanco | 769 a 896 | 255 | 255 | 255 |
| Naranja | 897 a 1023 | 255 | 127 | 0 |

</center>

* Repetir la actividad anterior mostrando el resultado por la consola.
* Realizar un programa con el sensor DHT11 que muestre los datos de temperatura y humedad en el serial plotter. Hacer un registro de datos con el datalogger y exportar los registros realizados.
