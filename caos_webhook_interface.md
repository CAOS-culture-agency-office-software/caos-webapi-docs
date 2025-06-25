# 📘 Schnittstellenbeschreibung: CAOS Webhook zu Künstler-Webseiten

## 1. Zweck der Schnittstelle

Die CAOS-Software sendet alle als „Online“ markierten Spieltermine eines Künstler-Tourplans automatisch per `HTTP POST` an eine oder mehrere konfigurierte Web-APIs (z. B. auf Künstler-Webseiten).

---

## 2. Konfiguration

- Jeder Tourplan (artist_tourdateName) kann eine eigene API-URL (Zieladresse) erhalten.
- Alternativ können mehrere Tourpläne auf denselben Endpunkt zeigen.
- CAOS übernimmt die Verwaltung und automatische oder manuelle Auslösung dieser Transfers.

---

## 3. Sicherheit

- Optional kann ein Schnittstellen-Schlüssel (API-Key) verwendet werden. *(Empfohlen)*
- Der Schlüssel kann als URL-Parameter oder HTTP-Header übermittelt werden.

**Beispiel-URL mit API-Key:**
```
https://example.com/api-endpoint?key=YOUR_API_KEY
```

---

## 4. Request: Übertragung per POST

CAOS sendet einen JSON-Array mit Spielterminen an die konfigurierte API-URL.

**HTTP-Methode:** `POST`  
**Header:**
```
Content-Type: application/json
```

**Beispielaufruf via curl:**
```bash
curl -X POST https://example.com/api-endpoint \
     -H "Content-Type: application/json" \
     --data @$json
```

---

## 5. Struktur des Payloads

Die JSON-Daten enthalten pro Spieltermin ein Objekt mit u. a. folgenden Feldern:

```json
{
  "uuid_artist": "uuid",
  "artist_name": "Calmus Ensemble",
  "artist_tourdateName": "Calmus",
  "uuid_contract": "uuid",
  "number_contract": "Testvertrag",
  "uuid_event": "uuid",
  "date_event": "2025-10-01",
  "time_event": "18:30",
  "program_name": "Programm (nach Absprache)",
  "venue_name": "Kaisersaal",
  "venue_city": "Stadt",
  "venue_country": "Land",
  "tickets_advancesale_internet": "[Tickets] Internet",
  "tickets_advancesale_internet_LINK": "Linkbezeichnung",
  "tickets_advancesale_phone": "",
  "time_getin": "",
  "time_rehearsal": "",
  "time_doors": "",
  "notes_event": "Notiz 18:30 (Konzert)",
  "venue_postalcode": "PLZ",
  "venue_street": "Straße",
  "venue_geo_lat": "",
  "venue_geo_lng": "",
  "venue_homepage": "",
  "venue_occasion": ""
}
```

---

## 6. Rückgabe / Response

Die Web-API sollte einen JSON-Response senden, z. B.:

```json
{ "status": "ok" }
```

Bei Fehlern:

```json
{ "status": "error", "message": "Ungültiger API-Key" }
```

---

## 7. API-Simulator (Testumgebung)

Ein Test-Interface steht zur Verfügung unter:

👉 **https://caos-software-service.de/fmi/webd/CAOS_ADMIN**  
🔐 Benutzer: `API`  
🔑 Passwort: `181835`

---

## 8. Hinweise für Webentwickler

✅ JSON-Array empfangen und iterieren  
✅ Eindeutigkeit der Events via `uuid_event` sicherstellen  
✅ Optionalen API-Key validieren  
✅ Aufruf regelmäßig oder asynchron entgegennehmen

---

© jk-solution - CAOS - culture agency office software | CAOS WebAPI | Stand: 2025-06-25
