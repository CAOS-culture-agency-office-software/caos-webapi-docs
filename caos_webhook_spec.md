# 📘 CAOS Webhook Interface

This document describes the webhook interface of the CAOS software for automatically sending tour events to external web servers (e.g., artist websites).

---

## 1. Purpose

CAOS transmits all tour dates marked as "Online" via `HTTP POST` to one or more configured API endpoints (usually artist-specific websites or platforms).

---

## 2. Configuration

- Each tour plan (calendar) can be linked to its own API endpoint.
- Alternatively, multiple tour plans can use the same endpoint.
- CAOS manages the transfer process automatically in the background.

---

## 3. Security

- An optional **API key** can be added for authentication.
- The key can be passed via query string or HTTP header.

**Example URL with API key:**
```
https://example.com/api-endpoint?key=YOUR_API_KEY
```

---

## 4. Payload Format

CAOS sends a `JSON array` containing one or more event objects to the target API.

### 📤 Transmission Options

#### 🔹 Standard JSON

- Method: `POST`
- Header:
  ```
  Content-Type: application/json
  ```
- Body: Raw JSON array

#### 🔹 Base64-encoded JSON (optional)

- Header:
  ```
  Content-Type: application/json
  Content-Transfer-Encoding: base64
  ```
- Body: Base64 string representing the JSON content

💡 The receiving server must decode the Base64 string before parsing the JSON.

---

### 🔄 Sample JSON Payload (anonymized)

The JSON payload consists of an array of objects.
Each object represents a single event (e.g., tour date) with all associated information such as artist, program, contract details, time specifications, venue, and publication status.

**Structure:**
```json
{
  "artists_Tourdates": [
    {
      // Event 1 (e.g., tour date)
    },
    {
      // Event 2
    },
    ...
  ]
}
```

**Example of a single event object:**
```json
{
  "artist_name": "Artist A",
  "artist_tourdateName": "Tour A",
  "contract_form_index": 1,
  "contract_form_text": "public performance (EN)",
  "date_event": "16.05.2029",
  "info_text": "Event description",
  "notes_event": "Remarks about this event",
  "number_contract": "XYZ123",
  "program_name": "Program title",
  "tickets_advancesale_internet": "https://example.com",
  "tickets_advancesale_internet_LINK": "Tickets",
  "tickets_advancesale_phone": "+49-000-000000",
  "time_doors": "18:00",
  "time_event": "18:30",
  "time_getin": "17:30",
  "time_rehearsal": "16:15–19:00",
  "time_catering": "16:00",
  "time_curfew": "23:00",
  "time_pause": "20:00–20:20",
  "time_photosession": "17:45",
  "time_showende": "22:00",
  "tickets_advancesale_internet_date_event": "https://example.com/presale/2025-07-16",
  "tickets_advancesale_phone_date_event": "+49-000-000001",
  "tickets_advancesale_start_date_event": "16.05.2029",
  "info_text_date_event": "Special event info for this date",
  "venue_name_date_event": "Special Venue Name for this event date",
  "uuid_contract": "uuid-contract",
  "uuid_artist": "uuid-artist",
  "uuid_event": "uuid-event",
  "uuid_product": "uuid-product",
  "venue_city": "City",
  "venue_country": "Country",
  "venue_geo_lat": "52.0000",
  "venue_geo_lng": "13.0000",
  "venue_homepage": "https://venue.example.com",
  "venue_name": "Venue X",
  "venue_occasion": "Occasion",
  "venue_postalcode": "12345",
  "venue_street": "Street 1"
}
```

---

## 5. API Response

The receiving API should return a JSON response:

```json
{ "status": "ok" }
```

In case of error:

```json
{ "status": "error", "message": "Invalid API key" }
```

---

## 6. 🧪 Test Environment

A secure Web API test interface is available for verified partners.

### Available Features

- Set API endpoint URL
- Optional API key input
- Buttons for raw JSON or Base64 JSON transmission
- Editable example payload
- Visible HTTP response output

---

## 7. Developer Notes

✅ Accept and process JSON arrays  
✅ Use `uuid_event` for unique identification  
✅ Handle authentication if API key is used  
✅ Support both plain and Base64 transmission

---

© jk-solution • CAOS - culture agency office software • CAOS Web-API • Updated: 2025-06-25
