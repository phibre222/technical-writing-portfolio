# Simple Weather API – Dokumentation (v1.0)

Die Simple Weather API stellt Wetterdaten basierend auf einer Stadt oder geografischen Koordinaten bereit.  
Sie eignet sich als Grundlage für mobile Apps, Web-Widgets oder Server-Integrationen.

---

## 1. Übersicht

**Base URL:**  
https://api.simpleweather.example/v1

**Authentifizierung:**  
Die API verwendet einen statischen API-Key.

**Header Beispiel:**
Authorization: Bearer YOUR_API_KEY
Accept: application/json

---

## 2. Endpunkte

### 2.1 Aktuelles Wetter abrufen
GET /weather/current

#### Zweck  
Liefert aktuelle Wetterinformationen für einen Ort.

#### Anfrageparameter

| Name        | Typ     | Pflicht | Beschreibung |
|-------------|---------|---------|--------------|
| `city`      | string  | nein    | Name der Stadt (z. B. „Berlin“). Wird bevorzugt verwendet. |
| `lat`       | float   | nein    | Breitengrad. |
| `lon`       | float   | nein    | Längengrad. |
| `units`     | string  | nein    | Einheitssystem: `metric` (Standard) oder `imperial`. |

**Hinweis:**  
Es muss **entweder** `city` **oder** (`lat` **und** `lon`) angegeben werden.

#### Beispielanfrage
GET https://api.simpleweather.example/v1/weather/current?city=Berlin&units=metric

#### Beispielantwort (200 OK)
```json
{
  "location": "Berlin",
  "temperature": 12.4,
  "unit": "C",
  "condition": "Cloudy",
  "humidity": 68,
  "wind_kmh": 14,
  "timestamp": "2025-11-12T14:20:00Z"
}
