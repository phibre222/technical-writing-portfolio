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

2.2 Vorhersage abrufen

GET /weather/forecast

Zweck

Liefert eine 5-Tage-Vorhersage in 3-Stunden-Intervallen.
Anfrageparameter
Name	Typ	Pflicht	Beschreibung
city	string	nein	Stadtname.
lat	float	nein	Breitengrad.
lon	float	nein	Längengrad.
units	string	nein	metric oder imperial.
limit	int	nein	Anzahl der zurückzugebenden Zeitpunkte (Standard = 10).
Beispielanfrage

GET https://api.simpleweather.example/v1/weather/forecast?city=Köln&limit=4

Beispielantwort (200 OK)

{
  "location": "Köln",
  "forecast": [
    {
      "timestamp": "2025-11-12T15:00:00Z",
      "temperature": 10.1,
      "condition": "Rain"
    },
    {
      "timestamp": "2025-11-12T18:00:00Z",
      "temperature": 9.4,
      "condition": "Rain"
    },
    {
      "timestamp": "2025-11-12T21:00:00Z",
      "temperature": 8.0,
      "condition": "Cloudy"
    },
    {
      "timestamp": "2025-11-13T00:00:00Z",
      "temperature": 7.2,
      "condition": "Clear"
    }
  ]
}

3. Fehlercodes
Statuscode	Meaning	Beschreibung
400 Bad Request	Parameter fehlen oder sind ungültig.	
401 Unauthorized	API-Key fehlt oder ist ungültig.	
404 Not Found	Angegebener Ort konnte nicht gefunden werden.	
429 Too Many Requests	Ratenlimit überschritten (Standard: 60 Requests / Minute).	
500 Internal Server Error	Unerwarteter Serverfehler.	
Fehlerantwort-Beispiel (400)

{
  "error": "Invalid parameters: either 'city' or ('lat' and 'lon') must be provided."
}

4. Ratenbegrenzung (Rate Limiting)
Plan	Limit
Free Tier	60 Requests / Minute
Pro Tier	600 Requests / Minute

Der Header X-RateLimit-Remaining informiert über das verbleibende Kontingent.
5. Versionshinweise
Version 1.0

    Veröffentlichung der Basis-Endpunkte

    aktuelle Wetterdaten

    5-Tage-Vorhersage

    Fehlercodes

    Authentifizierung über API-Key

6. Beispiele für verschiedene Sprachen
cURL

curl -X GET "https://api.simpleweather.example/v1/weather/current?city=Hamburg" \
     -H "Authorization: Bearer YOUR_API_KEY"

JavaScript (fetch)

fetch("https://api.simpleweather.example/v1/weather/current?city=Hamburg", {
  headers: { "Authorization": "Bearer YOUR_API_KEY" }
})
  .then(res => res.json())
  .then(data => console.log(data));

Schlussbemerkung

Diese API-Dokumentation dient als strukturiertes Beispiel und deckt typische Anforderungen an moderne REST-APIs ab.
Sie fokussiert auf Verständlichkeit, klare Parameterdefinitionen und direkt einsetzbare Beispiele.


---

Wenn du bereit bist, geht’s mit **Nummer 3: Release Notes (v1.2) — kompakt, professionell, realistisch** weiter.  
Einfach kurz „weiter“.
