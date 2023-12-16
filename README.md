<!DOCTYPE html>
<html>
<head>
<title>Circuito Simples</title>
</head>
<body>

<h1>T=Sensor de temperatura</h1>
<p>Circuito com sensor de temperatura, led, buzina, motor e arduino. Funcionamento: quando a temperatura fica maior ou igual a 30°C o led e a buzina são ativados para alertar e o motor é ativado para resfriar o ambiente.</p>

// C++ code
// Inicialização dos pinos 
const int TempPin = A0;
const int LedPin = 10;
const int BuzPin = 11;
const int MotorPin = 8;

void setup() {
  pinMode(TempPin, INPUT);
  pinMode(LedPin, OUTPUT);
  pinMode(BuzPin, OUTPUT);
  pinMode(MotorPin, OUTPUT);

// Inicialização da comunicação serial para exibição da temperatura
  Serial.begin(9600);
}

void loop() {
// Leitura do sensor
  int temperatura = analogRead(TempPin);

// Conversão para temperatura em Celsius
  float temperaturaC = (temperatura * 5.0 / 1024.0 - 0.5) * 100.0;

// Exibição da temperatura no monitor serial
  Serial.println(temperatura);
  Serial.print("Temperatura: ");
  Serial.print(temperaturaC);
  Serial.println("°C");

// Verificação da temperatura 
  if (temperaturaC >= 30) {
    digitalWrite(LedPin, HIGH); // Liga o LED
    tone(BuzPin, 1000); // Ativa a buzina com frequência de 1KHz
    analogWrite(MotorPin, 255); // Ativa o motor do ventilador na máxima velocidade
  } else {
    digitalWrite(LedPin, LOW); // Desliga o LED
    noTone(BuzPin); // Desativa a buzina
    analogWrite(MotorPin, 0); // Desliga o motor do ventilador
  }

  delay(2000); // Aguarda 2 segundos antes da próxima leitura
}

</body>
</html>
