# 📘 CAOS Data Model – Event Transmission

This document describes the underlying data structure used by the CAOS software to send event data via webhook to external APIs.

---

## 1. 🎭 Artist

| Field                 | Type   | Description                                  |
|----------------------|--------|----------------------------------------------|
| `uuid_artist`        | `uuid` | Unique internal ID of the artist             |
| `artist_name`        | `string` | Public artist name or label                 |
| `artist_tourdateName`| `string` | Internal tour calendar name                 |

---

## 2. 🎼 Product (Program)

| Field             | Type   | Description                                      |
|------------------|--------|--------------------------------------------------|
| `uuid_product`   | `uuid` | Unique ID of the program                         |
| `program_name`   | `string` | Title/label of the program                      |

---

## 3. 📄 Contract

| Field                 | Type     | Description                                  |
|----------------------|----------|----------------------------------------------|
| `uuid_contract`      | `uuid`   | Unique contract ID                           |
| `number_contract`    | `string` | Internal contract number                     |
| `contract_form_index`| `integer`| Index for contract type (internal use)       |
| `contract_form_text` | `string` | Contract type label (e.g. public performance)|

---

## 4. 🎫 Event

| Field             | Type     | Description                             |
|------------------|----------|-----------------------------------------|
| `uuid_event`     | `uuid`   | Unique ID of the event                  |
| `date_event`     | `string` | Event date (format: YYYY-MM-DD)         |
| `time_event`     | `string` | Event start time (format: HH:MM)        |
| `notes_event`    | `string` | Internal notes                          |
| `info_text`      | `string` | Public description (optional)           |
| `time_getin`     | `string` | Artist arrival time                     |
| `time_rehearsal` | `string` | Rehearsal time                          |
| `time_doors`     | `string` | Doors open time                         |

---

## 5. 🏛️ Venue

| Field              | Type     | Description                         |
|-------------------|----------|-------------------------------------|
| `venue_name`      | `string` | Name of the venue                   |
| `venue_street`    | `string` | Street                              |
| `venue_postalcode`| `string` | Postal code                         |
| `venue_city`      | `string` | City                                |
| `venue_country`   | `string` | Country                             |
| `venue_geo_lat`   | `string` | Latitude                            |
| `venue_geo_lng`   | `string` | Longitude                           |
| `venue_homepage`  | `string` | Website of the venue                |
| `venue_occasion`  | `string` | Occasion of the event               |

---

## 6. 🎟️ Ticket Info

| Field                               | Type     | Description                                 |
|------------------------------------|----------|---------------------------------------------|
| `tickets_advancesale_internet`     | `string` | URL for online ticket sales                |
| `tickets_advancesale_internet_LINK`| `string` | Link label or button text                  |
| `tickets_advancesale_phone`        | `string` | Phone number for ticket hotline            |

---

## 🔗 Relationships (Cardinality)

```text
Artist   (1) ───< (n) Product
Artist   (1) ───< (n) Contract
Product  (1) ───< (n) Contract
Contract (1) ───< (n) Event
Event    (1) ───– (1) Venue
```

---

## 💡 Notes

- All `uuid_*` fields are internal primary keys.
- Free-text fields are optional but recommended for completeness.
- The structure corresponds to the payload described in [caos_webhook_spec.md](./caos_webhook_spec.md)

---

© jk-solution • CAOS - culture agency office software • CAOS Data Model • Updated: 2025-06-25
