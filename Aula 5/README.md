<h1>Aula 5 - Sinais de saída analógicos com PWM.</h1>

<a href="https://github.com/RAS-UFPB/Resumo-das-aulas-do-Grupo-de-Robotica/blob/main/Resumo%20aula%205"><h2>Resumo da aula</h2></a>

<h2>Resolução dos desafios</h2>

<h3>Desafio 1 - Controle um Servo Motor usando um potenciômetro</h3>

<div align='center'>
    <h4>Tabela de materiais necessários para esse desafio</h4>
    <table>
        <tr><td>Quantidade</td> <td>Item</td></tr>
        <tr><td>01</td> <td>Arduino Uno</td></tr>
        <tr><td>01</td> <td>Protoboard</td></tr>
        <tr><td>01</td> <td>Potenciômetro</td></tr>
        <tr><td>01</td> <td>Servo Motor</td></tr>
        <tr><td>--</td> <td>Fios</td></tr>
    </table>
</div>

<br>
<div align="center"><img src="./images/A06D01.png" alt="" width="500px">
    <p><b>Esquema de montagem do circuito</b></p>
</div>

<h4>Código</h4>

```c++
#include <Servo.h>

#define SERVO_PIN 3

int potValue = 0;
int servoValue = 0;

Servo servo;

void setup() {
    servo.attach(SERVO_PIN);
    servo.write(servoValue);
}

void loop() {
    potValue = analogRead(A0);
  
    servoValue = map(potValue, 0, 1023, 0, 180);
    servo.write(servoValue);
}
```

<hr>

<h3>Desafio 2 - Dimmer utilizando a comunicação serial e o PWM</h3>

<div align='center'>
    <h4>Tabela de materiais necessários para esse desafio</h4>
    <table>
        <tr><td>Quantidade</td> <td>Item</td></tr>
        <tr><td>01</td> <td>Arduino Uno</td></tr>
        <tr><td>01</td> <td>Protoboard</td></tr>
        <tr><td>01</td> <td>220Ω Resistor</td></tr>
        <tr><td>01</td> <td>Leds</td></tr>
        <tr><td>--</td> <td>Fios</td></tr>
    </table>
</div>

<br>
<div align="center"><img src="./images/A06D02.png" alt="" width="500px">
    <p><b>Esquema de montagem do circuito</b></p>
</div>

<h4>Código</h4>

```c++
#define LED_PIN 5

void setup() {
    pinMode(LED_PIN, OUTPUT);
    Serial.begin(9600);
}

void loop() {
    if(Serial.available() > 0){
  	    int value = Serial.parseInt();
    	analogWrite(LED_PIN, value);
    }
}
```
