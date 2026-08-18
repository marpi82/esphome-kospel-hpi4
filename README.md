# Kospel HPI-4 — ESPHome / Home Assistant Integration

Repozytorium zawiera gotową konfigurację **ESPHome** do integracji pompy ciepła do ciepłej wody użytkowej (CWU) **Kospel HPI-4** z systemem **Home Assistant** przy użyciu protokołu **Modbus RTU over RS485**.

---

## 🛠️ Wymagania sprzętowe

* **Pompa ciepła:** Kospel HPI-4
* **Płytka mikrokontrolera:** Waveshare ESP32-S3-RS485-CAN (SKU: 32154)
* **Połączenie magistrali:** RS485 (A, B, GND) do portu serwisowego / płyty głównej pompy

---

## 🔌 Domyślna konfiguracja wyprowadzeń (Pinout)

Dla płytki **Waveshare ESP32-S3-RS485-CAN**:

| Sygnał RS485 | Pin ESP32-S3 | Uwagi |
| :--- | :--- | :--- |
| **TX** | `GPIO17` | Nadawanie UART |
| **RX** | `GPIO18` | Odbiór UART |
| **DE/RE (Flow Control)** | `GPIO21` | Sterowanie kierunkiem RS485 |

### Parametry Modbus RTU
* **Baud rate:** 9600
* **Data bits:** 8
* **Parity:** NONE
* **Stop bits:** 1
* **Adres urządzenia (Slave ID):** 88

---

## 📊 Odczytywane parametry i funkcje

* **Temperatury:** CWU (P01), powietrza zasysanego (P05), czynnika (przed/po sprężarce, parownik), wody (przed/po skraplaczu) oraz płyty sterującej.
* **Obliczenia (Templates):** $\Delta T$ wody, przegrzanie całkowite (Total Superheat), przegrzanie parownika.
* **Statusy pracy:** Sprężarka, wentylator, pompa wody CWU, stan zaworu 4-drogowego, faza pracy urządzenia oraz stany błędów.
* **Sterowanie:**
  * Zezwolenie na pracę (Enable switch)
  * Tryb "Zawsze aktywna" (Auto re-enable)
  * Nastawa temperatury docelowej CWU (N01: 20–55°C)
  * Nastawa minimalnej temperatury powietrza (N02: 5–15°C)

---

## 🚀 Instrukcja instalacji

1. Sklonuj to repozytorium do swojego folderu `esphome/` w Home Assistant.
2. Utwórz plik `secrets.yaml` na podstawie wzorca `secrets.yaml.example`:
   ```bash
   cp secrets.yaml.example secrets.yaml
