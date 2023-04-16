<h1>Aula 2.</h1>

<a href="https://github.com/RAS-UFPB/resumo_das_aulas_do_grupo_de_sistemas_embarcados/tree/main/Resumo%20aula%202"><b>Resumo da aula</b></a>

<h2>Resolução dos desafios</h2>

<h3>Desafio 1</h3>

<div align='center'>
    <h4>Tabela de materiais necessários para esse desafio</h4>
    <table>
        <tr><td>Quantidade</td> <td>Item</td></tr>
        <tr><td>01</td> <td>Protoboard</td></tr>
        <tr><td>04</td> <td>220Ω Resistor</td></tr>
        <tr><td>03</td> <td>Leds</td></tr>
        <tr><td>01</td> <td>Botão</td></tr>
        <tr><td>--</td> <td>Fios</td></tr>
    </table>
</div>

<br>

<div align="center"><img src="./imgs/circuito desafio 1.png" alt="" width="800px">
    <p><b>Esquema de montagem do circuito</b></p>
</div>
<hr>

<h4>Código</h4>

```c++
int ledPinVerde = 2;//Define ledPinVerde no pino digital 2
int ledPinAmarelo = 3;//Define ledPinAmarelo no pino digital 3
int ledPinVermelho = 4;//Define ledPinVermelho no pino digital 4
int pushbutton = 5;
int estadoButton = 0;//Variável responsável por armazenar o estado do botão (ligado/desligado)

void setup(){
  pinMode(ledPinVerde , OUTPUT);//Define ledPinVerde (pino 2) como saída
  pinMode(ledPinAmarelo , OUTPUT);//Define ledPinAmarelo (pino 3) como saída
  pinMode(ledPinVermelho , OUTPUT);//Define ledPinVermelho (pino 4) como saída
  pinMode(pushbutton , INPUT);//Define pushbutton (pino 5) como entrada
}

void loop(){
  
  estadoButton = digitalRead(pushbutton);
  
  if(estadoButton == HIGH){
    
    // Ativamos o pino referente ao led vermelho  
  	digitalWrite(ledPinVermelho, HIGH);
  	digitalWrite(ledPinAmarelo, LOW);
  	digitalWrite(ledPinVerde, LOW);
  }else{
  
    // Ativamos o pino referente ao led vermelho  
  	digitalWrite(ledPinVermelho, HIGH);
  	digitalWrite(ledPinAmarelo, LOW);
  	digitalWrite(ledPinVerde, LOW);

  	// Aguardamos 2 segundos
  	delay(2000);

  	// Ligamos o pino referente ao led amarelo
  	digitalWrite(ledPinVermelho, LOW);
  	digitalWrite(ledPinAmarelo, HIGH);
  	digitalWrite(ledPinVerde, LOW);

  	// Aguardamos mais um segundo
  	delay(1000);
  	
  	// Ativamos o pino referente ao led verde  
  	digitalWrite(ledPinVermelho, LOW);
  	digitalWrite(ledPinAmarelo, LOW);
  	digitalWrite(ledPinVerde, HIGH);
  	

  	// Aguardamos 3 segundos
  	delay(3000);
  }

}
```

<h3>Desafio 2</h3>

<div align='center'>
    <h4>Tabela de materiais necessários para esse desafio</h4>
    <table>
        <tr><td>Quantidade</td> <td>Item</td></tr>
        <tr><td>01</td> <td>Protoboard</td></tr>
        <tr><td>02</td> <td>220Ω Resistor</td></tr>
        <tr><td>02</td> <td>Leds</td></tr>
        <tr><td>--</td> <td>Fios</td></tr>
    </table>
</div>

<br>

<div align="center"><img src="./imgs/circuito desafio 2.png" alt="" width="800px">
    <p><b>Esquema de montagem do circuito</b></p>
</div>
<hr>

<h4>Código:</h4>

```c++
int pinoLedVermelho = 4;
int pinoLedVerde = 6;

//Armazena o estado dos leds
int estadoLedVermelho = LOW;
int estadoLedVerde = LOW;

//Armazena o valor (tempo) da ultima vez que o led foi aceso
int previousMillisLedVermelho = 0;
int previousMillisLedVerde = 0;
//Intervalo de tempo entre acionamentos do led (em milisegundos)
const int intervaloLedVermelho = 2000;
const int intervaloLedVerde = 1000;
void setup()
{
  //Define o pino do led como saida
  pinMode(pinoLedVermelho, OUTPUT);
  pinMode(pinoLedVerde, OUTPUT);
}
void loop()
{
  int currentMillis = millis();
  //Verifica se o intervalo do Led Vermelho já foi atingido
  if (currentMillis - previousMillisLedVermelho >= intervaloLedVermelho)
  {
    //Armazena o valor da ultima vez que o led foi aceso
    previousMillisLedVermelho = currentMillis;
    //Inverte o estado do led
    if (estadoLedVermelho == LOW)
    {
      estadoLedVermelho = HIGH;
    } else {
      estadoLedVermelho = LOW;
    }
    //Acende ou apaga o led
    digitalWrite(pinoLedVermelho, estadoLedVermelho);
  }
  
  //Verifica se o intervalo do Led Verde já foi atingido
  if (currentMillis - previousMillisLedVerde >= intervaloLedVerde)
  {
    //Armazena o valor da ultima vez que o led foi aceso
    previousMillisLedVerde = currentMillis;
    //Inverte o estado do led
    if (estadoLedVerde == LOW)
    {
      estadoLedVerde = HIGH;
    } else {
      estadoLedVerde = LOW;
    }
    //Acende ou apaga o led
    digitalWrite(pinoLedVerde, estadoLedVerde);
  }
}
```

