# Default Constructor

Default Constructor ทำหน้าที่เดียวกับ constructor กล่าวคือ ใช้สำหรับกำหนดค่าใน fields ให้กับวัตถุ แต่ Default Constructor แตกต่างออกไป โดยที่ จะไม่รับ parameters ใดๆ ซึ่งจะกำหนดค่าเริ่มต้นให้กับฟิลด์ของวัตถุ

```csharp
class Person
{
    public string name;
    public int age;
    // Implicit default constructor
}
```

เห็นได้ว่าคลาส Person ไม่มี constructor ใดๆ เมื่อมีการสร้างวัตถุของ Person ตัว compiler จะกำหนดค่าเริ่มต้นให้ ผลลัพธ์เมื่อสร้างวัตถุ

```csharp
Person p = new Person();
Console.WriteLine($"Name: {p.name}");     
Console.WriteLine($"Age: {p.age}");
```

<details>

<summary>ผลลัพธ์</summary>

```csharp
Name: 
Age: 0
```

</details>

## Implicit default constructor&#x20;

เมื่อไม่มีการประกาศ constructor ใดๆ ในคลาส compiler จะสร้าง default constructor ให้โดยอัตโนมัติดังตัวอย่างก่อนหน้า

## Explicit default constructor&#x20;

เป็นการสร้าง default constructor โดยที่ผู้เขียนกำหนดข้อมูลเริ่มต้นด้วยตัวเอง

```csharp
class Person
{
    public string name;
    public int age;

    // Explicit default constructor
    public Person()
    {
        name = "_";
        age = 20;
    }

    public static void Main(string[] args)
    {
        Person p = new Person();
        Console.WriteLine($"Name: {p.name}");     
        Console.WriteLine($"Age: {p.age}");
    }
}
```

<details>

<summary>ผลลัพธ์</summary>

```
Name: _
Age: 20
```

</details>

เห็นได้ว่าผู้เขียนได้กำหนดค่าเริ่มต้นให้กับ Name = "\_", age = 20 ผลลัพธ์ที่ได้ คือ name จะไม่มีค่า null และ age ไม่มีค่า 0 เหมือน Implicit default constructor แล้ว

## ค่าเริ่มต้นที่กำหนด&#x20;

ค่าเริ่มต้นที่กำหนดให้ขึ้นอยู่กับชนิดข้อมูลของฟิลด์แต่ละตัว

* `Numeric` เช่น `int`, `float`, `double`, `decimal` จะถูกกำหนดค่าเริ่มต้นเป็น <mark style="color:red;">0</mark>
* `Boolean` จะถูกกำหนดเป็น <mark style="color:red;">false</mark>
* `Character` จะถูกกำหนดเป็นค่า <mark style="color:yellow;">null</mark>
* `Reference` เช่น string, คลาสต่าง ๆ, อาเรย์ จะถูกกำหนดเป็น <mark style="color:yellow;">null</mark>
* `Enum` ค่าเริ่มต้นจะเป็น สมาชิกตัวแรก&#x20;

| Type                        | Default value                         |
| --------------------------- | ------------------------------------- |
| reference type              | `null`                                |
| numeric type                | 0 (zero)                              |
| floating-point numeric type | 0 (zero)                              |
| bool                        | `false`                               |
| char                        | `'\0'` (U+0000) null character        |
| enum                        | สมาชิกตัวแรก                          |
| struct                      | สมาชิกแต่ละตัว จะมีค่า default values |

```csharp
class Person
{
    public string name;
    public int age;
    public bool isAlive;
    public char code;
    
    public enum Gender
    {
        Male,
        Female
    }
    
    public static void Main(string[] args)
    {
        Person p = new Person();
        Console.WriteLine($"Name: {p.name}");     
        Console.WriteLine($"Age: {p.age}");        
        Console.WriteLine($"IsAlive: {p.isAlive}");
        Console.WriteLine($"Code: {p.code}");      
        Console.WriteLine($"Gender: {p.gender}"); 
    }
}
```

<details>

<summary>ผลลัพธ์</summary>

```csharp
Name:   //null
Age: 0
IsAlive: False
Code:   // null character
Gender: Male
```

</details>

## ข้อสำคัญ

ถ้าผู้เขียนใส่ constructor อย่างน้อยหนึ่งอัน compiler จะไม่สร้าง default constructor ให้เสมอไป

```csharp
class Person
{
    public string name;
    public int age;

    public Person(string name, int age)
    {
        this.name = name;
        this.age = age;
    }

    public static void Main(string[] args)
    {
        Person p = new Person(); // compile-time error
    }
}
```

ดังนั้นเมื่อมีการประกาศ constructor ใดๆแล้ว ถ้าต้องการประกาศ default constructor จะต้องประกาศด้วยตัวเองเพิ่มลงไป

## เปรียบเทียบกับ C,Java,Python

### C

เนื่องจากภาษา C เป็น Procedural programming language จึงไม่มี class หรือ object อย่าง OOP (object-oriented programming) และทำให้มีการทั้ง constructor, default constructor ได้ ซึ่งสามารถทำได้ในภาษาอื่นๆของ C-based นั้นคือ C++, C#

