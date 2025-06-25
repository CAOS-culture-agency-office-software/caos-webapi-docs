# 📘 Datenmodell: Künstlerbuchung (CAOS)

Dieses Dokument beschreibt die zugrunde liegenden Entitäten und Datenfelder, die im Rahmen der Webhook-Übertragung durch CAOS an externe API-Endpunkte gesendet werden.

---

## 1. 🎭 Artist (Künstler:in)

| Feld                  | Typ     | Beschreibung                                      |
|-----------------------|----------|---------------------------------------------------|
| `uuid_artist`         | `uuid`   | Interne eindeutige ID des Künstlers               |
| `artist_name`         | `string` | Öffentliche Bezeichnung des Künstlers             |
| `artist_tourdateName` | `string` | Interner Kalendername (Tourplan)                 |

---

## 2. 🎼 Product (Programm)

| Feld             | Typ     | Beschreibung                                          |
|------------------|----------|-------------------------------------------------------|
| `uuid_product`   | `uuid`   | Eindeutige ID des Programms                          |
| `program_name`   | `string` | Titel/Bezeichnung des Programms                     |

---

## 3. 📄 Contract (Vertrag)

| Feld              | Typ     | Beschreibung                                         |
|-------------------|----------|------------------------------------------------------|
| `uuid_contract`   | `uuid`   | Eindeutige ID des Vertrags                          |
| `number_contract` | `string` | Interne Vertragsnummer                              |
| `contract_form_index` | `integer` | Index zur Vertragsart-Auswahl (intern)       |
| `contract_form_text`  | `string`  | Beschreibung der Vertragsart (z. B. öffentlich) |

---

## 4. 🎫 Event (Spieltermin)

| Feld            | Typ     | Beschreibung                                  |
|-----------------|----------|-----------------------------------------------|
| `uuid_event`    | `uuid`   | Eindeutige ID des Spieltermins               |
| `date_event`    | `string` | Veranstaltungsdatum (Format: YYYY-MM-DD)     |
| `time_event`    | `string` | Beginn der Veranstaltung (Format: HH:MM)     |
| `notes_event`   | `string` | Interne Notizen zum Termin                   |
| `info_text`     | `string` | Freitext zur Veranstaltung (optional)        |
| `time_getin`    | `string` | Künstler-Ankunftszeit                         |
| `time_rehearsal`| `string` | Probenzeit                                   |
| `time_doors`    | `string` | Einlasszeit des Publikums                    |

---

## 5. 🏛️ Venue (Veranstaltungsort)

| Feld              | Typ     | Beschreibung                              |
|-------------------|----------|-------------------------------------------|
| `venue_name`      | `string` | Name der Location                         |
| `venue_street`    | `string` | Straße                                    |
| `venue_postalcode`| `string` | Postleitzahl                              |
| `venue_city`      | `string` | Stadt                                     |
| `venue_country`   | `string` | Land                                      |
| `venue_geo_lat`   | `string` | Geokoordinate: Breitengrad                |
| `venue_geo_lng`   | `string` | Geokoordinate: Längengrad                 |
| `venue_homepage`  | `string` | Website der Location                      |
| `venue_occasion`  | `string` | Anlass der Veranstaltung                  |

---

## 6. 🎟️ Ticket-Informationen

| Feld                              | Typ     | Beschreibung                                  |
|-----------------------------------|----------|-----------------------------------------------|
| `tickets_advancesale_internet`     | `string` | URL zur Online-Vorverkaufsstelle             |
| `tickets_advancesale_internet_LINK`| `string` | Bezeichnung des Links                        |
| `tickets_advancesale_phone`        | `string` | Telefonnummer der Vorverkaufsstelle          |

---

## 🔗 Beziehungen (Kardinalitäten)

```text
Artist   (1) ───< (n) Product
Artist   (1) ───< (n) Contract
Product  (1) ───< (n) Contract
Contract (1) ───< (n) Event
```

---

## 💡 Hinweise

- Alle `uuid_*` Felder sind interne Primärschlüssel zur eindeutigen Identifikation.
- Felder mit Freitext sind optional, sollten aber konsistent verwendet werden.
- Die Feldstruktur entspricht der Payload der Webhook-Schnittstelle (siehe: [caos_webhook_interface.md](./caos_webhook_interface.md)).

---

© jk-solution | CAOS Datenmodell | Stand: 2025-06-25
