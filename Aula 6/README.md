<h1>Aula 6 - Controlando motores utilizando pontes H.</h1>

<a href="https://github.com/RAS-UFPB/Resumo-das-aulas-do-Grupo-de-Robotica/blob/main/Resumo%20aula%206"><b>Resumo da aula</b></a>

<h2>Resolução dos desafios</h2>

<h3>Desafio 1 - Faça 2 motores girarem em sentidos opostos, use um potenciômetro para decidir em qual estado os motores estarão.
</h3>

<div align='center'>
    <h4>Tabela de materiais necessários para esse desafio</h4>
    <table>
        <tr><td>Quantidade</td> <td>Item</td></tr>
        <tr><td>01</td> <td>Arduino Uno</td></tr>
        <tr><td>01</td> <td>Protoboard</td></tr>
        <tr><td>01</td> <td>Potenciômetro</td></tr>
        <tr><td>02</td> <td>Motores DC</td></tr>
        <tr><td>01</td> <td>L293D</td></tr>
        <tr><td>--</td> <td>Fios</td></tr>
    </table>
</div>

<br>
<div align="center"><img src="./imgs/desafio%208.png" alt="" width="500px">
    <p><b>Esquema de montagem do circuito</b></p>
</div>

<h4>Código</h4>

```c++
#define POTENCIOMETRO A0
#define ENTRADA1 5
#define ENTRADA2 6
#define ENTRADA3 9
#define ENTRADA4 10
#define ENABLE1 2
#define ENABLE3 3

int valorPotenc;
int estadoMovimento;

void setup() {
    Serial.begin(9600);
  
    pinMode(POTENCIOMETRO, INPUT);
    pinMode(ENTRADA1, OUTPUT);
    pinMode(ENTRADA2, OUTPUT);
    pinMode(ENTRADA3, OUTPUT);
    pinMode(ENTRADA4, OUTPUT);
    pinMode(ENABLE1, OUTPUT);
    pinMode(ENABLE3, OUTPUT);
}

void loop() {
    valorPotenc = analogRead(POTENCIOMETRO);
    estadoMovimento = map(valorPotenc, 0, 1023, 1, 3);
  
    if(estadoMovimento == 1) {
        digitalWrite(ENABLE1, HIGH);
        digitalWrite(ENABLE3, HIGH);

        analogWrite(ENTRADA1, HIGH);
        digitalWrite(ENTRADA2, LOW);
        digitalWrite(ENTRADA3, LOW);
        digitalWrite(ENTRADA4, HIGH);
    } else if(estadoMovimento == 2) {
        digitalWrite(ENABLE1, HIGH);
        digitalWrite(ENABLE3, HIGH);
    
        digitalWrite(ENTRADA1, LOW);
        digitalWrite(ENTRADA2, HIGH);
        digitalWrite(ENTRADA3, HIGH);
        digitalWrite(ENTRADA4, LOW);
    } else if(estadoMovimento == 3) {
        digitalWrite(ENABLE1, LOW);
        digitalWrite(ENABLE3, LOW);

        digitalWrite(ENTRADA1, LOW);
        digitalWrite(ENTRADA2, LOW);
        digitalWrite(ENTRADA3, LOW);
        digitalWrite(ENTRADA4, LOW);
    }
  
    Serial.println(estadoMovimento);
}
```
