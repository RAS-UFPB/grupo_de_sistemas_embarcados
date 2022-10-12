<h1>Aula 2 - Estruturas condicionais e utilização dos pinos de entrada e saída digitais do Arduino.</h1>

<a href="https://github.com/RAS-UFPB/Resumo-das-aulas-do-Grupo-de-Robotica/blob/main/Resumo%20aula%202"><b>Resumo da aula</b></a>

<h2>Resolução dos desafios</h2>

<h3>Desafio 1 - Acionamento de alarme com botão</h3>

<div align='center'>
    <h4>Tabela de materiais necessários para esse desafio</h4>
    <table>
        <tr><td>Quantidade</td> <td>Item</td></tr>
        <tr><td>01</td> <td>Arduino Uno</td></tr>
        <tr><td>01</td> <td>Protoboard</td></tr>
        <tr><td>01</td> <td>220Ω Resistor</td></tr>
        <tr><td>01</td> <td>Buzzer</td></tr>
        <tr><td>--</td> <td>Fios</td></tr>
    </table>
</div>

<br>
<div align="center"><img src="./imgs/desafio%203.png" alt="" width="500px">
    <p><b>Esquema de montagem do circuito</b></p>
</div>

<h4>Código</h4>

```c++
#define BOTAO 8
#define BUZZER 9

void setup() {
    pinMode(BOTAO, INPUT);
    pinMode(BUZZER, OUTPUT);
}

void loop() {
    if (digitalRead(BOTAO)){
        tone(BUZZER, 2000);
    } else {
        noTone(BUZZER);
    }
}
```

<hr>

<h3>Desafio 2 - Semáforo que dá a vez para o pedestre ao apertar um botão</h3>

<div align='center'>
    <h4>Tabela de materiais necessários para esse desafio</h4>
    <table>
        <tr><td>Quantidade</td> <td>Item</td></tr>
        <tr><td>01</td> <td>Arduino Uno</td></tr>
        <tr><td>01</td> <td>Protoboard</td></tr>
        <tr><td>04</td> <td>220Ω Resistor</td></tr>
        <tr><td>03</td> <td>Leds</td></tr>
        <tr><td>01</td> <td>Botão</td></tr>
        <tr><td>--</td> <td>Fios</td></tr>
    </table>
</div>

<br>
<div align="center"><img src="./imgs/desafio%204.png" alt="" width="500px">
    <p><b>Esquema de montagem do circuito</b></p>
</div>

<h4>Código</h4>

```c++
#define LED_VERMELHO 4
#define LED_AMARELO 3
#define LED_VERDE 2
#define BOTAO 5

int i;

void setup() {
    pinMode(LED_VERMELHO, OUTPUT);
    pinMode(LED_AMARELO, OUTPUT);
    pinMode(LED_VERDE, OUTPUT);
    pinMode(BOTAO, INPUT);
}

void loop() {
    digitalWrite(LED_VERMELHO, HIGH);
    digitalWrite(LED_AMARELO, LOW);
    digitalWrite(LED_VERDE, LOW);
    delay(2000);
  
    digitalWrite(LED_VERMELHO, LOW);
    digitalWrite(LED_AMARELO, HIGH);
    digitalWrite(LED_VERDE, LOW);
    delay(1000);
    if(digitalRead(BOTAO)) {
        digitalWrite(LED_VERMELHO, HIGH);
        digitalWrite(LED_AMARELO, LOW);
        digitalWrite(LED_VERDE, LOW);
        delay(2000);
    } else {
        delay(1000);
    }
  
    if(digitalRead(BOTAO)){
        digitalWrite(LED_VERMELHO, HIGH);
        digitalWrite(LED_AMARELO, LOW);
        digitalWrite(LED_VERDE, LOW);
        delay(2000);
    } else {
        digitalWrite(LED_VERMELHO, LOW);
        digitalWrite(LED_AMARELO, LOW);
        digitalWrite(LED_VERDE, HIGH);
        delay(1000);
    
        if(digitalRead(BOTAO)) {
            digitalWrite(LED_VERMELHO, HIGH);
            digitalWrite(LED_AMARELO, LOW);
            digitalWrite(LED_VERDE, LOW);
            delay(2000);
        } else {
            delay(1000);
        }
    }
}
```
<hr>

<h3>Desafio 3 - Leds piscando alternadamente, aumentando a velocidade de piscada ou diminuindo para cada click no botão</h3>

<div align='center'>
    <h4>Tabela de materiais necessários para esse desafio</h4>
    <table>
        <tr><td>Quantidade</td> <td>Item</td></tr>
        <tr><td>01</td> <td>Arduino Uno</td></tr>
        <tr><td>01</td> <td>Protoboard</td></tr>
        <tr><td>04</td> <td>220Ω Resistor</td></tr>
        <tr><td>02</td> <td>Leds</td></tr>
        <tr><td>02</td> <td>Botão</td></tr>
        <tr><td>--</td> <td>Fios</td></tr>
    </table>
</div>

<br>
<div align="center"><img src="./imgs/desafio%205.png" alt="" width="500px">
    <p><b>Esquema de montagem do circuito</b></p>
</div>

<h4>Código</h4>

```c++
#define LED_VERMELHO 2
#define LED_AZUL 3
#define AUMENTA 5
#define DIMINUI 6

int tempo = 3000;

void setup() {
    pinMode(LED_AZUL, OUTPUT);
    pinMode(LED_VERMELHO, OUTPUT);
    pinMode(AUMENTA, INPUT);
    pinMode(DIMINUI, INPUT);
}

void loop() {
    digitalWrite(LED_AZUL, HIGH);
    digitalWrite(LED_VERMELHO, LOW);
    if(digitalRead(AUMENTA)) {
        tempo += 1000;
        delay(tempo);
    } else if(digitalRead(DIMINUI) && (tempo > 1000)) {
        tempo -= 1000;
        delay(tempo);
    } else {
        delay(tempo);
    }
  
    digitalWrite(LED_AZUL, LOW);
    digitalWrite(LED_VERMELHO, HIGH);
    if(digitalRead(AUMENTA)) {
        tempo += 1000;
        delay(tempo);
    } else if(digitalRead(DIMINUI) && (tempo > 1000)) {
        tempo -= 1000;
        delay(tempo);
    } else {
        delay(tempo);
    }
}
```
