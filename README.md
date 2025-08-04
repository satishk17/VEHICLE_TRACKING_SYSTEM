# 🚗 Vehicle Tracking System (VTS) with ESP32-S3 + EC200U-CN + L89 GNSS + MPU6050 + ThingsBoard
A real-time, FreeRTOS-based Vehicle Tracking System (VTS) that integrates:

🛰️ Quectel L89 GNSS module for precise GPS location
📈 MPU6050 for 6-axis motion sensing (accelerometer + gyroscope)
📡 Quectel EC200U-CN LTE module for HTTP cloud communication
🔁 FreeRTOS tasks with mutex-protected data access
☁️ Cloud connectivity to ThingsBoard IoT platform

# ✅ Features
📍 Real-time location via GNSS (latitude, longitude, altitude, speed, heading, satellites)
📐 Motion data (acceleration, rotation) from MPU6050
🌡️ Onboard temperature from MPU6050 sensor
🔒 FreeRTOS-based task architecture with shared data protection
📶 LTE signal strength, ICCID, and IMEI extraction
☁️ Periodic telemetry upload to ThingsBoard via HTTP JSON
🔁 GNSS/LTE conflict avoidance using task suspension

# 🧩 Hardware Requirements
Component	Description
ESP32-S3	Dual-core MCU with FreeRTOS support
EC200U-CN	Quectel LTE Cat-1 Module (UART-based)
L89 GNSS	Quectel GNSS Module (UART-based)
MPU6050	6-axis Accelerometer + Gyroscope (I2C)
(Optional)	CAN/OBD-II interface for vehicle data

# 📐 Wiring Summary
Peripheral	ESP32 GPIOs
MPU6050 (I2C)	SDA = GPIO8, SCL = GPIO9
GNSS (UART1)	RX = GPIO38, TX = GPIO39
LTE (UART2)	RX = GPIO40, TX = GPIO41
LTE PWR_EN	GPIO2
LTE RESET	GPIO1

# 🔄 Data Format (JSON)
json
Copy
Edit
{
  "accel_x_g": 0.01,
  "accel_y_g": -0.02,
  "accel_z_g": 1.01,
  "gyro_x_dps": 0.15,
  "gyro_y_dps": -0.07,
  "gyro_z_dps": 0.12,
  "temperature_C": 27.36,
  "latitude": 12.971599,
  "longitude": 77.594566,
  "altitude_m": 918.23,
  "speed_kmph": 34.51,
  "course_deg": 101.34,
  "satellites": 7,
  "hdop": 1,
  "date": "2025-08-04",
  "time": "11:23:45",
  "imei": "869XXXXXXXXXXXX",
  "sim_iccid": "8991XXXXXXXXXXXXXXX",
  "signal_strength": "87%"
}
☁️ Cloud: ThingsBoard Setup
Go to https://thingsboard.cloud (or your hosted instance).

Create a new device (e.g., vehicle-tracker-01).

Copy the Access Token from the device page.

Replace the token in the code:

cpp
Copy
Edit
const char* TOKEN = "your_device_access_token";
Data will be sent to:

bash
Copy
Edit
http://thingsboard.cloud/api/v1/YOUR_TOKEN/telemetry
🧪 Example Serial Output
yaml
Copy
Edit
✅ MPU6050 connected.
📍 GNSS Full Data: lat=12.971598, lng=77.594566, alt=918.23
📈 Accel: X=0.02g Y=0.01g Z=0.99g
📉 Gyro: X=0.12°/s Y=0.03°/s Z=0.10°/s
🌡️ Temp: 27.45°C
📶 Signal: 85%
🌐 Sending JSON:
{...}
✅ DATA Sent Successfully
📁 Folder Structure
bash
Copy
Edit
/vehicle-tracker/
├── main.ino            # Main firmware (FreeRTOS-based)
├── README.md           # Project overview
├── hardware/           # Schematics, datasheets (optional)
└── extras/             # Optional OBD or CAN docs

# 🔮 Future Improvements
⚙️ Add OBD-II vehicle speed, fuel data via CAN/UART
📦 Store data offline and upload later if LTE fails
🔋 Add deep sleep and wake triggers for power saving
🗺️ Dashboard for map + telemetry + movement graphs

# 👨‍💻 Author
SATISH KATTI
Embedded Systems & IoT Developer
GitHub | LinkedIn
