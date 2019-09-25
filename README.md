# SensorAgua

Agradecimento ao Leonardo Pereira e a Iulisloi Zacarias.

  MQTT - como instalar -> https://www.youtube.com/watch?v=GMMH6qT8_f4
  ESP - como instalar -> https://www.youtube.com/watch?v=4d8joORYTIA&t=1s
  Wi-Fi Manager  como instalar -> https://www.youtube.com/watch?v=wWO9n5DnuLA
  OTA -> já está incluida no IDE do Arudino
  
  NodeMcu Lua ESP8266 ESP-12F
  https://www.banggood.com/Geekcreit-Doit-NodeMcu-Lua-ESP8266-ESP-12F-WIFI-Development-Board-p-985891.html
  
  Sensor de Fluxo:
  https://www.banggood.com/G34-Inch-Liquid-Water-Flow-Sensor-Switch-Copper-Hall-Effect-Flowmeter-Meter-p-1188160.html
  
  Sensor Ultrassônico
  https://www.banggood.com/Wholesale-Geekcreit-Ultrasonic-Module-HC-SR04-Distance-Measuring-Ranging-Transducer-Sensor-DC-5V-2-450cm-p-40313.html


  Ligação Sensor de Fluxo:
  Fio Vermelho --> Pino VIN 5V
  Fio Preto    --> Pino GND (Qualquer um)
  Fio Amarelo  --> Pino D3 (GPIO0)

  Ligação Sensor HC-SR04:
  Vcc  -->  Pino VIN 5V
  Trig -->  Pino D6 (GPIO12)
  Echo -->  Pino D5 (GPIO14)
  Gnd  -->  Pino Gnd (Qualquer um)

  OBS:
  - Alimentar ambos sensores com 5V //VIN

  Ao enviar pela primeira vez seu ESP vai ficar em modo AP, com seu celular conecte no nome de sinal abra o 192.168.4.1 e defina o nome e senha de sua rede wifi

Configuração no Home Assistant:
<pre>
sensor:
  - platform: mqtt
    state_topic: 'SensorAgua/contagem'
    name: 'Vazão de Água'
    icon: mdi:water
    unit_of_measurement: 'litros/s'
    value_template: '{{ value_json.vazao }}'
  - platform: mqtt
    state_topic: 'SensorAgua/contagem'
    name: 'Consumo de Água'
    icon: mdi:water-percent
    unit_of_measurement: 'litros'
    value_template: '{{ value_json.consumo_agua }}'
  - platform: mqtt
    state_topic: 'SensorAgua/contagem'
    name: "Distancia D'agua"
    icon: mdi:ruler
    unit_of_measurement: 'cm'
    value_template: '{{ value_json.distancia }}'

utility_meter:
  consumo_de_agua_dia:
    source: sensor.consumo_de_agua
    cycle: daily
  consumo_de_agua_semana:
    source: sensor.consumo_de_agua
    cycle: weekly
  consumo_de_agua_mes:
    source: sensor.consumo_de_agua
    cycle: monthly
  consumo_de_agua_ano:
    source: sensor.consumo_de_agua
    cycle: yearly
    </pre>
<img src="https://raw.githubusercontent.com/remontti/SensorAgua/master/agua.png">
