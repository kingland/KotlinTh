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
Unit == Void คือกำหนดฟังก์ชันไม่มี ค่ารีเทิร์น (Return Type)
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
## Comments
```kotlin
// This is an end-of-line comment

/* This is a block comment
   on multiple lines. */
```
## String Template
```kotlin
var a = 1
// simple name in template:
val s1 = "a is $a" 

a = 2
// arbitrary expression in template:
val s2 = "${s1.replace("is", "was")}, but now is $a"
```
## Condition Expressions
```kotlin
fun maxOf(a: Int, b: Int): Int {
    if (a > b) {
        return a
    } else {
        return b
    }
}
```

```kotlin
fun maxOf(a: Int, b: Int) = if (a > b) a else b
```
## Checking for null
กำหนด ค่ารีเทิร์น เป็น Int? เพื่อระบุว่า ค่ารีเทิร์น อามีค่าเป็น Int หรือ null
```kotlin
fun parseInt(str: String): Int? {
    // ...
}
```
ตรวจสอบค่า null โดยใช้ if ในการตรวจสอบ
```kotlin
fun printProduct(arg1: String, arg2: String) {
    val x = parseInt(arg1)
    val y = parseInt(arg2)

    // Using `x * y` yields error because they may hold nulls.
    if (x != null && y != null) {
        // x and y are automatically cast to non-nullable after null check
        println(x * y)
    }
    else {
        println("either '$arg1' or '$arg2' is not a number")
    }    
}
```
หรือ
```kotlin
// ...
if (x == null) {
    println("Wrong number format in arg1: '$arg1'")
    return
}
if (y == null) {
    println("Wrong number format in arg2: '$arg2'")
    return
}

// x and y are automatically cast to non-nullable after null check
println(x * y)
```
## Type checks and Automatic casts
คีย์เวิร์ด is ในการตรวจสอบชนิดข้อมูล ถ้าเป็นชนิดข้อมูลนั้นจริง จะทำการ cast ข้อมูลให้อัตโนมัติ
```kotlin
fun getStringLength(obj: Any): Int? {
    if (obj is String) {
        // `obj` is automatically cast to `String` in this branch
        return obj.length
    }

    // `obj` is still of type `Any` outside of the type-checked branch
    return null
}
```

```kotlin
fun getStringLength(obj: Any): Int? {
    if (obj !is String) return null

    // `obj` is automatically cast to `String` in this branch
    return obj.length
}
```

```kotlin
fun getStringLength(obj: Any): Int? {
    // `obj` is automatically cast to `String` on the right-hand side of `&&`
    if (obj is String && obj.length > 0) {
        return obj.length
    }

    return null
}
```
## Loop
คีย์เวิร์ด in ใช้ในวนลูปค่า Array, Collection คล้ายกับ JavaScript
```kotlin
val items = listOf("apple", "banana", "kiwifruit")
for (item in items) {
    println(item)
}
```
หรือ
```kotlin
val items = listOf("apple", "banana", "kiwifruit")
for (index in items.indices) {
    println("item at $index is ${items[index]}")
}
```
## While Loop
คีย์เวิร์ด while ใช้ในวนลูปค่า Array, Collection โดยกำหนดเงือนไขสิ้นสุดการทำงานลงใน while
```kotlin
val items = listOf("apple", "banana", "kiwifruit")
var index = 0
while (index < items.size) {
    println("item at $index is ${items[index]}")
    index++
}
```
## When Expression
คีย์เวิร์ด when ลักษณะใช้งานคล้ายกับ if..ifelse หรือ switch แต่มีความยืดหยุ่นมากกว่า 
```kotlin
fun describe(obj: Any): String =
    when (obj) {
        1          -> "One"
        "Hello"    -> "Greeting"
        is Long    -> "Long"
        !is String -> "Not a string"
        else       -> "Unknown"
    }
```

## Ranges
ตรวจสอบค่าในแรงค์โดยใช้ if
```kotlin
val x = 10
val y = 9
if (x in 1..y+1) {
    println("fits in range")
}
```
```kotlin
val list = listOf("a", "b", "c")

if (-1 !in 0..list.lastIndex) {
    println("-1 is out of range")
}
if (list.size !in list.indices) {
    println("list size is out of valid list indices range, too")
}
```
สามารถใช้ for ในการวนลูปค่าในแรงค์
```kotlin
for (x in 1..5) {
    print(x)
}
```

```kotlin
for (x in 1..10 step 2) {
    print(x)
}
println()
for (x in 9 downTo 0 step 3) {
    print(x)
}
```
## Collections
คีย์เวิร์ด in วนลูปข้อมูลในคอลเลคชัน
```kotlin
for (item in items) {
    println(item)
}
```
คีย์เวิร์ด when, in ตรวจสอบข้อมูลในคอลเลคชัน
```kotlin
when {
    "orange" in items -> println("juicy")
    "apple" in items -> println("apple is fine too")
}
```
การใช้งาน lambda ในคอลเลคชัน
```kotlin
val fruits = listOf("banana", "avocado", "apple", "kiwifruit")
fruits
  .filter { it.startsWith("a") }
  .sortedBy { it }
  .map { it.toUpperCase() }
  .forEach { println(it) }
```
## Creating instance
การสร้างออปเจคและอินสแตนซ์
```kotlin
val rectangle = Rectangle(5.0, 2.0) //no 'new' keyword required
val triangle = Triangle(3.0, 4.0, 5.0)
```
