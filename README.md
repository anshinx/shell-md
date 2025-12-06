# Shell Eco-Marathon BLDC Motor Sürücü Kartı (Shell-MD)

Bu depo, **Shell Eco-Marathon** araçları için özel olarak tasarlanmış, STM32 tabanlı, yüksek performanslı 3-Faz BLDC motor sürücü kartının **KiCad** donanım tasarım dosyalarını içerir.

Proje, **Mitsuba M2096D** gibi yüksek verimli motorları sürmek ve araç telemetrisini yönetmek amacıyla geliştirilmiştir.

## 🚀 Öne Çıkan Özellikler

* **Güçlü İşlemci:** ARM Cortex-M3 tabanlı **STM32F205VGT6** (120MHz, 1MB Flash).
* **Yüksek Akım Kapasitesi:** Faz başına 4 adet paralel MOSFET (**4+4+4 Topolojisi**) ile düşük $R_{DS(on)}$ ve minimum ısınma.
* **Sağlam Gate Sürüşü:** **IR2110** High/Low Side sürücüler ve her MOSFET için ayrılmış Gate dirençleri ile parazitik osilasyon koruması.
* **Gelişmiş İletişim:**
    * **CAN Bus:** Araç içi haberleşme için izoleli **TJA1051** arayüzü.
    * **Bluetooth:** Telemetri ve mobil ayar için **HM-10** (BLE) desteği.
    * **USB Type-C:** Veri günlüğü ve konfigürasyon için USB 2.0 arayüzü.
* **Sensör Arayüzleri:** Hall Sensörleri (Gürültü filtreli), Gaz Pedalı (Potansiyometre), Fren ve Hız Sabitleme (Cruise) girişleri.

## 🛠 Donanım Özellikleri (Hardware Specs)

| Bileşen | Model / Değer | Açıklama |
| :--- | :--- | :--- |
| **MCU** | STM32F205VGT6 | Ana kontrolcü. |
| **MOSFET** | IXTP90N15T | 150V, 90A, TO-220 (Faz başına 4x High, 4x Low). |
| **Gate Driver** | IR2110 | 2A High/Low Side Driver. |
| **CAN Transceiver** | TJA1051 | 5V beslemeli, yüksek hızlı CAN PHY. |
| **Bluetooth** | HM-10 / JDY-08 | UART üzerinden BLE haberleşmesi. |
| **USB** | Type-C (16-Pin) | CC dirençli, Device modunda çalışır. |
| **Besleme** | 12V & 3.3V | Harici regülatör girişi gerektirir. |

## 🔌 Pinout ve Bağlantılar

Kart üzerindeki kritik konnektör ve pin bağlantıları şöyledir:

### Motor & Güç
* **DC Bus:** 16S Batarya (~67V) girişi.
* **Faz Çıkışları:** Phase A, Phase B, Phase C (Vidalı Klemens).
* **Hall Sensörleri:** 5 Pin (5V, GND, H1, H2, H3) - RC Filtreli.

### Kontrol Arayüzleri
* **Gaz Pedalı:** Analog Giriş (0-3.3V) - `PA2`
* **Rejeneratif Fren:** Analog Giriş - `PA4`
* **Fren Anahtarı:** Dijital Giriş (Active Low) - `PE5`
* **Cruise Control:** Dijital Giriş (Active Low) - `PE6`

### Haberleşme
* **SWD:** Programlama ve Debug (`3V3`, `GND`, `SWDIO`, `SWCLK`, `NRST`).
* **CAN Bus:** Sonlandırma direnci (120Ω) jumper ile seçilebilir.
* **UART (Bluetooth):** `PC10` (TX) ve `PC11` (RX).

## ⚠️ Güvenlik ve Montaj Uyarıları

1.  **VCAP Kapasitörleri:** STM32'nin stabil çalışması için VCAP pinlerindeki (Pin 49, 73) 2.2µF kapasitörler işlemciye çok yakın monte edilmelidir.
2.  **Voltaj Sırası:** Sisteme enerji verirken önce **3.3V (Lojik)**, ardından **12V (Gate)** ve en son **Yüksek Voltaj (Batarya)** verilmesi önerilir.
3.  **USB Bağlantısı:** USB Type-C portu üzerinden işlemciye kod atılabilir ancak **VBUS** hattının harici 5V kaynağı ile çakışmamasına dikkat edilmelidir.
4.  **Soğutma:** MOSFET'ler paralel yapıda olsa da, yüksek akımlarda (kalkış anı) pasif soğutucu blok kullanılması tavsiye edilir.

## 📂 Depo Yapısı

* `/schematic`: KiCad şematik (.kicad_sch) dosyaları.
* `/pcb`: PCB tasarım (.kicad_pcb) dosyaları.
* `/library`: Projeye özel sembol ve kılıf kütüphaneleri.
* `/docs`: Datasheetler ve ek dokümantasyon.

## 🤝 Katkıda Bulunma

Hatalı bir bağlantı fark ederseniz veya iyileştirme öneriniz varsa lütfen bir **Issue** açın veya **Pull Request** gönderin.

---
Anshinx 
