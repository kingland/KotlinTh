## Numbers
ข้อมูลชนิดตัวเลข มีพื้นฐานคล้ายกับจาวา แต่จะมีความแตกต่างในบ้างอย่างเช่น 
* implicit widening conversions
* literals are slightly different in some cases
### BitWidth
Type  | BitWidth
------ | --------
Double | 64
Float  | 32
Long | 64
Int | 32
Short  | 16
Byte  | 8
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
อ่านโค๊ดให้ง่ายขึ้นด้วย underscore (_) 
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
* implicitly converted คือกลไกที่คอมไพเลอร์ช่วยแปลงข้อมูล 
* explicit conversions คือคอมไพเลอร์ไม่มีการช่วยแปลงข้อมูลอยากได้ต้องทำเอง
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
## Conversion Functions
Function    | Type
----------- | --------
toByte()    | Byte
toShort()   | Short
toInt()     | Int
toLong()    | Long
toFloat()   | Float
toDouble()  | Double
toChar()    | Char
### Implicit conversions อัตโนมัติเมื่อ
* ต้องการประเมินชนิดตัวแปรจากบริบท กรณีที่ไม่ได้กำหนดชนิดข้อมูลที่ชัดเจน
* ดำเนินการทางคณิตศาสตร์ (arithmetical operations) Long + Int จะได้ค่าข้อมูลใหญ่กว่า Long เป็นค่ารีเทิร์น
```kotlin
val l = 1L + 3 // Long + Int => Long
```
## Operations
โอเปอเรชันทางคณิตศาสตร์ บวกลบคูณหาร มีให้ใช้ปกติ แต่ที่เพิ่มมาสามารถประกาศฟังก์ชันให้เป็นโอเปอร์เรชันได้ เรียกใช้ในรูปแบบ infix
```kotlin
val x = (1 shl 2) and 0x000FF000
```
### Int and Long Operations
Operator     | Description
---------    | --------
shl(bits)    | signed shift left (Java's <<)
shr(bits)    | signed shift right (Java's >>)
ushr(bits)   | unsigned shift right (Java's >>>)
and(bits)    | bitwise and
or(bits)     | bitwise or
xor(bits)    | bitwise xor
inv()        | bitwise inversion
## Floating Point Comparison
* Equality - a == b และ a != b
* Comparison - a < b, a > b, a <= b, a >= b
* Range - a..b, x in a..b, x !in a..b
## Any, Comparable<...> 
ข้อมูลประเภทอื่นที่ไม่ใช่ Static Floating Point ใช้ `equals` และ `compareTo`
* NaN จะ `equal` ตัวเอง
* NaN is considered greater than any other element including `POSITIVE_INFINITY`
* -0.0 is considered less than 0.0
## Characters
ข้อมูลชนิด Char ไม่สามารถแทนด้วยข้อมูลชนิดตัวเลข Int, Byte มันคือข้อมูลคนละประเภท
```kotlin
fun check(c: Char) {
    if (c == 1) { // ERROR: incompatible types
        // ...
    }
}
```
* character literals - `'1'`
* escape - `\t, \b, \n, \r, \', \", \\  \$`
* unicode escape - `'\uFF00'`

```kotlin
//แปลงค่า Char เป็น Int โดยใช้  explicitly convert
fun decimalDigitValue(c: Char): Int {
    if (c !in '0'..'9')
        throw IllegalArgumentException("Out of range")
    return c.toInt() - '0'.toInt() // Explicit conversions to numbers
}
```
## Booleans
มี 2 ค่าคือ true และ false และสามารถมีค่าเป็น null 
### Boolean Operations
Operation  | Description
---------  | --------
||    | lazy disjunction
&&    | lazy conjunction
!     | negation
## Arrays
คลาส Array จะมีฟังก์ชัน `get` , `set` ([] คือ operator overloading ของ set) และ `size` 
```kotlin
class Array<T> private constructor() {
    val size: Int
    operator fun get(index: Int): T
    operator fun set(index: Int, value: T): Unit

    operator fun iterator(): Iterator<T>
    // ...
}
```
### Function Create Array
Function     | Description
---------    | --------
arrayOf()    | arrayOf(1, 2, 3)
[1, 2, 3]    |  
arrayOfNulls() |  
```kotlin
// Creates an Array<String> with values ["0", "1", "4", "9", "16"]
val asc = Array(5, { i -> (i * i).toString() })
asc.forEach { println(it) }
```
### Arrays Of Primitive
Class     | Description
---------    | --------
ByteArray    | 
ShortArray   | 
IntArray     |  
`ทุกคลาสจะสืบทอดมาจากคลาส Array` 
```kotlin
val x: IntArray = intArrayOf(1, 2, 3)
x[0] = x[1] + x[2]
```
## Unsigned integers
Class     | Description
---------    | --------
kotlin.UByte | 0 to 255
kotlin.UShort | 0 to 65535
kotlin.UInt |  0 to 2^32 - 1
kotlin.ULong |  0 to 2^64 - 1