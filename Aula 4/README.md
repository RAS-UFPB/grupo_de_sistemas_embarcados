<h1>Aula 4 - Sinais de entrada analógicos e digitais: utilizando sensores.</h1>

<a href="https://github.com/RAS-UFPB/Resumo-das-aulas-do-Grupo-de-Robotica/blob/main/Resumo%20aula%204"><h2>Resumo da aula</h2></a>

<h2>Resolução dos desafios</h2>

<h3>Desafio 1 - Sensor de ré utilizando o sensor ultrassônico e buzzer</h3>

<div align='center'>
    <h4>Tabela de materiais necessários para esse desafio</h4>
    <table>
        <tr><td>Quantidade</td> <td>Item</td></tr>
        <tr><td>01</td> <td>Arduino Uno</td></tr>
        <tr><td>01</td> <td>Protoboard</td></tr>
        <tr><td>01</td> <td>100Ω Resistor</td></tr>
        <tr><td>01</td> <td>Buzzer</td></tr>
        <tr><td>--</td> <td>Fios</td></tr>
    </table>
</div>

<br>
<div align="center"><img src="./images/A05D01.png" alt="" width="500px">
    <p><b>Esquema de montagem do circuito</b></p>
</div>

<h4>Código</h4>

```c++
#define ECHO_PIN 4 
#define TRIGGER_PIN 5 

#define BUZZER_PIN 6

#define MIN_DISTANCE_TO_ALARM 100 /*Distância em cm, escolhida arbitrariamente*/

long duration;
int distance; 



void setup() {
  pinMode(TRIGGER_PIN, OUTPUT); 
  pinMode(ECHO_PIN, INPUT); 
  pinMode(BUZZER_PIN, OUTPUT);
}
void loop() {
  /*Efetuando a leitura da distância*/
  digitalWrite(TRIGGER_PIN, LOW);
  delayMicroseconds(2);
  digitalWrite(TRIGGER_PIN, HIGH);
  delayMicroseconds(10);
  digitalWrite(TRIGGER_PIN, LOW);
 
  duration = pulseIn(ECHO_PIN, HIGH);

  distance = duration * 0.034 / 2; 
  
  /*Avaliando acionamento do alarme (Buzzer)*/
  if(distance <= MIN_DISTANCE_TO_ALARM){
  	tone(BUZZER_PIN, 1000);
  }else{
    noTone(BUZZER_PIN);
  }
}

```

<hr>

<h3>Desafio 2 - Ligar/Desligar o LED de acordo com a luminosidade utilizando o LDR</h3>

<div align='center'>
    <h4>Tabela de materiais necessários para esse desafio</h4>
    <table>
        <tr><td>Quantidade</td> <td>Item</td></tr>
        <tr><td>01</td> <td>Arduino Uno</td></tr>
        <tr><td>01</td> <td>Protoboard</td></tr>
        <tr><td>02</td> <td>220Ω Resistor</td></tr>
        <tr><td>01</td> <td>Leds</td></tr>
        <tr><td>--</td> <td>Fios</td></tr>
    </table>
</div>

<br>
<div align="center"><img src="./images/A05D02.png" alt="" width="500px">
    <p><b>Esquema de montagem do circuito</b></p>
</div>

<h4>Código</h4>

```c++
#define LED_PIN 7
#define MIN_LUMINOSITY 800

int ldrValue = 0;


void setup()
{
  pinMode(LED_PIN, OUTPUT);
}

void loop()
{
  ldrValue = analogRead(A0);
  
  if(ldrValue >= MIN_LUMINOSITY){
  	digitalWrite(LED_PIN, HIGH);
  }else{
    digitalWrite(LED_PIN, LOW);
  } 
}
```
