<!---

This file is used to generate your project datasheet. Please fill in the information below and delete any unused
sections.

You can also include images in this folder and reference them in the markdown. Each image must be less than
512 kb in size, and the combined size of all images must be less than 1 MB.
-->

## How it works

El proyecto consiste en el diseño de un circuito Front end o interfaz para convertir a digital la señal proveniente de un sensor con salida en tiempo. La industria nos proporciona un sinfín de sensores para medir o monitorear diferentes variables físicas, dichos sensores pueden proporcionar su señal en diferentes formas, voltaje corriente, frecuencia, tiempo (ancho de pulso), entre otras. El bloque que se propone se enfoca en la conversión de tiempo (definido entre el pulso de start y stop) a un formato digital, también conocidos como circuitos TDC (Time to Digital Converter), para posteriormente enviarlo vía RS232 para que pueda ser monitoreado en una PC o dispositivo compatible con el protocolo RS232. 

En la figura 1 se muestra el diagrama a bloques del que se compone la aplicación, como se observa se compone de un bloque llamado **contadorTDC** el cual se encarga de realizar el conteo una vez que se recibe un pulso de entrada o señal de algun sensor, el dato generado se registra o almacena para posteriormente mediante el bloque **RS232_TX** enviarlo hacia la computadora.

Para que la aplicación funcione se crea una maquina de estados, la cual fungira como etapa de control teniendo el siguiente principio de funcionamiento cuando se active la señal o pulso se pasa a un estado que hace que se almacene el valor actual del contador, luego pasa a otro estado donde envia dicho dato al transmisor, luego pasa a otro estado que activa al transmisor para enviar el dato y luego a otro estado donde espera a que termine la transmisión y cuando ya termina la transmisión se regresa al estado inicial.

![](topTDC.png)
**Figura 1.** Diagrama a bloques del TDC.

Pines propuestos (3 entradas, 2 salidas) con breve descripción:

**Pulso/señal -> input**.- En este pin se conecta la señal que genera el pulso con el cual inicia el conteo del tiempo que tarda el dicho pulso para generar un dato digital que se tranmitirá mediante RS232.

**reset ->input**.- Elemento asíncrono que genera un reseto de la aplicación.

**clk ->input**.- Este elemento contiene la señal de reloj, la cual será de 50MHz.

**tx -> output**.- Pin por el cual se envía el dato digital convertido. 

**eot ->output**.- Pin por el cual se muestra un indicar de fin de transmisión.



## How to test

Las pruebas se realizaron en Modelsim en su versión gratuita, para ello se hizo una adecuación generando un pequeño modulo PWM dentro de la aplicación para simular lo que sería la señal de un sensor, para este caso se opto por generar cuatro valores de PWM los cuales generan cuatro valores distintos que se transmiten por RS232, en la figura 2 se muestra la primer combinación de PWM que corresponde a una combinación 00 y que genera un valor binario 00010011.

![](00.png)
**Figura 2.** Combinación 00 que genera un valor binario 00010011.

<!---
## External hardware

TDC
-->
