# 🚀 Arduino Web Server Series

Este repositório contém uma coleção de implementações de **Servidores Web utilizando Arduino** e o Shield Ethernet (W5100/W5500). Os projetos abrangem desde o básico da comunicação HTTP até sistemas de monitoramento IoT em tempo real.

## 🛠️ Tecnologias Utilizadas

* **Hardware:** Arduino (Uno/Mega), Ethernet Shield.
* **Linguagens:** C++ (Arduino), HTML5, CSS3, JavaScript.
* **Protocolos:** TCP/IP, HTTP, JSON.

---

## 📂 Projetos Incluídos

### 1. Water Volume Detector 
Sistema de monitoramento de nível de água com sensor ultrassônico e dashboard interativo.
* **Funcionalidades:** * Dashboard que consome dados via **endpoint JSON**.
    * Alertas visuais (LED) e sonoros (Buzzer) automáticos.
* **Destaque:** Uso de `fetch()` para atualização assíncrona (sem refresh de página).

### 2. Controle de Dispositivos 
Interface de controle remoto para acionamento de componentes via navegador.
* **Funcionalidades:**
    * Botões interativos com feedback visual em CSS.
    * Controle de LEDs independentes via parâmetros `GET` na URL.

### 3. Basic Web Server 
Estrutura fundamental para hospedar páginas diretamente no microcontrolador.
* **Funcionalidades:**
    * Entrega de HTML armazenado na memória Flash (`PROGMEM`).
    * Exibição do IP do servidor no Monitor Serial.

---

## 🔧 Como Usar

1.  **Bibliotecas Necessárias:**
    * `Ethernet.h`
    * `SPI.h`
    * `DistanceSensor.h` (necessária para o projeto de volume)

2.  **Configuração de Rede:**
    Altere o endereço MAC para o do seu Shield:
    ```cpp
    byte mac[6] = { 0x90, 0xA2, 0xDA, 0xXX, 0xXX, 0xXX };
    ```

3.  **Acesso:**
    Após o upload, abra o Monitor Serial (9600 bps) para verificar o IP e digite-o no seu navegador.

---

## 👥 Autores

* **Gabriel A.**
* **Felippe C.**
* **Reginaldo S.**

---
*Este projeto foi desenvolvido para fins de estudo sobre a camada de aplicação do modelo TCP/IP.*
