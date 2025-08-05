# SISTEM PALANG KERETA API OTOMATIS BERBASIS ARDUINO

## Pendahuluan

Proyek ini merupakan pengembangan sistem palang pintu kereta api otomatis yang dirancang untuk meningkatkan keamanan di perlintasan sebidang.  Latar belakang dari proyek ini adalah banyaknya kecelakaan yang terjadi di perlintasan kereta api akibat kurangnya prasarana palang pintu atau kelalaian petugas[cite: 26].  Sistem ini memanfaatkan beberapa sensor untuk mendeteksi kedatangan kereta dan secara otomatis mengaktifkan palang pintu, alarm, dan lampu peringatan[cite: 27, 52, 53].

## Tujuan Proyek

 Tujuan dari penelitian dan pengembangan ini adalah untuk menciptakan sistem palang pintu kereta api yang sepenuhnya otomatis[cite: 34].  Proyek ini diharapkan dapat mencegah pengendara menerobos palang pintu, sehingga dapat mengurangi angka kecelakaan[cite: 35].  Selain itu, sistem ini dirancang agar bekerja secara teratur, meningkatkan efektivitas operasional palang pintu kereta api[cite: 36].

## Metode Pelaksanaan

 Metode yang digunakan dalam proyek ini adalah pendekatan penelitian pengembangan (Research and Development) model Borg and Gall[cite: 39, 40]. Tahapan pelaksanaannya mencakup:
1.   **Analisis Kebutuhan**: Dilakukan survei dan diskusi dengan pihak PT KAI serta petugas penjaga palang pintu untuk menentukan kebutuhan sistem[cite: 52].
2.  **Perancangan Alat**: Perancangan hardware dan software sistem.
3.  **Pembuatan Alat**: Merakit komponen-komponen yang diperlukan.
4.  **Uji Alat**: Melakukan pengujian sistem yang telah dibuat.
5.   **Implementasi**: Menerapkan sistem dan membuat rekomendasi untuk PT KAI[cite: 48, 49].

## Komponen yang Digunakan

Berikut adalah komponen-komponen dasar yang digunakan dalam sistem ini:
*  **Arduino Uno**: Mikrokontroler utama yang mengontrol seluruh sistem[cite: 55].
*  **Servo Motor**: Digunakan untuk menggerakkan palang pintu[cite: 61, 63].
*  **Sensor Ultrasonik**: Berfungsi untuk mendeteksi jarak dan keberadaan kereta api yang melintas[cite: 83, 84].
*  **LED**: Digunakan sebagai lampu indikator peringatan[cite: 74].
*  **Buzzer**: Berfungsi sebagai alarm atau pemberi peringatan suara[cite: 100].
*  **NodeMCU ESP8266**: Board elektronik dengan kemampuan mikrokontroler dan koneksi WiFi, memungkinkan aplikasi monitoring dan controlling[cite: 80].
*  **Sensor Getar**: Alat ukur untuk mengukur getaran pada benda, dapat digunakan untuk antisipasi jika terjadi hal yang tidak diinginkan[cite: 86].
*  **Kabel Jumper**: Digunakan sebagai konduktor untuk menghubungkan komponen-komponen tanpa solder[cite: 90, 91].
*  **PCB (Printed Circuit Board)**: Papan yang digunakan untuk menghubungkan komponen elektronika dengan lapisan jalur konduktor[cite: 94, 95].
*  **LCD (Liquid Crystal Display)**: Komponen yang berfungsi sebagai penampil karakter atau angka[cite: 67].

## Skematik Rangkaian

Sistem ini dirangkai menggunakan komponen-komponen utama seperti Arduino Uno, sensor ultrasonik, servo motor, dan LED. Berikut adalah gambaran skematik dasar rangkaian:

## Kode Program

Kode program berikut adalah implementasi dasar untuk mengontrol sistem palang pintu otomatis. Kode ini membaca data dari sensor ultrasonik dan menggerakkan servo motor serta buzzer berdasarkan jarak yang terdeteksi.

```cpp
#include <Servo.h>

Servo servo;
int angle = 10;
int buzz = 2;

// defines pins numbers
const int trigPin = 12;
const int echoPin = 11;

// defines variables
long duration;
int distance;

void setup() {
  servo.attach(8);
  servo.write(angle);
  pinMode(trigPin, OUTPUT); // Sets the trigPin as an Output
  pinMode(echoPin, INPUT);  // Sets the echoPin as an Input
  pinMode(buzz, OUTPUT);
  Serial.begin(9600); // Starts the serial communication
}

void loop() {
  // Clears the trigPin
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);

  // Sets the trigPin on HIGH state for 10 micro seconds
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  // Reads the echoPin, returns the sound wave travel time in microseconds
  duration = pulseIn(echoPin, HIGH);

  // Calculating the distance
  distance = duration * 0.034 / 2;

  // Prints the distance on the Serial Monitor
  Serial.print("Distance: ");
  Serial.println(distance);
  delay(100);

  if (distance < 8) {
    digitalWrite(buzz, HIGH);
    servo.write(180);
    delay(1000);
  } else {
    digitalWrite(buzz, LOW);
    servo.write(70);
  }
}
