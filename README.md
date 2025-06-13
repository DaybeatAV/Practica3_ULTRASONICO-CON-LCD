# Practica 3 ULTRASONICO CON LCD
ESTE REPOSITORIO MUESTRA COMO PROGRAMAR UNA ESP32 CON ULTRASONICO
## INTRODUCCION

### DESCRIPCION

La Esp32 la utilizamos en un entorno de adquision de datos, lo cual en esta practica ocuparemos un ultrasonico para adquirir la distancia; Cabe aclarar que esta practica se usara un simulador llamado WOKWI.
Se agregara asi mismo un LCD I2C para observar dichos datos en cada cierto tiempo

## MATERIAL NECESARIO

Para realizar esta practica necesitas lo siguiente:

-[WOKWI](https://wokwi.com/)

-Tarjeta ESP 32

-HC-SR04 ULTRASONIC Distance sensor

-LCD 16X2 (I2C)

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
const int Trigger = 4;   //Pin digital 2 para el Trigger del sensor
const int Echo = 15;   //Pin digital 3 para el Echo del sensor

LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

void setup() {
  Serial.begin(9600);//iniciailzamos la comunicación
  pinMode(Trigger, OUTPUT); //pin como salida
  pinMode(Echo, INPUT);  //pin como entrada
  digitalWrite(Trigger, LOW);//Inicializamos el pin con 0
  lcd.init();
  lcd.backlight();
}

void loop()
{

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
}
```


2. Instalar la libreria de LiquidCrystal I2C como se muestra en la siguiente imagen



![](https://github.com/jaquelineriverh/PRACTICA-ESP32-CON-ULTRASONICO/blob/main/LIBRERIA%20LIQUID%20EJ3.png)



4.Hacer la conexion de HC-SR04 ULTRASONIC Distance sensor
 con la ESP32 como se muestra en la siguente imagen.

![](https://github.com/jaquelineriverh/PRACTICA-ESP32-CON-ULTRASONICO/blob/main/ULTRASONICO%20CONEXION.png)


5.Hacer la conexion de LCD con la ESP32 como se muestra en la siguente imagen.


![](https://github.com/jaquelineriverh/PRACTICA-ESP32-CON-ULTRASONICO/blob/main/ULTRASONIC%20CON%20LCD.png)


### Instrucciónes de operación
1.Iniciar simulador.

2.Visualizar los datos en el LCD 16x2.

3.Colocar LA DISTANCIA dando doble click al HC-SR04 ULTRASONIC Distance sensor


## Resultados

Cuando haya funcionado, verás los valores dentro del LCD 16x2 como se muestra en la siguente imagen.


![](https://github.com/jaquelineriverh/PRACTICA-ESP32-CON-ULTRASONICO/blob/main/EVIDENCIA%203%20IMAGEN.png)

### EVIDENCIAS


https://github.com/user-attachments/assets/e178b657-6386-4786-8853-6430b924e337


# Créditos

Desarrollado por **JOSE DAVID AYALA VILLALBA**

-[GITHUB](https://github.com/DaybeatAV)
