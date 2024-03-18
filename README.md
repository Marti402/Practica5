# Practica5
BUS I2C
# **1.1 Descibir la salida por el puerto serie**
A partir del código siguiente, se realiza un bucle que escanea todo el circuito en busca de "esclavos", que son buses de comunicación, los cuales esten disponibles o que puedan leer el lenguaje del host (ESP32), en nuestro caso es el 0x27.

``` c++
#include <Arduino.h>
#include <Wire.h>

void setup()
  {
  Wire.begin();
  Serial.begin(115200);
  while (!Serial);
  // Leonardo: wait for serial monitor
  Serial.println("\nI2C Scanner");
  }
void loop()
  {
  byte error, address;

  int nDevices;
  Serial.println("Scanning...");
  nDevices = 0;
  for(address = 1; address < 127; address++ )
  {
  // The i2c_scanner uses the return value of
  // the Write.endTransmisstion to see if
  // a device did acknowledge to the address.
  Wire.beginTransmission(address);
  error = Wire.endTransmission();
  if (error == 0)
  {
  Serial.print("I2C device found at address 0x");
  if (address<16)
  Serial.print("0");
  Serial.print(address,HEX);
  Serial.println(" !");
  nDevices++;
  }
  else if (error==4)
  {
  Serial.print("Unknown error at address 0x");
  if (address<16)
  Serial.print("0");
  Serial.println(address,HEX);
  }
  }
  if (nDevices == 0)
  Serial.println("No I2C devices found\n");
  else
  Serial.println("done\n");
  delay(5000);
  // wait 5 seconds for next scan
  }
```
**Hello World!**
Para hacer un Hello World hemos descargado la libreria LiquidCrystal_I2C by Frank de Brabander y con un ejemplo hemos logrado imprimir este texto:
"
Hello, world!
Ywrobot Arduino!
Arduino LCM IIC 2004
Power By Ec-yuan!
"
```c++
#include <Arduino.h>
//Compatible with the Arduino IDE 1.0
//Library version:1.1
#include <LiquidCrystal_I2C.h>

LiquidCrystal_I2C lcd(0x27,20,4);  // set the LCD address to 0x27 for a 16 chars and 2 line display

void setup()
{
  lcd.init();                      // initialize the lcd 
  // Print a message to the LCD.
  lcd.backlight();
  lcd.setCursor(3,0);
  lcd.print("Hello, world!");
  lcd.setCursor(2,1);
  lcd.print("Ywrobot Arduino!");
   lcd.setCursor(0,2);
  lcd.print("Arduino LCM IIC 2004");
   lcd.setCursor(2,3);
  lcd.print("Power By Ec-yuan!");
}


void loop()
{
}
```



