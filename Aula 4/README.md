# Aula 4

[**Resumo da aula**](https://github.com/RAS-UFPB/resumo_das_aulas_do_grupo_de_sistemas_embarcados/tree/main/Resumo%20aula%204)

## Resolução dos desafios

### Desafio 1

<div align='center'>

#### Tabela de materiais necessários para esse desafio

| Quantidade | Item |
|------------|------|
| 01 | Arduino Uno |
| 03 | LED |
| 03 | Resistor 220 ohm |
| 01 | Sensor HC-SR04 |
| -- | Fios |

</div>

<br>

<div align="center">

![](/Aula%204/imgs/sensor_de_re.png)

**Esquema de montagem do circuito**

</div>

#### Código
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

### Desafio 2

<div align='center'>

#### Tabela de materiais necessários para esse desafio

| Quantidade | Item |
|------------|------|
| 01 | Arduino Uno |
| 01 | Protoboard |
| 02 | Resistor de 1 kOhm |
| 01 | Buzzer |
| 01 | Sensor LDR |
| -- | Fios |

</div>

<br>

<div align="center">

![](/Aula%204/imgs/Desafio2_despertador_solar.png)

**Esquema de montagem do circuito**

</div>

#### Código
```c++
#define BUZZER 3
#define LDR A5

void setup() {
  Serial.begin(9600);
  pinMode(LDR, INPUT);
  pinMode(BUZZER, OUTPUT);
}
 
void loop() {
  int luz = analogRead(LDR);
  
  Serial.print("Luz: ");
  Serial.println(luz);
  
  if(luz <= 400){
    tone(BUZZER, 329);
  	delay(100);
    noTone(BUZZER);
    delay(100);
  }
}
```

### Desafio 3

<div align='center'>

#### Tabela de materiais necessários para esse desafio

| Quantidade | Item |
|------------|------|
| 01 | Arduino Uno |
| 01 | Protoboard |
| 01 | Resistor de 5 kOhm |
| 01 | Servo motor |
| 01 | Sensor DHT11 |
| -- | Fios |

</div>

<br>

<div align="center">

![](/Aula%204/imgs/Desafio3_controle_de_estufa.png)

**Esquema de montagem do circuito**

</div>

#### Código
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
