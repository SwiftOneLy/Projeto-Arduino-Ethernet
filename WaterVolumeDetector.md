```
/**
 * @authors Gabriel A.,
 * Felippe C., Reginaldo S */

#include <Ethernet.h>
#include <DistanceSensor.h>
#include <unistd.h>

#define VERMELHO 8

constexpr int TrigPin = 2;
constexpr int EchoPin = 3;

DistanceSensor<TrigPin, EchoPin> sensor;

// 90:A2:DA:36:56:67
byte mac[6] = { 0x90, 0xA2, 0xDA, 0x36, 0x56, 0x67 };
EthernetServer server(80);

const char page[] PROGMEM = R"HTML(
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Arduino - Temperature visualizer</title>

    <style>
        body {
            font-family: Calibri, 'Trebuchet MS', sans-serif;
            text-align: center;
        }

        h1 {
            font-size: 1.7rem;
        }

        #container {
            background-color: rgba(44, 44, 255, 0.26);
            width: 30%;
            margin: 0 auto;
            padding: 2px;
        }

        #warning {
            color: red;
            font-size: 1.2rem;
            font-weight: bold;
        }
    </style>
</head>

<body>
    <h1>Water volume detector</h1>

    <div id="container">
        <span>Distância atual: </span>
        <span id="d"></span>
    </div>

    <span id="warning"></span>
</body>

<script>
    const update = () => {
        fetch("/json")
            .then(response => response.json())
            .then(data => {
                let distance = data.distancia;
                const distanceElement = document.getElementById("d");
                const warning = document.getElementById("warning");

                distanceElement.innerText = distance;

                if(distance < 30) {
                    if(distance < 10) {
                        warning.innerText = "a distância está abaixo de 10. Todos entrem em pânico!";
                    } else {
                        warning.innerText = "Cuidado, a distância está abaixo de 30.";
                    }
                } else {
                    warning.innerText = "";
                }

                console.log(distance);
            });
    }

    setInterval(update, 200);
</script>
</html>
)HTML";

void setup() {
    Serial.begin(9600);

    Ethernet.begin(mac);
    server.begin();

    // Buzzer
    pinMode(9, OUTPUT);

    // LED
    pinMode(8, OUTPUT);

    sensor.begin();
}

void loop() {
    int distancia = sensor.tick();
    if (distancia == sensor.NREADY) return;

    zezinhoFunction(distancia);
    Serial.println(distancia);

    if (distancia < 30) {
        if (distancia < 10) {
            digitalWrite(8, HIGH);
            delay(200);

            digitalWrite(8, LOW);
            delay(200);

            tone(9, 250);
        } else {
            digitalWrite(8, HIGH);
            noTone(9);
        }
    } else {
        digitalWrite(8, LOW);
        noTone(9);
    }
}

void zezinhoFunction(int distancia) {
    EthernetClient client = server.available();
    if (client) {
        String request = "";

        while (client.available()) {
            char c = client.read();
            request += c;
        }

        // endpoint JSON
        if (request.indexOf("GET /json") >= 0) {
            Serial.println("funcionando");

            client.println(F("HTTP/1.1 200 OK"));
            client.println(F("Content-Type: application/json"));
            client.println(F("Connection: close"));
            client.println();

            client.print("{\"distancia\":");
            client.print(distancia);
            client.print("}");

            delay(1);
            client.stop();
            return;
        }

        // página principal
        client.println(F("HTTP/1.1 200 OK"));
        client.println(F("Content-Type: text/html"));
        client.println(F("Connection: close"));
        client.println();

        client.print((__FlashStringHelper *)page);

        delay(1);

        client.stop();
    }
}
```