### Java

ภาษา Java เป็นทั้งภาษาที่สนับสนุน OOP จึงมี default constructor เช่นเดียวกับ C#

```java
class Person{
    public String name;
    public int age;
    public boolean isAlive;
    public char code;
    public Gender gender;
    
    public enum Gender
    {
        Male,
        Female
    }

    public static void main(String[] args)
    {
        Person p = new Person();
        System.out.println("Name : " + p.name);
        System.out.println("Age : " + p.age);
        System.out.println("Alive : " + p.isAlive);
        System.out.println("Code : " + p.code);
        System.out.println("Gender : " + p.gender);
    }
}
```

<details>

<summary>ผลลัพธ์</summary>

```java
Name : null
Age : 0
Alive : false
Code : 
Gender : null
```

</details>

แต่มีข้อแตกต่างในส่วนค่าเริ่มต้นของ enum ซึ่งใน Java ค่าเริ่มต้น คือ null ส่วนอื่นๆทำงานเช่นเดียวกับ C#

| Data Type                | Default Value (for fields) |
| ------------------------ | -------------------------- |
| byte                     | 0                          |
| short                    | 0                          |
| int                      | 0                          |
| long                     | 0L                         |
| float                    | 0.0f                       |
| double                   | 0.0d                       |
| char                     | '\u0000'                   |
| String (or any object)   | null                       |
| boolean                  | false                      |

### Python

Python เป็นภาษาสนับสนุน OOP และ การประกาศตัวแปรไม่จำเป็นต้องระบุชนิดข้อมูล(Dynamic Typing) ซึ่งถ้าไม่ได้มีการกำหนดชนิดข้อมูล ก็จะไม่สามารถกำหนดค่าเริ่มต้นให้ตัวแปรได้ ส่วนใหญ่จะใช้วิธี Explicit default constructor แทน

```python
class Person:
    def __init__(self): # explicit default constructor
        self.name = "Unknown"
        self.age = 20

p = Person()
print(p.name)
print(p.age)
```

<details>

<summary>ผลลัพธ์</summary>

```python
Unknown
20
```

</details>

ซึ่งแตกต่างที่สามารถกำหนด default constructor ใน parameters ของ constructor ได้เลย

```python
class Person:
    def __init__(self, name="Unknown", age = 20):
        self.name = name
        self.age = age

p = Person()
print(p.name)
print(p.age)
```

<details>

<summary>ผลลัพธ์</summary>

```python
Unknown
20
```

</details>

และ Python สามารถกำหนดชนิดข้อมูลตอนประกาศตัวแปรได้

```python
class Person:
    name = str()
    age = int()

p = Person()
print(p.name)
print(p.age)
```

<details>

<summary>ผลลัพธ์</summary>

```python
    #null
0
```

</details>

ผลลัพธ์ที่ได้ คือ compiler กำหนดค่าเริ่มต้นให้เมื่อมีการประกาศชนิดข้อมูลร่วมด้วย

#### Python default values

* **Numeric Types**&#x20;
  * จำนวนเต็ม `int` -> <mark style="color:red;">0</mark>&#x20;
  * จำนวนทศนิยม `float` -> <mark style="color:red;">0.0</mark>&#x20;
  * จำนวนเชิงซ้อน `complex` -> <mark style="color:red;">0j</mark>
* **Sequence Types**&#x20;
  * สตริง `str` -> <mark style="color:yellow;">`null`</mark>
  * ลิสต์ `list` -> `[]`
  * `tuple` -> `()`
* **Mapping Type**&#x20;
  * คู่อันดับ `dict` -> `{}`
* **Set Types**&#x20;
  * เซ็ต `set` -> `{}`&#x20;
  * เซ็ตที่ไม่สามารถเปลี่ยนแปลงค่าได้ `frozenset` -> `frozenset()`
* **Boolean Type**&#x20;
  * ค่าความจริง `bool` -> <mark style="color:red;">false</mark>
* **None Type**&#x20;
  * ไม่ระบุชนิดข้อมูล `anyVar` -> <mark style="color:yellow;">None</mark>

## Slide

Default Constructor in C#.pdf

{% file src=".gitbook/assets/Default Constructor.pdf" %}

## Video&#x20;

[Default Constructor in C#](https://youtu.be/4ENzgI9810o)

## Reference :

### C\#

* [C# simple default constructor ](https://www.geeksforgeeks.org/c-sharp-default-constructor/)
* [C# Parameterless constructor(default constructor), default values](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/default-values)

### C

* [Imperative programming language (C) ](https://www.geeksforgeeks.org/what-is-imperative-programming/)

### Java

* [Java default constructor](https://www.javatpoint.com/java-constructor)&#x20;
* [Java default values](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/datatypes.html)

### Python

* [Python Constructor ](https://beginnersbook.com/2018/03/python-constructors-default-and-parameterized/)
* [Python Casting type ](https://www.w3schools.com/python/python\_variables.asp)
