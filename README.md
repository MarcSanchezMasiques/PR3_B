# Pr3B: Procedimiento
Añadimos en el programa la libreria  BluetoothSerial :
```
#include "BluetoothSerial.h"
```
para habilitar las posibles conexiones con bluetooth, seguidamente comprobamos si se encuentra habilitado:
```
#if !defined(CONFIG_BT_ENABLED) || !defined(CONFIG_BLUEDROID_ENABLED)
#error Bluetooth is not enabled! Please run `make menuconfig` to and enable it
#endif
```
A continuación crea una instancia de BluetoothSerial llamada SerialBT :
```
BluetoothSerial SerialBT;
```
El programa lo seguimos con el void setup(), en nuestro caso(igual que en las otras practicas) inicializamos el proceso con 115200 bauds:
```
Serial.begin(115200);
```
Despues de realizar las comprovaciones necesarias continuamos realizando la conexión utilizando el ESP32test:
```
SerialBT.begin("ESP32test");
```
Por ultimo imprimimos por pantalla que es emparejable por BT:
```
Serial.println("The device started, now you can pair it with bluetooth!");
}
```
Por ultimo creamos un loop donde añadiremos 2 IFs, en el primero comprobaremos que esta recibiendo bytes de forma correcta
```
if (Serial.available()) {
SerialBT.write(Serial.read());
}
```
Y en el segundo if comprovaremos si estan estos bytes disponibles y, si es asi, lo imprimiremos por pantalla
```
if (SerialBT.available()) {
Serial.write(SerialBT.read());
}
```
```
delay(20);
```

### Resultado de la simulación
Como resultado final, podemos enviar mensajes através del del dispositivo secundario y podremos ver esos mensajes impresos por el terminal, los cuales estan siendo recibidos por la misma placa.