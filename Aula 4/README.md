<h1>Aula 4</h1>

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
<div align="center"><img src="/Aula 4/imgs/sensor_de_re.png" alt="" width="500px">
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
        <tr><td>02</td> <td>Resistor de 1 kOhm</td></tr>
        <tr><td>01</td> <td>Buzzer</td></tr>
        <tr><td>01</td> <td>Sensor LDR</td></tr>
        <tr><td>--</td> <td>Fios</td></tr>
    </table>
</div>

<br>
<div align="center"><img src="/Aula 4/imgs/Desafio2_despertador_solar.png" alt="" width="500px">
    <p><b>Esquema de montagem do circuito</b></p>
</div>

<h4>Código</h4>

```c++
#define BUZZER 4

const int ldr = A5;

void setup() {
  Serial.begin(9600);
  pinMode(A5, INPUT);
  pinMode(BUZZER, OUTPUT);
}
 
void loop() {
  int luz = analogRead(ldr);
  
  Serial.print("Luz: ");
  Serial.println(luz);
  
  if(luz <= 400){
    tone(BUZZER, 329);
  	delay(100);
    noTone(BUZZER);
    delay(100);
  }
  else
    delay(200);
}
```


<h3>Desafio 3</h3>

<div align='center'>
    <h4>Tabela de materiais necessários para esse desafio</h4>
    <table>
        <tr><td>Quantidade</td><td>Item</td></tr>
        <tr><td>01</td> <td>Arduino Uno</td></tr>
        <tr><td>01</td> <td>Protoboard</td></tr>
        <tr><td>01</td> <td>Resistor de 5 kOhm</td></tr>
        <tr><td>01</td> <td>Servo motor</td></tr>
        <tr><td>01</td> <td>Sensor DHT11</td></tr>
        <tr><td>--</td> <td>Fios</td></tr>
    </table>
</div>

<br>
<div align="center"><img src="/Aula 4/imgs/Desafio3_controle_de_estufa.png" alt="" width="500px">
    <p><b>Esquema de montagem do circuito</b></p>
</div>

<h4>Código</h4>

```c++
#include <DHT.h>
#include <Servo.h>

#define DHTPIN 2          // Pino do sensor DHT11
#define DHTTYPE DHT11     // Tipo de sensor DHT11

DHT dht(DHTPIN, DHTTYPE);
Servo myservo;

bool servoRotated = false;

void setup() {
  Serial.begin(9600);
  dht.begin();
  myservo.attach(3);   // Pino do servo motor
}

void loop() {
  float temp = dht.readTemperature();     // Ler a temperatura em graus Celsius
  float umid = dht.readHumidity();        // Ler a umidade relativa em percentual

  Serial.print("Temperatura: ");
  Serial.print(temp);
  Serial.print("°C | Umidade: ");
  Serial.print(umid);
  Serial.println("%");

  if (temp >= 40.0 && !servoRotated) {
    myservo.write(90);  // Girar o servo motor 90 graus
    servoRotated = true;
  } else if (temp <= 38.0 && servoRotated) {
    myservo.write(0);   // Retornar o servo à posição original
    servoRotated = false;
  }

  if (umid > 70.0) {
    myservo.write(45);  // Abrir o servo motor por 45 graus
    delay(1000);        // Manter aberto por 1 segundo
    myservo.write(0);   // Retornar o servo à posição original
  }

  delay(2000);  // Aguardar 2 segundos entre leituras
}
```
