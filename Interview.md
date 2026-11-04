# Java Interview Questions

## 1. JDK, JRE, and JVM are three important components of Java.

- JDK (Java Development Kit): Used to develop, compile, and run Java applications. It includes development tools like javac, java, and javadoc.
- JRE (Java Runtime Environment): Provides the environment required to run Java applications. It includes the JVM and supporting libraries.
- JVM (Java Virtual Machine): Executes Java bytecode and provides platform independence. It also handles memory management and garbage collection.

## 2. How a Java program runs

javac compiles .java source into bytecode in .class files. Then the JVM loads, verifies, and runs that bytecode.

- javac turns Hello.java into Hello.class (bytecode, not machine code).
- java Hello starts the JVM.
- The class loader loads the class (bootstrap, platform, then application loaders).
- The bytecode verifier checks the code is safe.
- The execution engine runs it, using an interpreter and a JIT compiler.

## 3. Interpreter vs JIT Compiler
Interpreter and JIT (Just-In-Time) Compiler are two mechanisms used by the JVM to execute Java bytecode.

- Interpreter: Executes Java bytecode instruction by instruction. It starts execution quickly but is generally slower for repeatedly executed code.

- JIT Compiler: Converts frequently executed bytecode into native machine code at runtime, improving performance.

> "In Java, the Interpreter and JIT Compiler are part of JVM execution.
>
> The Interpreter executes bytecode instruction by instruction.
>
> The JIT Compiler identifies frequently executed code and compiles it into machine code.
>
> So, the Interpreter helps with quick startup, while the JIT Compiler improves execution speed."

## 4. Primitive vs Non-primitive
### 1. Primitive Data Types

Primitive data types are the basic built-in data types in Java.

Java has **8 primitive data types**:

| Data Type | Size | Range |
|-----------|------|-------|
| `byte` | 1 byte (8 bits) | -128 to 127 |
| `short` | 2 bytes (16 bits) | -32,768 to 32,767 |
| `int` | 4 bytes (32 bits) | -2³¹ to 2³¹ - 1 |
| `long` | 8 bytes (64 bits) | -2⁶³ to 2⁶³ - 1 |
| `float` | 4 bytes (32 bits) | Approx. ±3.4 × 10³⁸ |
| `double` | 8 bytes (64 bits) | Approx. ±1.8 × 10³⁰⁸ |
| `char` | 2 bytes (16 bits) | 0 to 65,535 (`'\u0000'` to `'\uffff'`) |
| `boolean` | JVM-dependent storage | `true` or `false` |

### Key Points

- Store simple values directly.
- Have fixed sizes (except boolean, whose size is not precisely defined).
- Cannot call methods directly on primitive values.
- Generally use less memory than objects.


### 2. Non-Primitive Data Types

Non-primitive data types are also called **Reference Data Types**.

They refer to objects or arrays rather than directly containing primitive values.

### Examples

- String
- Array
- Class
- Object
- Interface
- Enum

### Key Points

- Variables store references to objects or arrays.
- Can have methods and properties depending on the type.
- Can hold `null`.
- Objects are generally allocated on the heap.

### 3. Primitive vs Non-Primitive

| Primitive | Non-Primitive |
|-----------|---------------|
| Stores actual value | Stores a reference |
| 8 built-in types | Many reference types |
| Cannot be null | Can be null |
| Cannot call methods directly | Can access methods |
| Examples: int, char | Examples: String, Array |

> "In Java, data types are divided into two categories: Primitive and Non-Primitive.
>
> Primitive data types store simple values directly. Java has eight primitive types, such as int, double, char, and boolean.
>
> Non-Primitive data types are reference types, such as String, Array, and Class. They store references to objects or arrays and can have methods.
>
> The main difference is that primitive variables hold actual values, while non-primitive variables hold references to objects."

## 5. Wrapper Class , Autoboxing & Unboxing
Wrapper classes are objects that hold primitive values (Integer, Long, Double, Character, Boolean, and so on). Autoboxing and unboxing convert between the two automatically.

> Autoboxing: Integer x = 5; becomes Integer.valueOf(5).
>
> Unboxing: int y = x; becomes x.intValue().
>
> Use wrappers for generics (List<Integer>) because generics only accept objects.   
>
> Wrappers can be null. Unboxing null throws NullPointerException.


## 6. Integer Cache
Integer.valueOf() reuses cached objects for values from -128 to 127. So == returns true in that range but false outside it, because it compares references.

```java
Integer a = 127, b = 127;
System.out.println(a == b);       // true  (same cached object)

Integer c = 128, d = 128;
System.out.println(c == d);       // false (different objects)
System.out.println(c.equals(d));  // true  (compares values)
```

- Always compare wrapper values with equals().
- Byte, Short, Long, and Character (0 to 127) also cache values. Float and Double never cache.
- The upper limit of the Integer cache can be raised with `-XX:AutoBoxCacheMax=<n>`.
- new Integer(...) is deprecated. Use Integer.valueOf() or autoboxing.

> Likely follow-up: “Why use the cache?” It saves memory and allocation time for common small values.   