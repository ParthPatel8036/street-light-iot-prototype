\# Street Light IoT Prototype 💡🌙



\[!\[Stack](https://img.shields.io/badge/Stack-PHP%20%7C%20ESP32%2FESP8266%20%7C%20CanvasJS-blue)](#)

\[!\[Comms](https://img.shields.io/badge/Comms-HTTP%20%7C%20JSON-green)](#)

\[!\[License: MIT](https://img.shields.io/badge/License-MIT-success.svg)](LICENSE)



A small IoT system that records/visualizes street-light sensor data (LDR) and controls a relay for the lamp.  

Frontend charts use \*\*CanvasJS\*\*; backend endpoints in \*\*PHP\*\*; optional helper in \*\*Python\*\*.



---



\## ✨ Features

\- 🌗 Auto/Manual light control (relay)

\- 📈 Log + visualize readings (CanvasJS)

\- 🔄 Simple HTTP endpoints to record/view

\- 🧰 Easy to host on XAMPP/WAMP/LAMP



---



\## 🗂 Project structure (high-level)



canvasjs3.6/ # charting library (frontend)

vendor/ # (optional) PHP deps via Composer (ignored)

\_index.html # dashboard / chart view

\_recordtemp.php # endpoint to record sensor values

\_view\_log.php # list / view logged data

\_displaytemp.php # display latest value

\_log\_data.php # helper to append to log

\_log.xml # (example log file; ignored by default)

\_streetlight.py # optional Python helper script





> Folder/file names may vary slightly; see the code for exact endpoints.



---



\## ▶️ Run locally (XAMPP on Windows)

1\. Install \*\*XAMPP\*\*, start \*\*Apache\*\*.

2\. Copy this project folder into:  

&nbsp;  `C:\\xampp\\htdocs\\street-light-iot-prototype`

3\. Visit:  

&nbsp;  - `http://localhost/street-light-iot-prototype/\_index.html` (dashboard)  

&nbsp;  - `http://localhost/street-light-iot-prototype/\_view\_log.php`  

&nbsp;  - `http://localhost/street-light-iot-prototype/\_displaytemp.php`



\- `lux` → LDR/brightness reading  

\- `state` → `ON`/`OFF` (relay state)



---



\## 🔒 Security

\- Don’t commit real secrets/keys.  

\- Use `config.example.php` → copy to `config.local.php` on your server.  

\- Lock down endpoints if exposed to the internet.



---



\## 📄 License

MIT – feel free to reuse with attribution.



