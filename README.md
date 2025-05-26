# Sistema de Irrigação Inteligente com ESP32 e MQTT

Um protótipo de sistema de irrigação automático baseado em IoT que utiliza um ESP32 para monitorar a "umidade do solo" (simulada por um potenciômetro) e controlar um atuador (LED simulado). Os dados são transmitidos via MQTT para monitoramento remoto.

---

## 🛠️ Hardware Utilizado
| Componente          | Descrição                                                                 |
|---------------------|---------------------------------------------------------------------------|
| **ESP32-S2**        | Microcontrolador com Wi-Fi integrado para processamento e comunicação.    |
| **Potenciômetro**   | Simula o sensor de umidade do solo (conectado ao pino `GPIO4`).           |
| **LED**             | Substitui a bomba d'água (acionado via pino `GPIO5`).                     |
| **Resistores**      | Limitação de corrente para componentes (opcional no Wokwi).               |
| **Fonte de Alimentação** | 3.3V para o ESP32 (simulada no Wokwi).                                |

---

## 📡 Comunicação e Protocolos
### **MQTT**
- **Broker**: `broker.hivemq.com:1883` (público e sem autenticação).
- **Tópicos**:
  - `irrigacao/umidade`: Publica o valor analógico lido do potenciômetro (0–4095).
  - `irrigacao/status`: Notifica o estado do LED (`LIGADA` ou `DESLIGADA`).
- **Biblioteca**: `PubSubClient.h` para gerenciamento MQTT.

### **Wi-Fi**
- **Rede**: `Wokwi-GUEST` (simulada no ambiente Wokwi).

---

## ⚙️ Configuração do Projeto

### **Pré-requisitos**
- Ambiente de desenvolvimento (Arduino IDE ou PlatformIO).
- Bibliotecas:
  - `WiFi.h` (já incluída no ESP32).
  - `PubSubClient.h` (instale via **Library Manager**).

### **Instruções**
1. **Conexões no Wokwi**:
   - Potenciômetro → `GPIO4` (ADC).
   - LED → `GPIO5`.
   - *O ESP32 já está pré-configurado no simulador*.

2. **Código**:
   - Substitua `SSID` e `MQTT_BROKER` conforme sua rede (em hardware físico).
   - Ajuste o limiar `2500` no código para calibrar a sensibilidade.

3. **Monitoramento**:
   - Use o **Serial Monitor** (115200 baud) para debug local.
   - Conecte-se ao broker MQTT com um cliente como [MQTT Explorer](http://mqtt-explorer.com/) ou [HiveMQ Web Client](https://www.hivemq.com/demos/websocket-client/).

---

## 📝 Documentação do Código

### **Estrutura Principal**
```cpp
#include <WiFi.h>
#include <PubSubClient.h>

// Configurações de rede e MQTT
const char* SSID = "Wokwi-GUEST";
const char* MQTT_BROKER = "broker.hivemq.com";

// Pinos
#define SENSOR 4   // Pino analógico do potenciômetro
#define RELE 5     // Pino digital do LED/relé

WiFiClient espClient;
PubSubClient client(espClient);

void setup() {
  // Inicializa GPIO, Wi-Fi e MQTT
}

void reconnectMQTT() {
  // Reconecta ao broker em caso de falha
}

void loop() {
  // Lê sensor, aciona atuador e publica dados
}
