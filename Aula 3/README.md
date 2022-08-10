<h1>Aula 3 - Comunicação serial e a função millis.</h1>

<a href="https://github.com/RAS-UFPB/Resumo-das-aulas-do-Grupo-de-Robotica/blob/main/Resumo%20aula%203"><h2>Resumo da aula</h2></a>

<h2>Resolução dos desafios</h2>

<h3>Desafio 1 - Buzzer e leds funcionando alternadamente usando a função millis</h3>

<div align='center'>
    <h4>Tabela de materiais necessários para esse desafio</h4>
    <table>
        <tr><td>Quantidade</td> <td>Item</td></tr>
        <tr><td>01</td> <td>Arduino Uno</td></tr>
        <tr><td>01</td> <td>Protoboard</td></tr>
        <tr><td>02</td> <td>220Ω Resistor</td></tr>
        <tr><td>02</td> <td>Leds</td></tr>
        <tr><td>01</td> <td>Buzzer</td></tr>
        <tr><td>--</td> <td>Fios</td></tr>
    </table>
</div>

<br>
<div align="center"><img src="./imgs/desafio%206.png" alt="" width="500px">
    <p><b>Esquema de montagem do circuito</b></p>
</div>

<h4>Código</h4>

```c++
#define LED_VERMELHO 4
#define LED_AZUL 3
#define BUZZER 2

unsigned long millisLed1 = millis();
unsigned long millisLed2 = millis();
unsigned long millisBuzzer = millis();

void setup() {
    pinMode(LED_VERMELHO, OUTPUT);
    pinMode(LED_AZUL, OUTPUT);
    pinMode(BUZZER, OUTPUT);
}

void loop() {
    if ((millis() - millisLed1) < 500) {
        digitalWrite(LED_VERMELHO, HIGH);
    } else {
        digitalWrite(LED_VERMELHO, LOW);
    }
  
    if ((millis() - millisLed1) > 1500) {
        millisLed1 = millis();
    }
  
    if ((millis() - millisLed2) < 1500) {
        digitalWrite(LED_AZUL, HIGH);
    } else {
        digitalWrite(LED_AZUL, LOW);
    }
  
    if ((millis() - millisLed2) > 2500) {
        millisLed2 = millis();
    }

  
    if ((millis() - millisBuzzer) < 2500) {
        tone(BUZZER, 2000);
    } else {
        noTone(BUZZER);
    }
  
    if ((millis() - millisBuzzer) > 3500) {
        millisBuzzer = millis();
    }
}

```

<hr>

<h3>Desafio 2 - Leds acendendo através do monitor serial</h3>

<div align='center'>
    <h4>Tabela de materiais necessários para esse desafio</h4>
    <table>
        <tr><td>Quantidade</td> <td>Item</td></tr>
        <tr><td>01</td> <td>Arduino Uno</td></tr>
        <tr><td>01</td> <td>Protoboard</td></tr>
        <tr><td>03</td> <td>220Ω Resistor</td></tr>
        <tr><td>03</td> <td>Leds</td></tr>
        <tr><td>--</td> <td>Fios</td></tr>
    </table>
</div>

<br>
<div align="center"><img src="./imgs/desafio%207.png" alt="" width="500px">
    <p><b>Esquema de montagem do circuito</b></p>
</div>

<h4>Código</h4>

```c++
#define LED_VERDE 4
#define LED_AMARELO 3
#define LED_AZUL 2

String valorLido; 

void setup() {
    Serial.begin(9600);
  
    pinMode(LED_AZUL, OUTPUT);
    pinMode(LED_AMARELO, OUTPUT);
    pinMode(LED_VERDE, OUTPUT);
}

void loop() {
    valorLido = Serial.readString();
  
    if(valorLido == "VERDE") {
        digitalWrite(LED_VERDE, HIGH);
        digitalWrite(LED_AMARELO, LOW);
        digitalWrite(LED_AZUL, LOW);
    } else if (valorLido == "AMARELO") {
        digitalWrite(LED_VERDE, LOW);
        digitalWrite(LED_AMARELO, HIGH);
        digitalWrite(LED_AZUL, LOW);
    } else if (valorLido == "AZUL") {
        digitalWrite(LED_VERDE, LOW);
        digitalWrite(LED_AMARELO, LOW);
        digitalWrite(LED_AZUL, HIGH);
    } else {
  	    digitalWrite(LED_VERDE, LOW);
        digitalWrite(LED_AMARELO, LOW);
        digitalWrite(LED_AZUL, LOW);
    }
}
```
