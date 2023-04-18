<h1>Aula 3</h1>

<a href="https://github.com/RAS-UFPB/resumo_das_aulas_do_grupo_de_sistemas_embarcados/tree/main/Resumo%20aula%204"><b>Resumo da aula</b></a>

<h2>Resolução dos desafios</h2>

<h3>Desafio 1</h3>

<div align='center'>
    <h4>Tabela de materiais necessários para esse desafio</h4>
    <table>
        <tr><td>Quantidade</td><td>Item</td></tr>
        <tr><td>01</td> <td>Arduino Uno</td></tr>
        <tr><td>03</td> <td>LED</td></tr>
        <tr><td>03</td> <td>Resistor 220 ohm</td></tr>
        <tr><td>01</td> <td>Sensor HC-SR04</td></tr>
        <tr><td>--</td> <td>Fios</td></tr>
    </table>
</div>

<br>
<div align="center"><img src="Aula 4/imgs/sensor_de_re.png" alt="" width="500px">
    <p><b>Esquema de montagem do circuito</b></p>
</div>

<h4>Código</h4>

```c++
#define TRIGGER 6
#define ECHO 5
#define LED_VD 4
#define LED_AM 3
#define LED_VM 2

int tempo, distancia;

void setup()
{
  Serial.begin(9600);
  pinMode(LED_VM, OUTPUT);
  pinMode(LED_AM, OUTPUT);
  pinMode(LED_VD, OUTPUT);
  pinMode(ECHO, INPUT);
  pinMode(TRIGGER, OUTPUT);
}

void loop()
{
  digitalWrite(TRIGGER, HIGH);
  delayMicroseconds(10);
  digitalWrite(TRIGGER, LOW);
  
  tempo = pulseIn(ECHO, HIGH);
  
  distancia = tempo*0.01715;
  
  Serial.print("distancia: ");
  Serial.print(distancia);
  Serial.println("cm");
 
  if(distancia >= 250){
    digitalWrite(LED_VD, HIGH);
  	digitalWrite(LED_AM, HIGH);
    digitalWrite(LED_VM, HIGH);
    
  }else if(distancia >= 150){
  	digitalWrite(LED_VD, HIGH);
    digitalWrite(LED_AM, HIGH);
    digitalWrite(LED_VM, LOW);
    
  }else{
    digitalWrite(LED_VD, HIGH);
    digitalWrite(LED_AM, LOW);
    digitalWrite(LED_VM, LOW);
  }
```



<h3>Desafio 2</h3>

<div align='center'>
    <h4>Tabela de materiais necessários para esse desafio</h4>
    <table>
        <tr><td>Quantidade</td><td>Item</td></tr>
        <tr><td>01</td> <td>Arduino Uno</td></tr>
        <tr><td>01</td> <td>Protoboard</td></tr>
        <tr><td>02</td> <td>LED</td></tr>
        <tr><td>04</td> <td>Resistor de 1 kOhm</td></tr>
        <tr><td>01</td> <td>Buzzer</td></tr>
        <tr><td>01</td> <td>Sensor LDR</td></tr>
        <tr><td>01</td> <td>Sensor TMP36</td></tr>
        <tr><td>--</td> <td>Fios</td></tr>
    </table>
</div>

<br>
<div align="center"><img src="Aula 4/imgs/sensor_incendio.png" alt="" width="500px">
    <p><b>Esquema de montagem do circuito</b></p>
</div>

<h4>Código</h4>

```c++
#define LED_VD 2
#define LED_VM 3
#define BUZZER 5

const int sensor_tmp = A4;
const int ldr = A5;

void setup() {
  Serial.begin(9600);
  pinMode(A5, INPUT);
  pinMode(A4, INPUT);
  pinMode(LED_VD, OUTPUT);
  pinMode(LED_VM, OUTPUT);
  pinMode(BUZZER, OUTPUT);
}
 
void loop() {
  int temperatura = analogRead(sensor_tmp);
  int luz = analogRead(ldr);
  
  temperatura = map(temperatura, 20, 358, -40, 125);
  
  Serial.print("Luz: ");
  Serial.println(luz);
  Serial.print("Temperatura: ");
  Serial.println(temperatura);
  
  if(temperatura >= 60 && luz <= 500){
    tone(BUZZER, 329);
    digitalWrite(LED_VD, LOW);
    
    for(int i = 0; i < 5; i++){
      digitalWrite(LED_VM, HIGH);
      delay(20);
      digitalWrite(LED_VM, LOW);
    }
    
  }else if(temperatura >= 60 && luz > 500){
  	tone(BUZZER, 261);
    
  }else{
  	digitalWrite(LED_VD, HIGH);
  	noTone(BUZZER);
  }
  
  delay(300);
}
```
