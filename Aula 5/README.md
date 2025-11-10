# Aula 5

[**Resumo da aula**](https://github.com/RAS-UFPB/resumo_das_aulas_do_grupo_de_sistemas_embarcados/tree/main/Resumo%20aula%205)

## Resolução do desafio
```C++
#include <Servo.h>
#include <LiquidCrystal.h>
#include <SoftwareSerial.h>
#define rxPin 1
#define txPin 0
LiquidCrystal lcd (12, 11, 5,4 ,3 ,2);
SoftwareSerial serialdobluetooth(rxPin, txPin);
Servo myServo;
char valordobluetooth = '0';
int servo = 8;
void setup() {
  lcd.begin(16,2);
  myServo.attach(servo);
  pinMode(rxPin, INPUT);
  pinMode(txPin, OUTPUT);
  serialdobluetooth.begin(9600);
  serialdobluetooth.print("$");
  serialdobluetooth.print("$");
  serialdobluetooth.print("$");
}
void loop() {
  lcd.setCursor(0,0);
  lcd.print("Ligado");
  if(serialdobluetooth.available()){
    valordobluetooth = serialdobluetooth.read();
    serialdobluetooth.print(valordobluetooth);
  }
 
  myServo.write(0);
  if(valordobluetooth == 'A'){
    lcd.setCursor(0,0);
    lcd.print("Cuidado !!");
    lcd.setCursor(0,1);
    lcd.print("Saida de Veiculo");
   
    myServo.write(90);
    delay(1000);
    myServo.write(0);
  }
 
  if(valordobluetooth == 'B'){
    lcd.setCursor(0,0);
    lcd.print("Fechando portao");
    lcd.setCursor(0,1);
    lcd.print(" ");
    myServo.write(0);
    delay(1000);
  }
}
```
