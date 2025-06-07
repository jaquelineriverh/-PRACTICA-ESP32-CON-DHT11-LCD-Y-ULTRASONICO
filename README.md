# -PRACTICA-ESP32-CON-DHT11-LCD-Y-ULTRASONICO
ESTE REPOSITORIO MUESTRA COMO PROGRAMAR CON DHT, LCD Y ULTRASONICO
## INTRODUCCION

### DESCRIPCION

La Esp32 la utilizamos en un entorno de adquision de datos, lo cual en esta practica ocuparemos un sensor (DTH11) para adquirir temperatura y humedad del entorno, al igual que un sensor ultrasonico para medir distancia; Cabe aclarar que esta practica se usara un simulador llamado WOKWI.
Se agregara asi mismo un LCD I2C para observar dichos datos en cada cierto tiempo.

## MATERIAL NECESARIO

Para realizar esta practica necesitas lo siguiente:

-[WOKWI](https://wokwi.com/)

-Tarjeta ESP 32

-Sensor DHT11

-LCD 16X2 (I2C)

-HC-SR04 ULTRASONIC Distance sensor

## INSTRUCCIONES

### Requisitos previos

Para poder usar este repositorio necesitas entrar a la plataforma [WOKWI](https://wokwi.com/)

### Instrucciones de preparación de entorno

1.Abrir la terminal de programación y colocar la siguente programación:

```
#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4
#include "DHTesp.h"
const int Trigger = 4;   //Pin digital 2 para el Trigger del sensor
const int Echo = 15;   //Pin digital 3 para el Echo del sensor
const int DHT_PIN = 16;
DHTesp dhtSensor;

LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

void setup() {
  Serial.begin(9600);//iniciailzamos la comunicación
  pinMode(Trigger, OUTPUT); //pin como salida
  pinMode(Echo, INPUT);  //pin como entrada
  digitalWrite(Trigger, LOW);//Inicializamos el pin con 0
  lcd.init();
  lcd.backlight();
   dhtSensor.setup(DHT_PIN, DHTesp::DHT22);
}

void loop()
{
TempAndHumidity  data = dhtSensor.getTempAndHumidity();
 
  long t; //timepo que demora en llegar el eco
  long d; //distancia en centimetros

  digitalWrite(Trigger, HIGH);
  delayMicroseconds(10);          //Enviamos un pulso de 10us
  digitalWrite(Trigger, LOW);
  
  t = pulseIn(Echo, HIGH); //obtenemos el ancho del pulso
  d = t/59;             //escalamos el tiempo a una distancia en cm
  
  Serial.print("Distancia: ");
  Serial.print(d);      //Enviamos serialmente el valor de la distancia
  Serial.print("cm");
  Serial.println();
  delay(1000);          //Hacemos una pausa de 100ms

  lcd.setCursor(0, 0);
  lcd.print("   DIPLOMADO");
  lcd.setCursor(0, 1); 
  lcd.print(" AUTOMATIZACION");
   delay(2000);
  lcd.clear();

   lcd.setCursor(0, 0);
  lcd.print(" JAQUELINE R.H");
  lcd.setCursor(0, 1); 
  lcd.print("   INDUSTRIAL");
   delay(2000);
  lcd.clear();
   lcd.setCursor(0, 0);
  lcd.print("   07-06-2025");
  delay(2000);
  lcd.clear();
  
  
  lcd.setCursor(0, 0);
  lcd.print("DISTANCIA: " + String(d) + "cm");
  
  delay(2000);
  lcd.clear();
  
  lcd.setCursor(0, 0);
  lcd.print("  Temp: " + String(data.temperature, 1) + "\xDF"+"C  ");
  lcd.setCursor(0, 1); 
  lcd.print(" Humidity: " + String(data.humidity, 1) + "% ");
 
  delay(1000);
  lcd.clear();
}
```


2.Instalar la libreria de DHT sensor library for ESPx como se muestra en la siguente imagen


![](https://github.com/jaquelineriverh/PRACTICA-ESP32-DHT11/blob/main/DHT.jpg)

3. Instalar la libreria de LiquidCrystal I2C como se muestra en la siguiente imagen



![](https://github.com/jaquelineriverh/PRACTICA-2-ESP32-CON-DHT11-Y-Lcd/blob/main/libreria%20liquid.png)



4.Hacer la conexion de DHT11 con la ESP32 como se muestra en la siguente imagen.

![]()


5.Hacer la conexion de LCD con la ESP32 como se muestra en la siguente imagen.


![]()

6.Hacer la conexion de HC-SR04 ULTRASONIC Distance sensor con la ESP32 como se muestra en la siguente imagen.

![]()

### Instrucciónes de operación
1.Iniciar simulador.

2.Visualizar los datos en el LCD 16x2.

3.Colocar la temperatura y humedad dando doble click al sensor DHT11

4. Colocar la distancia dando doble click al sensor ultrasonico

## Resultados

Cuando haya funcionado, verás los valores dentro del LCD 16x2 como se muestra en la siguente imagen.


![](https://github.com/jaquelineriverh/-PRACTICA-ESP32-CON-DHT11-LCD-Y-ULTRASONICO/blob/main/resultados%20para%20distancia.png)


![](

### Evidencias



# Créditos

Desarrollado por **RIVERA HERNANDEZ JAQUELINE**

-[GITHUB](https://github.com/jaquelineriverh)
