# 🏷️ ESP32 RFID Attendance Logger

An IoT-based attendance logging system powered by an **ESP32**, an **RC522 RFID Reader**, and an **SH1106 / SSD1306 OLED Display**. This system scans RFID tags, checks NTP network time, toggles between Entry and Exit states, and logs attendance data directly to **Google Sheets** via Google Apps Script webhooks.

---

## ✨ Key Features

* **Real-time Clock (NTP):** Synchronizes exact current time and date over WiFi via NTP servers.
* **Smart Entry/Exit Toggle:** Automatically tracks whether a scanned card represents an **Entry** or **Exit** event.
* **OLED Visual Feedback:** Displays animated connection status, a live clock with blinking colons, scan animations, and user recognition feedback.
* **Cloud Integration (Google Sheets):** Sends log data via HTTP GET requests to a Google Apps Script web app endpoint.
* **Debounce Protection:** Ignores rapid duplicate scans within a configurable time threshold.
* **Auto-Reconnection:** Handles WiFi disconnections gracefully without crashing the main loop.

---

## 🛠️ Hardware Requirements

* ESP32 Development Board
* RC522 RFID Module (SPI interface)
* OLED Display (128x64 SSD1306 / SH1106, I2C interface)
* RFID Tags / Cards
* Jumper Wires & Breadboard

---

## 📌 Wiring Diagram

### 1. RC522 RFID Reader (SPI)
| RC522 Pin | ESP32 Pin |
| :--- | :--- |
| **SDA (SS)** | GPIO 21 |
| **RST** | GPIO 22 |
| **SCK** | GPIO 18 |
| **MOSI** | GPIO 23 |
| **MISO** | GPIO 19 |
| **GND** | GND |
| **3.3V** | 3.3V |

### 2. OLED Display (I2C)
| OLED Pin | ESP32 Pin |
| :--- | :--- |
| **SCL** | GPIO 5 |
| **SDA** | GPIO 4 |
| **GND** | GND |
| **VCC** | 3.3V / 5V |

---

## 🚀 Getting Started

### Step 1: Google Sheets Setup
1. Create a new Google Sheet.
2. Go to **Extensions > Apps Script**, paste the provided Google Apps Script code (`GOOGLE SHEET SCRIPT esp32.txt`), and save it.
3. Deploy the script as a **Web App** with access set to **"Anyone"**.
4. Copy the generated Web App URL and paste it into the `SHEET_URL` variable in your Arduino code.

### Step 2: Configure Firmware
1. Open the Arduino IDE and ensure you have installed the following libraries:
   * `MFRC522` by Miguel Balboa
   * `Adafruit_SSD1306` & `Adafruit_GFX`
2. Update your WiFi credentials (`WIFI_SSID` and `WIFI_PASSWORD`) in the code.
3. Add your authorized RFID card UIDs and names into the `uidToName` map:
   ```cpp
   std::map<String, String> uidToName = {
       {"YOUR_CARD_UID", "Your Name"}
   };
   ```

### Step 3: Upload and Run
* Connect your ESP32 via USB, select the correct board and port, and upload the code. Open the Serial Monitor at `115200` baud to watch logs and scan UIDs!

---

## 📜 License
This project is open-source under the [MIT License](LICENSE).
