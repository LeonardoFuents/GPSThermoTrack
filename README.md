# ThermoTrack — Módulo GPS

Firmware para **ESP32** que lê a localização do módulo **SIM808** por comandos AT e publica as coordenadas via **MQTT**. Faz parte do projeto **ThermoTrack**.

> O firmware completo (temperatura, umidade, movimento e GPS) está em [CodigoThermoTrack](https://github.com/LeonardoFuents/CodigoThermoTrack).

## O que ele faz

- Liga e configura o GPS do SIM808 (`AT+CGPSPWR`, `AT+CGPSRST`, `AT+CGPSMODE`)
- Solicita a posição a cada **3 segundos** (`AT+CGPSINF=0`) e verifica o status do fix a cada 15 s
- Converte as coordenadas do formato `DDMM.MMMM` para graus decimais
- Descarta leituras inválidas enquanto o GPS não tem fix
- Publica latitude e longitude em JSON no broker MQTT

## Hardware

| Componente | Ligação |
|---|---|
| ESP32 DevKit | — |
| SIM808 | RX 16 / TX 17 (UART2) |

## Tecnologias

- C++ / Arduino framework
- [PlatformIO](https://platformio.org/)
- PubSubClient (MQTT)

## Como compilar

1. Instale o VS Code com a extensão **PlatformIO**.
2. Preencha o Wi-Fi em `include/senhas.h` (`SSID` e `SENHA`).
3. Compile e grave:

```bash
pio run --target upload
pio device monitor -b 115200
```

## Autor

**Leonardo Fuentes** — [GitHub](https://github.com/LeonardoFuents)
