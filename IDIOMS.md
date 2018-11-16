## Creating DTOs (POJOs/POCOs)
```kotlin
data class Customer(val name: String, val email: String)
```
สร้างคลาสด้วย data class จะประกอบด้วยฟังก์ชัน
* getters and setters - val -> กำหนดเฉพาะ getters  ส่วน var -> กำหนดทั้ง getters, setters
* equals()
* hashCode()
* toString()
* copy()
* component1(), component2(), …, for all properties (see Data classes)
## Default values for function parameters
กำหนดค่าดีฟอลต์เป็น 0 ให้กับค่าพารามิเตอร์ a และค่าดีฟอลต์เป็น "" ให้กับค่าพารามิเตอร์ b ถ้าไม่มีการใส่ค่าพารามิเตอร์
```kotlin
fun foo(a: Int = 0, b: String = "") { ... }
```
## Filtering a list
```kotlin
val positives = list.filter { x -> x > 0 }
```
สั้นได้อีก
```kotlin
val positives = list.filter { it > 0 }
```
## String Interpolation
ใช้ชื่อตัวแปรให้เป็นประโยน์ได้อีก ดูเพิ่มเติมที่ String Template
```kotlin
println("Name $name")
```
## Instance Checks
คีย์เวิร์ด when, is ตรวจสอบอินสแตนซ์
```kotlin
when (x) {
    is Foo -> ...
    is Bar -> ...
    else   -> ...
}
```
## Traversing a map/list of pairs
แสดงค่า key, value ใน Map ง่ายๆด้วย in
```kotlin
for ((k, v) in map) {
    println("$k -> $v")
}
```
## Ranges
กำหนดค่าแรนซ์ง่าย ด้วย .. เล่นท่ายากด้วย until, step, downTo
```kotlin
for (i in 1..100) { ... }  // closed range: includes 100
for (i in 1 until 100) { ... } // half-open range: does not include 100
for (x in 2..10 step 2) { ... }
for (x in 10 downTo 1) { ... }
if (x in 1..10) { ... }
```
## Read-only list
คีย์เวิร์ด val มันทำให้ตัวแปรใช้อ่านอย่างเดียว
ฟังก์ชัน listOf จะได้อินสแตนซ์ของอินเตอร์เฟซ List ออกมา
```kotlin
val list = listOf("a", "b", "c")
```
## Read-only map
คีย์เวิร์ด val มันทำให้ตัวแปรใช้อ่านอย่างเดียว
ฟังก์ชัน mapOf จะได้อินสแตนซ์ของอินเตอร์เฟซ Map ออกมา
```kotlin
val map = mapOf("a" to 1, "b" to 2, "c" to 3)
```
## Accessing a map
เข้าถึงข้อมูลใน Map ด้วย key ได้เลยไม่ต้องเรียกเมธอด get(key) เหมือนจาวา
```kotlin
println(map["key"])
map["key"] = value
```
## Lazy property
อันนี้ก็ยังไม่ค่อยเข้าใจ ใส่ TODO ไว้ก่อน ใครเข้าใจก็ช่วยหน่อย
```kotlin
val p: String by lazy {
    // compute the string
}
```
## Extension Functions
นี่มันฟังก์ชันทันใจชัดๆ อยากได้ฟังก์ชันสามารถสร้างได้ทันที
```kotlin
fun String.spaceToCamelCase() { ... }

"Convert this to camelcase".spaceToCamelCase()
```
## Creating a singleton
ไม่ต้องประกาศ private คอนสตรักเตอร์ เหมือนจาวาแล้ว
```kotlin
object Resource {
    val name = "Name"
}
```
## If not null shorthand
ตรวจสอบ null มีมาตรฐานมาให้
```kotlin
val files = File("Test").listFiles()

println(files?.size)
```
## If not null and else shorthand
ตรวจสอบ null มีมาตรฐานมาให้
```kotlin
val files = File("Test").listFiles()
println(files?.size ?: "empty")
```
## Executing a statement if null
เมื่อค่า values["email"] เป็น null จะทำการ throw IllegalStateException
```kotlin
val values = ...
val email = values["email"] ?: throw IllegalStateException("Email is missing!")
```
## Execute if not null
เมื่อค่า value ไม่เป็น null เราสามารถใช้ let เพื่อรันบล็อคคำสั่ง
```kotlin
val value = ...

value?.let {
    ... // execute this block if not null
}
```
## Map nullable value if not null
ใช้ let ร่วมกับ ?: คล้ายกับ Condition Statement ในจาวา 
```kotlin
val value = ...

val mapped = value?.let { transformValue(it) } ?: defaultValueIfValueIsNull
```
## Return on when statement
ค่ารีเทิร์น (Return Type) สามารถใช้ expression ของ when หรือ if หรือ ?:
```kotlin
fun transform(color: String): Int {
    return when (color) {
        "Red" -> 0
        "Green" -> 1
        "Blue" -> 2
        else -> throw IllegalArgumentException("Invalid color param value")
    }
}
```
## try/catch expression
บล็อค try คิดเสียว่าเป็นฟังก์ชันที่ตรวจจับ exception ภายใน ซึ่งสามารถสร้างตัวแปรมารับค่า รีเทิร์นจากบล็อค try
```kotlin
fun test() {
    val result = try {
        count()
    } catch (e: ArithmeticException) {
        throw IllegalStateException(e)
    }

    // Working with result
}
```
## if expression
สร้างตัวแปรมารับค่า รีเทิร์นจากบล็อค if
```kotlin
fun foo(param: Int) {
    val result = if (param == 1) {
        "one"
    } else if (param == 2) {
        "two"
    } else {
        "three"
    }
}
```
## Builder-style usage of methods that return Unit
ฟังก์ชัน fill จะรีเทิร์นค่า Unit ซึ่งสามารถนำมาใช้งานร่วมกับ apply ในการกำหนดค่าเริ่มการสร้างอ็อปเจ็ค
```kotlin
fun arrayOfMinusOnes(size: Int): IntArray {
    return IntArray(size).apply { fill(-1) }
}
```
## Single-expression functions
ค่าคงที่ก็กำหนดเป็นฟังก์ชันได้นะ ประโยชน์ละ? ที่คิดออกก็ Pure Function อย่างอืนมีอีกมั๊ย?
```kotlin
fun theAnswer() = 42
```
หรือ
```kotlin
fun theAnswer(): Int {
    return 42
}
```
ตัวอย่างแรกดูจะง่ายและสั้นกว่า
## Combined with other idioms
มิกซ์กระบวนท่ารวมร่าง 
```kotlin
fun transform(color: String): Int = when (color) {
    "Red" -> 0
    "Green" -> 1
    "Blue" -> 2
    else -> throw IllegalArgumentException("Invalid color param value")
}
```
## Calling multiple methods on instance
with อันนี้เจ๋ง ลดและทำให้โค๊ดดูสะอาดขึ้น 
```kotlin
class Turtle {
    fun penDown()
    fun penUp()
    fun turn(degrees: Double)
    fun forward(pixels: Double)
}

val myTurtle = Turtle()
with(myTurtle) { //draw a 100 pix square
    penDown()
    for(i in 1..4) {
        forward(100.0)
        turn(90.0)
    }
    penUp()
}
```
## Java 7's try with resources
```kotlin
val stream = Files.newInputStream(Paths.get("/some/file.txt"))
stream.buffered().reader().use { reader ->
    println(reader.readText())
}
```
## Consuming a nullable Boolean
null == true -> false
null == false -> true
```kotlin
val b: Boolean? = ...
if (b == true) {
    ...
} else {
    // `b` is false or null
}
```