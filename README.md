# gesture-control


### **2. Linh kiện cần thiết**

* **Arduino Uno/Nano** (Ưu tiên Nano nếu muốn làm thiết bị đeo tay).
* **Cảm biến siêu âm HC-SR04** (2 cái) hoặc **Cảm biến cử chỉ APDS-9960**.
* **Dây nhảy (Jumper wires)** và **Breadboard**.

---

### **3. Nguyên lý hoạt động**

1. **Arduino:** Đo khoảng cách từ tay bạn đến 2 cảm biến siêu âm.
* Nếu tay trái che: Thực hiện hành động A (ví dụ: Next bài hát).
* Nếu tay phải che: Thực hiện hành động B (ví dụ: Back bài hát).
* Nếu cả 2 tay cùng đưa lại gần: Tăng/giảm âm lượng.


2. **Python:** Chạy một script trên máy tính để đọc dữ liệu từ cổng Serial và giả lập các phím bấm tương ứng (sử dụng thư viện `pyautogui`).



Code



```cpp
long duration;
int distance;

int getDistance(int trigPin, int echoPin) {
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  duration = pulseIn(echoPin, HIGH);
  distance = duration * 0.034 / 2;
  return distance;
}

void loop() {
  int distL = getDistance(trigL, echoL);
  int distR = getDistance(trigR, echoR);
  
  if (distL < 10 && distR < 10) {
    Serial.println("BOTH");
  } else if (distL < 10) {
    Serial.println("LEFT");
  } else if (distR < 10) {
    Serial.println("RIGHT");
  }
  delay(200); // Tránh gửi dữ liệu quá nhanh gây treo Serial
}

```

ơn – đúng chất dân Tự động hóa).

Bạn có muốn mình viết chi tiết đoạn code **Python** để nhận tín hiệu từ Arduino không?
