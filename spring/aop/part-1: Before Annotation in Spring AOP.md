---
layout: default
title: AOP অধ্যায় ১
---

অসাধারণ সিদ্ধান্ত নিয়েছেন! ✅ **Java AOP** ও **Spring AOP** শিখলে আপনি production-level application-এ অনেক clean, reusable ও maintainable code লিখতে পারবেন।

আমি আপনাকে ধাপে ধাপে খুবই **beginner-friendly** ভাবে শিখাবো। নিচে পুরো রোডম্যাপ এবং প্রথম লেসন শুরু করছি।

---

## 🧭 শেখার রোডম্যাপ:

1. **AOP Concept (Theory)**
2. **AOP Core Terms** – Aspect, Join Point, Pointcut, Advice, Weaving
3. **Spring AOP Setup** – Project তৈরি
4. **@Before, @After, @Around Advice**
5. **Pointcut Expressions (execution, within, this, @annotation, etc.)**
6. **Custom Annotation Based AOP**
7. **Practical Use Cases: Logging, Security, Validation, Retry, etc.**
8. **Debug & Test AOP**

---

## 🔰 প্রথম ধাপ: AOP Concept বোঝা (এই অংশটা বাংলায় বুঝুন)

### 🎯 AOP কি?

AOP মানে হলো এমন কোড লেখা যা মুল কাজের বাইরে থাকে কিন্তু প্রায়ই দরকার হয়।

**যেমন:**

* প্রতিটি মেথড শুরু হলে লগিং করা,
* exception ধরলে একটা মেসেজ পাঠানো,
* প্রতিটি সার্ভিস মেথডে ইউজার অথরাইজড কিনা তা চেক করা,
  এই কাজগুলো business logic নয় — এগুলো **cross-cutting concerns**।

AOP এই কাজগুলো এক জায়গায় লিখে সব জায়গায় apply করতে সাহায্য করে।

---

## 🧪 Practical শুরু করি

### 🔨 Step 1: Spring Boot Project তৈরি

আপনি চাইলে IntelliJ বা Spring Initializr দিয়ে নিচের মতো করে একটা প্রজেক্ট বানাতে পারেন:

**Dependencies দিন:**

* Spring Web
* Spring AOP
* Lombok (optional)

---

### 📁 Folder Structure:

```
src/main/java/com/example/aopdemo
│
├── AopDemoApplication.java
├── service/
│   └── HelloService.java
├── aspect/
│   └── LoggingAspect.java
```

---

### ✍️ Step 2: HelloService.java

```java
package com.example.aopdemo.service;

import org.springframework.stereotype.Service;

@Service
public class HelloService {
    public String sayHello(String name) {
        return "Hello, " + name + "!";
    }
}
```

---

### ✍️ Step 3: LoggingAspect.java

```java
package com.example.aopdemo.aspect;

import org.aspectj.lang.JoinPoint;
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Before;
import org.springframework.stereotype.Component;

@Aspect
@Component
public class LoggingAspect {

    @Before("execution(* com.example.aopdemo.service.HelloService.*(..))")
    public void logBefore(JoinPoint joinPoint) {
        System.out.println("Method Called: " + joinPoint.getSignature().getName());
    }
}
```

---

### ✍️ Step 4: Main Class থেকে Call করুন

```java
package com.example.aopdemo;

import com.example.aopdemo.service.HelloService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.CommandLineRunner;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class AopDemoApplication implements CommandLineRunner {

    @Autowired
    private HelloService helloService;

    public static void main(String[] args) {
        SpringApplication.run(AopDemoApplication.class, args);
    }

    @Override
    public void run(String... args) {
        System.out.println(helloService.sayHello("Shakib"));
    }
}
```

---

### ✅ Output:

```
Method Called: sayHello
Hello, Shakib!
```

🎉 Bingo! এটিই আপনার প্রথম AOP Implementation ✅

---

## 🔜 পরবর্তী ধাপ কী?

আমি পরবর্তী লেসনে শিখাবো:

* `@After`, `@Around` কিভাবে কাজ করে
* Pointcut expression কিভাবে use করা যায়
* Custom annotation দিয়ে কিভাবে AOP চালানো যায়

আপনি যদি বলেন, আমি ধাপে ধাপে পরবর্তী লেসন শিখিয়ে দেব।

🔔 আপনি কি এখন `@After`, `@Around` বা **custom annotation** ভিত্তিক AOP শিখতে চান? জানান, শুরু করি।
