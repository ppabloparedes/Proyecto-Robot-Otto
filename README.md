# 🤖 Proyecto Robot Otto

---

### 1️⃣ Código prueba de 4 servos

#### 🔌 Pines Conectados:
| Componente | Pin Arduino |
|-----------|------------|
| Servo 1 | 2 |
| Servo 2 | 3 |
| Servo 3 | 4 |
| Servo 4 | 5 |
| Sensor Ultrasónico (Trigger) | 6 |
| Sensor Ultrasónico (Echo) | 7 |
| Sensor Sonido | A0 |

#### 🛠️ Materiales:
- 4 Servos
- Sensor ultrasónico HC-SR04
- Sensor de sonido analógico
- Arduino (o compatible)
- Cables de conexión

#### 💻 Código:
```cpp
#include <Servo.h>

Servo servo1;
Servo servo2;
Servo servo3;
Servo servo4;

int sensorSonido = A0;
int umbral = 500;

int trigPin = 6;
int echoPin = 7;

long duracion;
int distancia;

void medirDistancia() {
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  duracion = pulseIn(echoPin, HIGH);
  distancia = duracion * 0.034 / 2;

  Serial.print("Distancia: ");
  Serial.print(distancia);
  Serial.println(" cm");
}

void setup() {
  servo1.attach(2);
  servo2.attach(3);
  servo3.attach(4);
  servo4.attach(5);

  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);

  Serial.begin(9600);

  int valorInicial = analogRead(sensorSonido);
  Serial.print("Valor de sonido inicial: ");
  Serial.println(valorInicial);
}

void loop() {
  int valor = analogRead(sensorSonido);

  if (valor > umbral) {
    Serial.print("Sonido detectado (activacion): ");
    Serial.println(valor);

    servo1.write(0);
    delay(200);
    medirDistancia();
    servo1.write(90);
    delay(500);
    medirDistancia();

    servo2.write(0);
    delay(200);
    medirDistancia();
    servo2.write(90);
    delay(500);
    medirDistancia();

    servo3.write(0);
    delay(200);
    medirDistancia();
    servo3.write(90);
    delay(500);
    medirDistancia();

    servo4.write(0);
    delay(200);
    medirDistancia();
    servo4.write(90);
    delay(500);
    medirDistancia();

    servo1.write(0);
    servo2.write(0);
    delay(200);
    medirDistancia();

    servo1.write(180);
    servo2.write(180);
    delay(500);
    medirDistancia();

    servo1.write(0);
    servo2.write(0);
    delay(200);
    medirDistancia();

    servo3.write(0);
    servo4.write(0);
    delay(200);
    medirDistancia();

    servo3.write(180);
    servo4.write(180);
    delay(500);
    medirDistancia();

    servo3.write(0);
    servo4.write(0);
    delay(200);
    medirDistancia();

    int valorFinal = analogRead(sensorSonido);
    Serial.print("Valor de sonido final: ");
    Serial.println(valorFinal);

    delay(2000);
  }
}
