## Numbers
ข้อมูลชนิดตัวเลข มีพื้นฐานคล้ายกับจาวา แต่จะมีความแตกต่างในบ้างอย่างเช่น 
* implicit widening conversions
* literals are slightly different in some cases
Type  | Bit Width
------ | --------
Double | 64
Float  | 32 
Long   | 64 
Int    | 32 
Short  | 16 
Byte   | 8 
## Literal Constants
Type  | Example
------ | --------
Decimals | 123
Longs  | 123L
Hexadecimals | 0x0F
Binaries | 0b00001011
Octal  | Not support
Doubles  | 123.5, 123.5e10
Floats  | 123.5f
## Underscores in numeric literals (since 1.1)
อ่านโค๊ดให้ง่ายขึ้นด้วย _
```kotlin
val oneMillion = 1_000_000
val creditCardNumber = 1234_5678_9012_3456L
val socialSecurityNumber = 999_99_9999L
val hexBytes = 0xFF_EC_DE_5E
val bytes = 0b11010010_01101001_10010100_10010010
```
## Representation
Int? สามารถเป็นได้ ข้อมูลตัวเลข และ null ดังนั้น
```kotlin
val a: Int = 10000
println(a === a) // Prints 'true'
val boxedA: Int? = a
val anotherBoxedA: Int? = a
println(boxedA === anotherBoxedA) // !!!Prints 'false'!!!
```
หรือ
```kotlin
val a: Int = 10000
println(a == a) // Prints 'true'
val boxedA: Int? = a
val anotherBoxedA: Int? = a
println(boxedA == anotherBoxedA) // Prints 'true'
```
## Explicit Conversions
กฏคือชนิดข้อมูลที่เล็กว่าไม่ได้อยู่ในชนิดข้อมูลใหญ่กว่า พูดอีกอย่างทุกชนิดข้อมูลเป็นอิสระไม่ได้เป็นส่วนหนึงของอีกชนิดข้อมูล
```kotlin
// Hypothetical code, does not actually compile:
val a: Int? = 1 // A boxed Int (java.lang.Integer)
val b: Long? = a // implicit conversion yields a boxed Long (java.lang.Long)
print(b == a) // Surprise! This prints "false" as Long's equals() checks whether the other is Long as well
```
ข้อมูลไม่สามารถทำ implicitly converted ไปยังชนิดข้อมูลที่ใหญ่กว่า
*implicitly converted คือกลไกที่คอมไพเลอร์ช่วยแปลงข้อมูล 
*explicit conversions คือคอมไพเลอร์ไม่มีการช่วยแปลงข้อมูลอยากได้ต้องทำเอง
```kotlin
val b: Byte = 1 // OK, literals are checked statically
val i: Int = b // ERROR
```
การทำ explicit conversions
```kotlin
val i: Int = b.toInt() // OK: explicitly widened
print(i)
```
ข้อมูลตัวเลขมีฟังก์ชันช่วยในการแปลงค่าข้อมูล
Function    | Type
----------- | --------
toByte()    | Byte
toShort()   | Short
toInt()     | Int
toLong()    | Long
toFloat()   | Float
toDouble()  | Double
toChar()    | Char
ข้อยกเว้น implicit conversions อัตโนมัติ
*การประเมินชนิดตัวแปรจากบริบทต่าง กรณีที่ไม่ได้กำหนดชนิดข้อมูลที่ชัดเจน
*ดำเนินการทางคณิตศาสตร์ (arithmetical operations)
```kotlin
val l = 1L + 3 // Long + Int => Long
```
## Operations
```kotlin
val x = (1 shl 2) and 0x000FF000
```
เฉพาะ Int และ Long
Operator     | Description
---------    | --------
shl(bits)    | signed shift left (Java's <<)
shr(bits)    | signed shift right (Java's >>)
ushr(bits)   | unsigned shift right (Java's >>>)
and(bits)    | bitwise and
or(bits)     | bitwise or
xor(bits)    | bitwise xor
inv()        | bitwise inversion