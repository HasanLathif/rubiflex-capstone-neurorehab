# RUBIflex: IoT Neurorehabilitation System for Brachial Plexus Injury

**Tags:** `Capstone`, `Web Bluetooth API`, `BLE`, `Seeed XIAO ESP32-C3`, `JavaScript`, `Medical Device`

> **Status: [Complete]** A fully functional FES-based rehabilitation system featuring a low-latency, browser-based control interface via Web Bluetooth.

---

![Project Image](https://placehold.co/800x400/99f6e4/115e59?text=RUBIflex+Final+Prototype)
*(Replace this with a photo of the final device or a screenshot of your Web Interface)*

## 1. The Problem

Brachial Plexus Injury (BPI) often leads to partial or total arm paralysis. Rehabilitation using Functional Electrical Stimulation (FES) is effective but often requires expensive, hospital-bound equipment. There is a need for an affordable, home-use device that is easy to control without complex infrastructure.

## 2. Our Solution

**RUBIflex** is a wearable neurorehabilitation device that delivers electrical stimulation to restore motor function. Unlike traditional IoT devices that rely on cloud servers (increasing latency), RUBIflex utilizes a **Local-First** architecture.

It features a **Web-Based Interface** (hosted on GitHub Pages) that communicates *directly* with the hardware using the **Web Bluetooth API**. This eliminates the need for internet connectivity during therapy, ensuring instant response times and higher safety standards.

## 3. Technical Architecture & Implementation

The wireless control system integrates **Bluetooth Low Energy (BLE)** technology with a web interface. The architectural decisions prioritize low latency, which is critical for neural stimulation applications where device response must be instantaneous.

### 3.1. Web-Based Interface (GitHub Pages)
* **Hosting:** GitHub Pages serves the static HTML, CSS, and JavaScript files.
* **Accessibility:** Users access a simple web link; the browser downloads the interface assets locally. No app installation is required, increasing accessibility for patients and clinicians.
* **Logic:** Once loaded, client-side JavaScript initiates a scan for the BLE device using the **Web Bluetooth API**.

### 3.2. Hardware Control (Seeed XIAO ESP32-C3)
* **Role:** The microcontroller acts as a **BLE Peripheral** (GATT Server).
* **Service Structure:** Communication is defined by unique **Service UUIDs** and **Characteristic UUIDs** to separate control paths from sensor data paths.
* **Control Flow:**
    * **User Input:** When a user adjusts an amplitude slider on the web interface, JavaScript transmits binary data packets directly to the relevant characteristic on the ESP32-C3 via `writeValue()`.
    * **Feedback Loop:** Kinetic data from flex sensors is sent back to the web interface via **BLE Notifications**, enabling real-time graphical monitoring.

### 3.3. Why Web Bluetooth?
* **Low Latency:** Point-to-point communication eliminates the variable latency of internet routing.
* **Power Efficiency:** BLE consumes significantly less power than Wi-Fi, which is essential for a LiPo-battery-powered wearable.
* **Reliability:** Direct communication minimizes connection failures caused by internet interference, as long as the device remains within Bluetooth range.

## 4. My Role & Key Contributions

I served as the **Lead Electrical & Software Engineer (PIC)** for this project.

* **System Architecture:** Designed the direct browser-to-hardware communication flow, bypassing traditional backend brokers to reduce latency.
* **Firmware Engineering:** Programmed the Seeed XIAO ESP32-C3 to parse binary BLE packets and generate precise PWM signals for the H-Bridge driver (`TB6612FNG`).
* **Web Development:** Built the responsive dashboard that handles BLE pairing, service discovery, and real-time data visualization using pure JavaScript.
* **Fabrication:** Managed the integration of the high-voltage boost converter and safety isolation circuits onto the final PCB.

## 5. Technology Stack

* **Microcontroller:** `Seeed XIAO ESP32-C3`
* **Driver:** `TB6612FNG` (Motor Driver used for Biphasic Pulse Generation)
* **Connectivity:** `Web Bluetooth API` (BLE)
* **Frontend:** `JavaScript`, `HTML5`, `CSS3`, `GitHub Pages`
* **Design Tools:** `KiCad` (PCB), `Fusion360` (Enclosure)

## 6. Proof & Key Results
* **[Live Dashboard]:** Access the control dashboard here (requires a BLE-enabled browser like Chrome):
    * **[RUBIflex Web Controller](https://hasanlathif.github.io/fes-remote/)**

## 7. Project Status

**Status: [Complete]**
*This project was successfully completed, demonstrated, and passed the Final Semester Exam (UAS) for the Biomedical Engineering Capstone Design course.*
