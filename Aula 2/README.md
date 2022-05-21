<h1>Aula 2 - Introdução ao Arduino: Teoria e prática de construção circuitos básicos com Arduino.</h1>

<a href=""><p>Resumo da aula</p></a>

<h2>Resolução dos desafios</h2>

<h3>Desafio 1 - Leds piscando alternadamente</h3>

<img src="" alt="">

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

<h3>Desafio 2 - Semáforo</h3>

<img src="" alt="">

```c++
#define LED_VERMELHO 2
#define LED_AMARELO 3
#define LED_VERDE 4

void setup() {
  pinMode(LED_VERMELHO, OUTPUT);
  pinMode(LED_AMARELO, OUTPUT);
  pinMode(LED_VERDE, OUTPUT);
}

void loop() {
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
