# Street Light IoT Prototype 💡🌙

[![Stack](https://img.shields.io/badge/Stack-PHP%20%7C%20ESP32%2FESP8266%20%7C%20CanvasJS-blue)](#)
[![Transport](https://img.shields.io/badge/Transport-HTTP%20%7C%20Query%20Params-green)](#)
[![Server](https://img.shields.io/badge/Server-Apache%20%7C%20XAMPP-orange)](#)
[![License: MIT](https://img.shields.io/badge/License-MIT-success.svg)](LICENSE)

A small IoT system that **records LDR readings** and (optionally) **controls a relay**.  
Frontend uses **CanvasJS** for charts; backend is a set of **PHP** endpoints. A tiny **Python** script can simulate the device.

---

## ✨ Features
- 🌗 Record brightness (`lux`) with optional relay `state` (`ON`/`OFF`)
- 📈 View latest value and historical log as charts/tables
- 🔌 Simple HTTP GET endpoints (easy from ESP32/ESP8266 or any client)
- 🖥️ Drop-in XAMPP/WAMP/LAMP hosting

---

## 🗂 Project Structure (from repo)
canvasjs3.6/ # CanvasJS charting library (frontend)
vendor/ # (optional) PHP deps (ignored by .gitignore)

_index.html # Main dashboard page (loads CanvasJS / shows charts)
_graph.php # Server-side chart/data view (reads log)
_view_log.php # Tabular view of the historical log
_displaytemp.php # Latest reading / small status endpoint
_recordtemp.php # Ingest endpoint: ?lux=123&state=ON

_convertXMLtoJSON.php # Utility: transforms XML log to JSON for charts
_log_data.php # Helper used by other scripts to append to log
_log.xml # Example/live log file (XML) ← usually git-ignored
_tempData_example.xml # Example XML format (sample data)
_info.php # phpinfo/diagnostics (dev only)
_php-ml-test.php # (experimental) ML test harness (dev only)
_streetlight.py # Python test client to send readings


> File names with leading underscores are kept as-is to match the original assignment.

---

## 🏗 Architecture

```mermaid
flowchart LR
  subgraph Device["ESP32/ESP8266 or Script"]
    A["LDR sensor"] --> B["Client code"]
    B -->|HTTP GET ?lux=&state=| C["_recordtemp.php"]
  end

  subgraph Server["Apache + PHP"]
    C --> D[[" _log.xml "]]
    E["_log_data.php"] --> D
    F["_convertXMLtoJSON.php"] -. reads/writes .-> D
    G["_displaytemp.php"] --> D
    H["_view_log.php"] --> D
    I["_graph.php"] --> D
  end

  subgraph UI["Browser"]
    J["index.html (CanvasJS)"]
    J -->|AJAX| G
    J -->|AJAX| H
    J -->|AJAX| I
  end


▶️ Run locally (XAMPP on Windows)

Install XAMPP, start Apache.

Copy this folder to:

C:\xampp\htdocs\street-light-iot-prototype


Open in your browser:

Dashboard: http://localhost/street-light-iot-prototype/_index.html

Chart view: http://localhost/street-light-iot-prototype/_graph.php

Log table: http://localhost/street-light-iot-prototype/_view_log.php

Latest: http://localhost/street-light-iot-prototype/_displaytemp.php
Send a sample reading

Browser:

http://localhost/street-light-iot-prototype/_recordtemp.php?lux=123&state=ON


curl:

curl "http://localhost/street-light-iot-prototype/_recordtemp.php?lux=456&state=OFF"


Params

lux → numeric brightness (ADC-derived)

state → ON | OFF (optional)

🔌 Endpoints
| Endpoint                | Method | Query params                        | Purpose                           |
| ----------------------- | ------ | ----------------------------------- | --------------------------------- |
| `_recordtemp.php`       | GET    | `lux` (number), `state` (`ON/ OFF`) | Append a reading to `_log.xml`.   |
| `_displaytemp.php`      | GET    | –                                   | Show/return latest reading.       |
| `_view_log.php`         | GET    | `limit` (optional)                  | Render historical log.            |
| `_graph.php`            | GET    | –                                   | Chart view (reads the log).       |
| `_convertXMLtoJSON.php` | GET    | –                                   | Utility to produce JSON from XML. |
| `_log_data.php`         | GET    | internal                            | Helper used by other scripts.     |

🖼 Screenshots & 🎥 Demo

Add media later and they’ll render here automatically:


🔒 Security

Don’t commit secrets; prefer config.example.php → copy to config.local.php on server.

Lock down endpoints before exposing to the internet (auth/token, rate-limit, CORS).

Ignore logs & temp files in git.

🗺️ Roadmap

 JSON API for all views (easier JS charts)

 CSV export

 Basic auth/token

 Dockerfile (Apache+PHP)

 ESP32 sample firmware snippet

 🤝 Contributing

Issues/PRs welcome. Keep endpoints small and documented.
📄 License

MIT – see LICENSE
. CanvasJS remains © its authors (check their terms for redistribution).
