# CISCO-AP-Auth-web
1. enable secret cisco123
คืออะไร: ตั้งรหัสผ่านสำหรับเข้าสู่โหมด Privileged EXEC (enable mode)
ทำอะไร: เมื่อใช้คำสั่ง enable จะต้องใส่รหัสนี้เพื่อเข้าถึงการตั้งค่าขั้นสูง
ทำไมต้องใช้: เพื่อความปลอดภัย ไม่ให้ใครที่ไม่ได้รับอนุญาตแก้ไขค่าอุปกรณ์ได้

2. ip http server
คืออะไร: เปิดการใช้งาน HTTP server บนอุปกรณ์
ทำอะไร: ทำให้เราเข้าอุปกรณ์ผ่านเว็บเบราว์เซอร์ได้
ทำไมต้องใช้: สะดวกสำหรับการจัดการอุปกรณ์ผ่าน GUI

3. aaa new-model
คืออะไร: เปิดใช้งาน AAA (Authentication, Authorization, Accounting)
ทำอะไร: กำหนดระบบการยืนยันตัวตน, อนุญาต, และบันทึกกิจกรรมผู้ใช้
ทำไมต้องใช้: เพื่อความปลอดภัยและควบคุมสิทธิ์ผู้ใช้อย่างเป็นระบบ

4. aaa authentication login default local
คืออะไร: กำหนดวิธีการตรวจสอบผู้ใช้สำหรับ login
ทำอะไร: ใช้บัญชีผู้ใช้ที่สร้างไว้ในอุปกรณ์ (local) เพื่อ login
ทำไมต้องใช้: ถ้าไม่กำหนด ผู้ใช้จะไม่สามารถ login ได้

5. aaa authorization network default local
คืออะไร: กำหนดวิธีอนุญาตการเข้าเครือข่าย
ทำอะไร: ตรวจสอบสิทธิ์ผู้ใช้จากบัญชี local ก่อนให้ใช้งานเครือข่าย
ทำไมต้องใช้: ป้องกันผู้ไม่หวังดีเข้ามาใช้งานเครือข่าย

6. dot11 guest
คืออะไร: สร้างบัญชีผู้ใช้สำหรับ Guest Wireless
ทำอะไร: สร้าง username/password ให้ Guest ใช้เชื่อมต่อ Wi-Fi
ทำไมต้องใช้: เพื่อแยก Guest กับผู้ใช้งานภายใน

7. username LAB01 password 1234
คืออะไร: กำหนดบัญชีผู้ใช้ชื่อ LAB01 และรหัส 1234
ทำอะไร: รหัสผ่านไม่มีวันหมดอายุ
ทำไมต้องใช้: ให้ Guest ใช้งานง่ายโดยไม่ต้องเปลี่ยนรหัส

8. ip admission name web_auth proxy http
คืออะไร: สร้างนโยบาย Web Authentication
ทำอะไร: ให้ผู้ใช้ต้องผ่านหน้าเว็บ login ก่อนใช้เน็ต
ทำไมต้องใช้: ป้องกันคนแปลกหน้าใช้ Wi-Fi ฟรีโดยไม่อนุญาต

9. ip admission name web_auth method-list authentication default
คืออะไร: กำหนดให้ใช้วิธี authentication ที่เราสร้างไว้ (default)
ทำอะไร: บอกอุปกรณ์ว่าการ login ต้องใช้บัญชีผู้ใช้ที่สร้างไว้
ทำไมต้องใช้: เพื่อให้การยืนยันตัวตนถูกต้อง

10. dot11 ssid Guest
คืออะไร: สร้างชื่อ SSID ของ Wi-Fi
ทำอะไร: ตั้งชื่อเครือข่ายไร้สายเป็น "Guest"
ทำไมต้องใช้: เพื่อแยก Guest Network ออกจาก Network ภายใน

11.
authentication open
web-auth
guest-mode
คืออะไร: เป็นการตั้งค่า SSID
ทำอะไร:
  authentication open → ไม่ต้องใส่รหัสผ่านก่อนหน้าเว็บ login
  web-auth → ต้อง login ผ่านหน้าเว็บ
  guest-mode → SSID แสดงให้ทุกคนเห็น
ทำไมต้องใช้: ให้ Guest เชื่อมต่อง่าย และต้องยืนยันตัวตนก่อนใช้เน็ต

12. interface dot11radio 0
คืออะไร: เข้าไปตั้งค่า Interface Wireless Radio
ทำอะไร: กำหนดการเชื่อมต่อ Wi-Fi
ทำไมต้องใช้: ต้องเชื่อม SSID กับ Radio จริงถึงจะใช้งานได้

13.
ssid Guest
ip admission web_auth
no shutdown
คืออะไร: ตั้งค่า interface Wireless
ทำอะไร:
  เชื่อม SSID Guest
  ใช้ Web Authentication
  เปิดใช้งาน interface (no shutdown)
ทำไมต้องใช้: ถ้าไม่เปิด (shutdown) Wi-Fi จะไม่ทำงาน

14. interface BVI1
คืออะไร: เข้าสู่ Bridge Virtual Interface (BVI)
ทำอะไร: ใช้สำหรับให้ VLAN หรือ SSID มี IP Address
ทำไมต้องใช้: ต้องมี IP เพื่อให้ Guest เชื่อมต่อและออกเน็ตได้

15.
ip address 192.168.10.10 255.255.255.0
no shutdown
คืออะไร: ตั้งค่า IP ให้ BVI
ทำอะไร: อุปกรณ์มี IP ในเครือข่าย 192.168.10.0/24
ทำไมต้องใช้: เพื่อให้สามารถสื่อสารกับเครือข่ายอื่นได้

16. username LAB01 password 1234
คืออะไร: สร้างบัญชีผู้ใช้ Local สำหรับผู้ใช้ปกติ
ทำอะไร: ใช้สำหรับ login เข้าระบบ
ทำไมต้องใช้: ต้องมี user สำหรับ AAA authentication
