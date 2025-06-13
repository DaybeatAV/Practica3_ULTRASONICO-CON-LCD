# Práctica 3 "ULTRASÓNICO CON LCD"
En este repositorio se mostrará como programar una Tarjeta ```ESP32``` con un ```Ultrasónico``` mostrando datos en una pantalla ```LCD (I2C)```.
## INTRODUCCIÓN

### DESCRIPCIÓN

Vamos a utilizar una tarjeta ```ESP32``` en un entorno de adquision de datos, por lo que en esta práctica utilizaremos un componente llamado ```Ultrasonico``` para obtener la distancia; Se debe anticipar que para esta practica haremos uso del simulador llamado [WOKWI](https://wokwi.com/), mismo que hemos utilizado para las prácticas anteriores.
Además insertaremos una pantalla ```LCD (I2C)``` para monitorear los valores arrojados por el Ultrasónico cada cierto intervalo de tiempo.

## MATERIAL NECESARIO

La siguiente es una lista de los componentes que se necesitarán para llevar a cabo la práctica:

-[WOKWI](https://wokwi.com/)

- ```Tarjeta ESP32```

- ```HC-SR04 ULTRASONIC Distance sensor```

- ```LCD 16X2 (I2C)```

## INSTRUCCIONES

### Requisitos previos

Es necesario iniciar el software [WOKWI](https://wokwi.com/) para poder llevar a cabo esta práctica

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

  lcd.setCursor(4, 0);
  lcd.print("DIPLOMADO");
  lcd.setCursor(2, 1); 
  lcd.print("AUTOMATIZACION");
  delay(2000);
  lcd.clear();

  lcd.setCursor(1, 0);
  lcd.print("JOSE DAVID A.V");
  lcd.setCursor(4, 1); 
  lcd.print("MECANICO");
  delay(2000);
  lcd.clear();
  lcd.setCursor(3, 0);
  lcd.print("07-06-2025");
  delay(2000);
  lcd.clear();

  lcd.setCursor(2, 0);
  lcd.print("Distancia: " + String(d) + "cm");
  
  delay(2000);
   lcd.clear();
}
```

2. El primer paso será instalar la libreria de LiquidCrystal I2C como se muestra en la siguiente imagen:

![](https://github.com/DaybeatAV/Practica3_ULTRASONICO-CON-LCD/blob/main/Pr%C3%A1ctica%203%20Librer%C3%ADa%20LyquidCrystal%20I2C.png)

3. El siguiente paso será insertar el componente ```HC-SR04 ULTRASONIC Distance sensor``` junto a la tarjeta ```ESP32```:

![](https://github.com/DaybeatAV/Practica3_ULTRASONICO-CON-LCD/blob/main/Pr%C3%A1ctica%203%20Inserto%20de%20Ultras%C3%B3nico.png)

4. Después haremos la conexion del componente ```HC-SR04 ULTRASONIC Distance sensor``` con la tarjeta ```ESP32``` tal como se ve a continuación:

![](https://github.com/DaybeatAV/Practica3_ULTRASONICO-CON-LCD/blob/main/Pr%C3%A1ctica%203%20Conexiones%20de%20Ultras%C3%B3nico.png)

5. Por último procederemos a realizar la conexion de la pantalla ```LCD I2C``` con la tarjeta ```ESP32``` para obtener el resultado final:

![](https://github.com/DaybeatAV/Practica3_ULTRASONICO-CON-LCD/blob/main/Pr%C3%A1ctica%203%20Conexiones%20de%20Ultras%C3%B3nico%20y%20Pantalla%20LCD.png)

### Instrucciónes de operación
1. El primer paso será inicializar el simulador.

2. Después se visualizarán los datos en la pantalla ```LCD 16x2 (I2C)``` cada cierto invervalo de tiempo.

3. Variar la distancia dando doble click al ```HC-SR04 ULTRASONIC Distance sensor``` para observar la distancia final en pantalla.

## Resultados

Si la simulación opera de manera correcta se verán los valores dentro de la pantalla ```LCD 16x2 (I2C)``` como se ve en la siguiente imagen:

![](https://github.com/DaybeatAV/Practica3_ULTRASONICO-CON-LCD/blob/main/Pr%C3%A1ctica%203%20Resultado%20Final.png)

### EVIDENCIAS

https://github.com/user-attachments/assets/127a41fe-b55d-41a7-a087-176baa5df09d

# Créditos

Desarrollado por **JOSE DAVID AYALA VILLALBA**

-[GITHUB](https://github.com/DaybeatAV)
