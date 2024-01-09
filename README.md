# Konfigurera Azure IoT Hub för ESP32-S och DHT11

## Innehållsförteckning
- [Översikt](#översikt)
- [Introduktion](#introduktion)
  - [Komponenter](#komponenter)
- [Instruktioner](#instruktioner)
  - [Steg 1: Skicka Data från ESP32 till Azure IoT Hub](#steg-1-skicka-data-från-esp32-till-azure-iot-hub)
  - [Steg 2: Uppkoppling](#steg-2-uppkoppling)
  - [Steg 3: Statistik](#steg-3-statistik)
- [Säkerhet/Skalbarhet](#säkerhetskalbarhet)
- [Slutsats](#slutsats)
- [Azure Funktioner och Databas Kod](#azure-funktioner-och-databas-kod)

## Översikt
![IoT Diagram](./img/iot-diagram.drawio.png)
*Översikt på diagramet för IoT-flödet setup.*

## Introduktion
Detta projekt är en omfattande guide för att konfigurera och använda Azure IoT Hub för att samla in och analysera data från en ESP32-S enhet kopplad till en DHT11-sensor. Genom att följa denna guide kommer du att kunna skapa en IoT-lösning som kan samla in, bearbeta och visualisera data i realtid. Detta kan vara särskilt användbart för olika IoT-applikationer, som att övervaka miljöförhållanden, skapa smarta hemlösningar eller för att förbättra affärsprocesser genom att använda datainsikter. Slutresultatet kommer att vara en fullt fungerande IoT-lösning som kan skala upp för att hantera stora mängder data och ge värdefulla insikter genom visualisering i PowerBI.

## Komponenter
- Ett aktivt Azure-konto.
- En IoT-hub på ditt Azure-konto.
- En ESP32-S och DHT11 som är korrekt konfigurerad och ansluten.
- Arduino IDE för att programmera ESP32.
- Stream Analytics för att bearbeta och analysera data.
- PowerBI för att visualisera data.
- Cosmos DB för att lagra data.

![ESP32 Image](./img/esp32bild.png)
*Esp32 och DHT11 Setup*

![Diagram Presentation](./img/diagram_presentation.svg)
*Hur komponenterna ska integreras med molnet*

## Steg-för-steg Instruktioner

###  Nedladdningar
1. **Installera den senaste versionen av Arduino IDE från Arduino:s officiella webbplats**: Besök [Arduino](https://www.arduino.cc/en/software) och följ instruktionerna.
2. **Installera ESP8266-paketet i Arduino IDE**: Lägg till (http://arduino.esp8266.com/stable/package_esp8266com_index.json) i din Arduino IDE.
3. **Installera Azure SDK C-biblioteket**:
   - [ArdiunoJson](https://github.com/bblanchon/ArduinoJson): Installera ArduinoJson.
   - [PubSubClient](https://github.com/knolleary/pubsubclient): Installera PubSubClient.

###  Uppkoppling
1. **Gå till din IoT Hub**: Navigera till din IoT Hub i Azure-portalen.
2. **Lägg till en enhet**:
   - Använd sensorn (temperatur- och fuktighetsmätare) för datainsamling.
   - Kolla in datainsamlingen på din IoT-enhet.
   ![Data Statistik](./img/statistik.png)
   - Bekräfta att enheten, t.ex. "ESP32-DHT11-Device", är insamlad och tar emot data.
   - Lämna "Authentication type" som "Symmetric Key".

```csharp
// Wifi
#define IOT_CONFIG_WIFI_SSID "SSID"
#define IOT_CONFIG_WIFI_PASSWORD "PWD"
// Azure IoT Config
#define IOT_CONFIG_IOTHUB_FQDN "[your Azure IoT host name].azure-devices.net"
#define IOT_CONFIG 

### Statistik
- **Datainsamling via Cosmos DB**: Använd Cosmos DB för att lagra och hantera data från sensorerna.
- **Azure Functions**: Anslut Azure Functions till IoT Hub för att bearbeta inkommande data.

### Testning och Validering
- **Verifiera anslutningen**: Kontrollera att din ESP32-enhet korrekt överför data till Azure IoT Hub.
- **Felsökning**: Använd Azure IoT Hub's inbyggda monitor för att identifiera och åtgärda eventuella problem.

### Steg 5: Säkerhet/Skalbarhet
- **Integrera Azure Device Provisioning Service (DPS)**: För att automatisera registrering och hantering av enheter.
- **Använda Azure Key Vault och certifikat**: För att skydda känslig information som nycklar och lösenord.
- **Uttnyttja Azures flexibla betalningsplaner**: För kostnadseffektiv skalning baserat på användningsmönster.
- **Implementera MQTTS-protokollet**: För säker dataöverföring mellan IoT-enheter och Azure IoT Hub.

## Slutsats
Detta projekt ger en komplett lösning för att övervaka och analysera miljöförhållanden genom att kombinera ESP32 med Azure IoT Hub. Data från temperatur- och luftfuktighetssensorer lagras i Cosmos DB och presenteras i realtid via Power BI. Projektet erbjuder en robust och skalbar lösning för miljöövervakning och dataanalys, vilket kan vara avgörande för olika tillämpningar inom IoT.
