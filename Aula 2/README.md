<h1>Aula 2 - Introdução ao Arduino: Teoria e prática de construção circuitos básicos com Arduino.</h1>

<a href="https://github.com/RAS-UFPB/Resumo-das-aulas-do-Grupo-de-Robotica/blob/main/Resumo%20aula%202"><h2>Resumo da aula</h2></a>

<h2>Resolução dos desafios</h2>

<h3>Desafio 1 - Leds piscando alternadamente</h3>

<div align='center'>
    <h4>Tabela de materiais necessários para esse desafio</h4>
    <table>
        <tr><td>Quantidade</td> <td>Item</td></tr>
        <tr><td>01</td> <td>Arduino Uno</td></tr>
        <tr><td>01</td> <td>Protoboard</td></tr>
        <tr><td>02</td> <td>220Ω Resistor</td></tr>
        <tr><td>02</td> <td>Leds</td></tr>
        <tr><td>--</td> <td>Fios</td></tr>
    </table>
</div>

<br>
<div align="center"><img src="https://github.com/RAS-UFPB/Grupo-de-Robotica/blob/main/Aula%202/imgs/desafio%201.png" alt="" width="500px">
    <p><b>Esquema de montagem do circuito</b></p>
</div>

<h4>Código</h4>

```c++
#define LED_VERMELHO 2
#define LED_AZUL 3

void setup() {
  pinMode(LED_VERMELHO, OUTPUT);
  pinMode(LED_AZUL, OUTPUT);
}

void loop() {
  int tempo = 1000;
  
  digitalWrite(LED_VERMELHO, HIGH);
  digitalWrite(LED_AZUL, LOW);
  delay(tempo);
  tempo += 2000;
  digitalWrite(LED_VERMELHO, LOW);
  digitalWrite(LED_AZUL, HIGH);
  delay(tempo);
  tempo -= 1000;
}
```

<hr>

<h3>Desafio 2 - Semáforo</h3>

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
<div align="center"><img src="https://github.com/RAS-UFPB/Grupo-de-Robotica/blob/main/Aula%202/imgs/desafio%202.png" alt="" width="500px">
    <p><b>Esquema de montagem do circuito</b></p>
</div>

<h4>Código</h4>

```c++
#define LED_VERMELHO 2
#define LED_AMARELO 3
#define LED_VERDE 4

void setup()
{
  pinMode(LED_VERMELHO, OUTPUT);
  pinMode(LED_AMARELO, OUTPUT);
  pinMode(LED_VERDE, OUTPUT);
}

void loop()
{
  digitalWrite(LED_VERMELHO, HIGH);
  digitalWrite(LED_AMARELO, LOW);
  digitalWrite(LED_VERDE, LOW);
  delay(2000);
  digitalWrite(LED_VERMELHO, LOW);
  digitalWrite(LED_AMARELO, HIGH);
  digitalWrite(LED_VERDE, LOW);
  delay(2000);
  digitalWrite(LED_VERMELHO, LOW);
  digitalWrite(LED_AMARELO, LOW);
  digitalWrite(LED_VERDE, HIGH);
  delay(2000);
}
```
