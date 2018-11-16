## Packages
ควรอยู่บนสุดของไฟล์

```kotlin
package io.kotlin

import java.util.*
```
## Functions
ฟังก์ชันควรประกอบ ค่าพารามิเตอร์ (Parameters) และ ค่ารีเทิร์น (Return Type)
```kotlin
fun sum(a: Int, b: Int): Int {
    return a + b
}
```
ค่ารีเทิร์น (Return Type) อาจจะไม่มีการประกาศตั้งแต่ตอนต้น แต่คอมไพเลอร์จะกำหนดค่าให้ตอนคอมไพล์อยู่ดี ประเมินจากชนิดข้อมูลในฟังก์ชั่นที่เป็น 
เอ็กเพรสชัน (Expression) สุดท้าย เช่น a + b เป็น Int ดังนั้นเมื่อ a, b ผ่านตัวดำเนินการ (Operator)ใดๆ ควรได้ค่า Int ค่ารีเทิร์น (Return Type) จึงเป็นค่า Int
```kotlin
fun sum(a: Int, b: Int) = a + b
```
Unit == Void คือกำหนดฟังก์ชันไม่การ ค่ารีเทิร์น (return type) กลับมา
```kotlin
fun printSum(a: Int, b: Int): Unit {
    println("sum of $a and $b is ${a + b}")
}
```
Unit อาจจะไม่มีการประกาศตั้งแต่ตอนต้น แต่คอมไพเลอร์จะกำหนดค่าให้ตอนคอมไพล์อยู่ดี ประเมินจากชนิดข้อมูลในฟังก์ชั่นที่เป็น 
เอ็กเพรสชัน (Expression) สุดท้าย
```kotlin
fun printSum(a: Int, b: Int) {
    println("sum of $a and $b is ${a + b}")
}
```

## Variables
val ตัวแปรที่อ่านอย่างเดียว (Read Only)
```kotlin
val a: Int = 1  // immediate assignment
val b = 2   // `Int` type is inferred
val c: Int  // Type required when no initializer is provided
c = 3       // deferred assignment
```
var ตัวแปรที่สามารถเปลี่ยนแปลงสถานะ (Mutable)
```kotlin
var x = 5 // `Int` type is inferred
x += 1
```
กำหนดตัวแปรบนสุด
```kotlin
val PI = 3.14
var x = 0

fun incrementX() { 
    x += 1 
}
```
