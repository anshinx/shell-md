 ##Pinout Tablosu (Full Liste)

| Kategori            | Fonksiyon             | Pin     | Perifer         | PCB / Notlar                        |
| :------------------ | :-------------------- | :------ | :-------------- | :---------------------------------- |
| **PWM (Power)**     | **HS MOSFET A**       | `PE9`   | TIM1_CH1        | "Port E (Layout Kolaylığı)"         |
|                     | **HS MOSFET B**       | `PE11`  | TIM1_CH2        | "                                   |
|                     | **HS MOSFET C**       | `PE13`  | TIM1_CH3        | "                                   |
|                     | **LS MOSFET A**       | `PE8`   | TIM1_CH1N       | "                                   |
|                     | **LS MOSFET B**       | `PE10`  | TIM1_CH2N       | "                                   |
|                     | **LS MOSFET C**       | `PE12`  | TIM1_CH3N       | "                                   |
| **Güvenlik**        | **ACİL STOP (Kill)**  | `PB12`  | TIM1_BKIN       | **Donanımsal Koruma** (PWM'i Keser) |
| **Kontrol (Input)** | **FREN (Switch)**     | `PE2`   | GPIO_Input      | Mekanik fren algılama               |
|                     | **CRUISE (Buton)**    | `PE3`   | GPIO_Input      | Hız Sabitleme (Bas-Çek)             |
| **Analog (ADC)**    | **AKIM SENS.**        | `PA0`   | ADC1_IN0        | Sensör çıkışı (Max 3.3V)            |
|                     | **BATARYA V.**        | `PA1`   | ADC1_IN1        | Gerilim bölücü ile                  |
|                     | **GAZ / PEDAL**       | `PA2`   | ADC1_IN2        | Gaz kolu/pedalı                     |
|                     | **SICAKLIK**          | `PA3`   | ADC1_IN3        | NTC Okuma                           |
|                     | **REJEN (Pedal)**     | `PA4`   | ADC1_IN4        | **Analog Fren/Rejen Ayarı**         |
| **Arayüz (UI)**     | **I2C SCL (Ekran)**   | `PB6`   | I2C1_SCL        | **4.7k Pull-Up Gerekli**            |
|                     | **I2C SDA (Ekran)**   | `PB7`   | I2C1_SDA        | **4.7k Pull-Up Gerekli**            |
|                     | **BUZZER**            | `PE1`   | GPIO_Output     | Transistör ile sürülmeli            |
|                     | **STAT LED**          | `PE0`   | GPIO_Output     | Durum LED'i                         |
| **Haberleşme**      | **CAN RX**            | `PB8`   | CAN1_RX         | **Transceiver Gerekli (TJA1050)**   |
|                     | **CAN TX**            | `PB9`   | CAN1_TX         | **Transceiver Gerekli (TJA1050)**   |
|                     | **BT TX (Telemetri)** | `PB10`  | USART3_TX       | Bluetooth Modülü                    |
|                     | **BT RX (Telemetri)** | `PB11`  | USART3_RX       | Bluetooth Modülü                    |
| **USB**             | **USB VBUS**          | `PA9`   | USB_OTG_FS_VBUS | 5V Algılama (Direnç ile)            |
|                     | **USB ID**            | `PA10`  | USB_OTG_FS_ID   |                                     |
|                     | **USB DM (-)**        | `PA11`  | USB_OTG_FS_DM   | Diferansiyel Çift                   |
|                     | **USB DP (+)**        | `PA12`  | USB_OTG_FS_DP   | Diferansiyel Çift                   |
| **Hall Sensör**     | **HALL A**            | `PC6`   | TIM3_CH1        | Pull-Up + Filtre Devresi            |
|                     | **HALL B**            | `PC7`   | TIM3_CH2        | "                                   |
|                     | **HALL C**            | `PC8`   | TIM3_CH3        | "                                   |
| **Sistem**          | **SWDIO**             | `PA13`  | SYS_SWDIO       | Kod Yükleme                         |
|                     | **SWCLK**             | `PA14`  | SYS_SWCLK       | Kod Yükleme                         |
|                     | **OSC IN**            | `PH0`   | RCC_OSC_IN      | 8MHz Kristal                        |
|                     | **OSC OUT**           | `PH1`   | RCC_OSC_OUT     | 8MHz Kristal                        |
|                     | **NRST**              | `NRST`  | Reset           | Buton + 100nF                       |
|                     | **BOOT0**             | `BOOT0` | Boot            | Buton + 10k PD                      |


 **FET Topolojisi:** Half-Bridge (Yarım Köprü)

 ### Voltaj Regülasyonu (Power Tree)
Isınmayı yönetmek için kademeli düşüm uygulanmıştır:
1.  **67.2V ➡️ 12V:** `LM5017` (Buck Converter) - *Ana yük, Gate Driver beslemesi.*
2.  **12V ➡️ 5V:** `AP2204` (LDO) - *Sensörler, USB VBUS simülasyonu.*
3.  **5V ➡️ 3.3V:** `XC6206` (LDO) - *STM32 MCU, Bluetooth, Ekran.*

 Gate Driver (IR2110)
* **Bootstrap Diyotu:** `US1M` veya `ES1J` (Ultra Fast olmak zorunda).
* **Bootstrap Kapasitörü:** 1µF - 2.2µF (Low ESR Seramik).
* **Gate Dirençleri:** Simülasyon sonucuna göre 10Ω - 22Ω arası (Ringing'i önlemek için).

  
