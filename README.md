# Konfigurera Azure IoT Hub för ESP32-S och DHT11

## Innehållsförteckning
- [Översikt](#översikt)
- [Introduktion](#introduktion)
  - [Komponenter](#komponenter)
- [Instruktioner](#instruktioner)
  - [Steg 1: Skicka Data från ESP32 till Azure IoT Hub](#steg-1-skicka-data-från-esp32-till-azure-iot-hub)
  - [Steg 2: Uppkoppling](#uppkoppling)
  - [Steg 3: Statistik](#statistik)
- [Säkerhet/Skalbarhet](#säkerhet/skalbarhet)
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

### Steg 1: Nedladdningar
1. **Installera den senaste versionen av Arduino IDE från Arduino:s officiella webbplats**: Besök [Arduino](https://www.arduino.cc/en/software) och följ instruktionerna.
2. **Installera ESP8266-paketet i Arduino IDE**: Lägg till `http://arduino.esp8266.com/stable/package_esp8266com_index.json` i din Arduino IDE.
3. **Installera Azure SDK C-biblioteket**:
   - [ArduinoJson](https://github.com/bblanchon/ArduinoJson): Installera ArduinoJson.
   - [PubSubClient](https://github.com/knolleary/pubsubclient): Installera PubSubClient.

### Steg 2: Uppkoppling
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
#define IOT_CONFIG_DEVICE_ID "YourDeviceId"
#define IOT_CONFIG_DEVICE_KEY "YourDeviceKey"
```
### Steg 3: Statistik och Dataanalys
- **Datainsamling via Cosmos DB**: Konfigurera Cosmos DB för att effektivt lagra och hantera data som samlas in från DHT11-sensorerna. Detta innebär att skapa en databasstruktur som kan ta emot och ordna data från Azure IoT Hub på ett sätt som underlättar analys och rapportering.
- **Azure Functions för datamanipulering**: Utveckla Azure Functions för att bearbeta och förbereda insamlad data för analys. Detta kan inkludera datarensning, normalisering och transformation för att säkerställa att datan är användbar och meningsfull för slutanvändaren.

### Steg 4: Visualisering med Power BI
![Power BI Visualization](./img/powerbi.png) 
- **Integration med Power BI**: Lär dig att integrera data från Cosmos DB med Power BI för att skapa dynamiska och insiktsfulla visualiseringar. Detta steg fokuserar på att överföra data från Cosmos DB till Power BI och konfigurera datakällan korrekt.
- **Utforma Dashboard i Power BI**: Skapa anpassade dashboards i Power BI som visualiserar temperaturdata i realtid. Här utnyttjar du Power BI:s avancerade visualiseringsverktyg för att skapa klara och insiktsfulla grafiska representationer av dina data.
- **Använda Query Functions för detaljerad analys**: Utveckla och tillämpa frågefunktioner i Power BI för att extrahera specifika insikter från temperaturdatan. Detta kan inkludera tidsbaserade trender, jämförelser mellan olika tidpunkter eller områden, och avancerad analys som hjälper till att identifiera mönster eller avvikelser i datan.

### Steg 5: Säkerhet/Skalbarhet
- **Integrera Azure Device Provisioning Service (DPS)**: Använd Azure DPS för att automatisera registrering och hantering av IoT-enheter för en säker och smidig uppskalning.
- **Använda Azure Key Vault och certifikat**: Implementera Azure Key Vault för att hantera och skydda känslig information som nycklar och lösenord, vilket säkerställer integriteten och säkerheten i din IoT-lösning.
- **Uttnyttja Azures flexibla betalningsplaner**: Skala din lösning kostnadseffektivt med hjälp av Azures betalningsplaner, anpassade efter ditt faktiska användningsmönster och behov.
- **Implementera MQTTS-protokollet**: Säkra dataöverföringen mellan IoT-enheter och Azure IoT Hub med MQTTS (MQTT över SSL/TLS), för att skydda data under överföring.

## Slutsats
I denna guide har vi framgångsrikt konfigurerat en robust och skalbar IoT-lösning med ESP32 och Azure IoT Hub. Genom att kombinera datalagring i Cosmos DB med avancerad dataanalys och visualisering i Power BI, har vi skapat ett kraftfullt system för att övervaka och analysera temperaturdata i realtid. Denna lösning erbjuder inte bara insiktsfull övervakning och rapportering, utan öppnar även upp för en mängd tillämpningar inom IoT, från smarta hem till affärsoptimering. Med de rätta verktygen och metoderna kan vi utnyttja IoT:s fulla potential för att skapa innovativa och effektiva lösningar.
