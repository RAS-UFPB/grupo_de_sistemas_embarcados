<h1>Aula 3</h1>

<a href="https://github.com/RAS-UFPB/Resumo-das-aulas-do-Grupo-de-Robotica/blob/main/Resumo%20aula%203"><b>Resumo da aula</b></a>

<h2>Resolução dos desafios</h2>

<h3>Desafio 1</h3>

<div align='center'>
    <h4>Tabela de materiais necessários para esse desafio</h4>
    <table>
        <tr><td>Quantidade</td><td>Item</td></tr>
        <tr><td>01</td> <td>Arduino Uno</td></tr>
        <tr><td>01</td> <td>LED</td></tr>
        <tr><td>01</td> <td>Resistor 220 ohm</td></tr>
        <tr><td>--</td> <td>Fios</td></tr>
    </table>
</div>

<br>
<div align="center"><img src="./imgs/desafio1.png" alt="" width="500px">
    <p><b>Esquema de montagem do circuito</b></p>
</div>

<h4>Código</h4>

```c++
#define LED_PIN = 9;
int dimmerValue = 0;

void setup() {
    Serial.begin(9600);
    pinMode(LED_PIN, OUTPUT);
}

void loop() {
    if (Serial.available()) {
        dimmerValue = Serial.read();
        dimmerValue = map(dimmerValue, 0, 255, 0, 255);
        analogWrite(LED_PIN, dimmerValue);
        Serial.println(dimmerValue);
    }
}
```



<h3>Desafio 2</h3>

<div align='center'>
    <h4>Tabela de materiais necessários para esse desafio</h4>
    <table>
        <tr><td>Quantidade</td><td>Item</td></tr>
        <tr><td>01</td> <td>Arduino Uno</td></tr>
        <tr><td>01</td> <td>Protoboard</td></tr>
        <tr><td>01</td> <td>Potenciômetro</td></tr>
        <tr><td>01</td> <td>Servo Motor</td></tr>
        <tr><td>--</td> <td>Fios</td></tr>
    </table>
</div>

<br>
<div align="center"><img src="./imgs/desafio2.png" alt="" width="500px">
    <p><b>Esquema de montagem do circuito</b></p>
</div>

<h4>Código</h4>

```c++
#include <Servo.h>

#define PIN_POTENCIOMETRO A5
#define PIN_SERVO 9

int valorDoPotenciometro = 0;
Servo servo;

void setup(){
  servo.attach(PIN_SERVO);
  pinMode(PIN_POTENCIOMETRO, INPUT);
}
void loop(){
  valorDoPotenciometro = analogRead(PIN_POTENCIOMETRO);
  servo.write(map(valorDoPotenciometro, 0, 1023, 0, 180));
}
```


<h3>Desafio 3</h3>

<div align='center'>
    <h4>Tabela de materiais necessários para esse desafio</h4>
    <table>
        <tr><td>Quantidade</td> <td>Item</td></tr>
        <tr><td>01</td> <td>Arduino Uno</td></tr>
        <tr><td>01</td> <td>Protoboard</td></tr>
        <tr><td>01</td> <td>Potenciômetro</td></tr>
        <tr><td>02</td> <td>Motores DC</td></tr>
        <tr><td>01</td> <td>L293D</td></tr>
        <tr><td>--</td> <td>Fios</td></tr>
    </table>
</div>

<br>
<div align="center"><img src="./imgs/desafio3.png" alt="" width="500px">
    <p><b>Esquema de montagem do circuito</b></p>
</div>

<h4>Código</h4>

```c++
#define POTENCIOMETRO A0
#define ENTRADA1 5
#define ENTRADA2 6
#define ENTRADA3 9
#define ENTRADA4 10
#define ENABLE1 2
#define ENABLE3 3

int valorPotenc;
int estadoMovimento;

void setup() {
    Serial.begin(9600);
  
    pinMode(POTENCIOMETRO, INPUT);
    pinMode(ENTRADA1, OUTPUT);
    pinMode(ENTRADA2, OUTPUT);
    pinMode(ENTRADA3, OUTPUT);
    pinMode(ENTRADA4, OUTPUT);
    pinMode(ENABLE1, OUTPUT);
    pinMode(ENABLE3, OUTPUT);
}

void loop() {
    valorPotenc = analogRead(POTENCIOMETRO);
    estadoMovimento = map(valorPotenc, 0, 1023, 1, 3);
  
    if(estadoMovimento == 1) {
        digitalWrite(ENABLE1, HIGH);
        digitalWrite(ENABLE3, HIGH);

        analogWrite(ENTRADA1, HIGH);
        digitalWrite(ENTRADA2, LOW);
        digitalWrite(ENTRADA3, LOW);
        digitalWrite(ENTRADA4, HIGH);
    } else if(estadoMovimento == 2) {
        digitalWrite(ENABLE1, HIGH);
        digitalWrite(ENABLE3, HIGH);
    
        digitalWrite(ENTRADA1, LOW);
        digitalWrite(ENTRADA2, HIGH);
        digitalWrite(ENTRADA3, HIGH);
        digitalWrite(ENTRADA4, LOW);
    } else if(estadoMovimento == 3) {
        digitalWrite(ENABLE1, LOW);
        digitalWrite(ENABLE3, LOW);

        digitalWrite(ENTRADA1, LOW);
        digitalWrite(ENTRADA2, LOW);
        digitalWrite(ENTRADA3, LOW);
        digitalWrite(ENTRADA4, LOW);
    }
  
    Serial.println(estadoMovimento);
}
```
