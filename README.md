# Control joystick con raspberry pi pico

# Tabla de contenidos
1. [Materiales](#Materiales)
2. [Descripción](#Descripción)
3. [Código](#Código)

## Materiales
* Raspberry pi pico
* Módulo joystick
* Protoboard
* Jumpers


## Descripción

El módulo joistick tiene 5 pines: VCC para alimentación, GND para tierra, Vx que nos da el valor del eje X, Vy que nos da el valor del eje Y y SW que es un push buttton. La salida X, Y es analógica, además, puede presionar el SW para activar la salida digital.

![Joystick](https://github.com/victorgjacobo/joystick_raspberry_pi_pico/assets/141197135/a0f17d79-9437-4cd0-bfeb-92a8d912be2c)


Es importante la posición del joystick, por ejemplo, en la imágen de abajo está totalmente a la izquierda, la salida analógica Vx que devuelve un 0 y cuando está totalmente a la derecha devuelve 1023. En el caso contrario, en la izquierda devuelve 1023 y en la derecha 0. Cuando se encuentra en una posición intermedia devuelve el número correspondiente a dicha posición, ya sea 512, 128, etc. 

![post66_face_sensor_joystick](https://github.com/victorgjacobo/joystick_raspberry_pi_pico/assets/141197135/033e482a-b3a8-4d3a-83c0-3ebd469b8a53)


En la figura de abajo se muestra la conexión del módulo joystick con la raspberry pi pico. Para capturar la señal del eje x `Vx -> GPIO 27`, para el eje y `Vy -> GPIO 26` y para el SW `SW -> GPIO 22`.

![joystick](https://github.com/victorgjacobo/joystick_raspberry_pi_pico/assets/141197135/ca3d8325-b6fe-44b8-afc8-7ca6abd2066b)


## Código
```python
"""
  Nombre de la práctica: Módulo joystick con 
  Raspberry Pi Pico
  Autor: Ing. Víctor González Jacobo
"""
from machine import Pin, ADC
from time import sleep

VRX = ADC(Pin(27))
VRY = ADC(Pin(26))
SW = Pin(22,Pin.IN, Pin.PULL_UP)

while True:
    xAxis = VRX.read_u16()
    yAxis = VRY.read_u16()
    switch = SW.value()
    
    print("X-axis: " + str(xAxis)) 
    print("Y-axis: " + str(yAxis))
    print("Switch " + str(switch))
    
    if switch == 0:
        print("Push button PRESIONADO !")
    print(" ")
    sleep(1)
```

![](https://img.shields.io/github/watchers/victorgjacobo/joystick_raspberry_pi_pico)
![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![Raspberry Pi](https://img.shields.io/badge/-RaspberryPi-C51A4A?style=for-the-badge&logo=Raspberry-Pi)
![GitHub followers](https://img.shields.io/github/followers/victorgjacobo)
