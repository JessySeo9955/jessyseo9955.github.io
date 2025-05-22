---
layout: post
title:  "[DevOps] AWS Lambda, API Gateway"
date:   2025-05-19 20:27:14 -0400
categories: jekyll update
---
## Project
- DateTime Formatter
- Java, Gradle, FatJar, AWS Lambda, AWS Gateway
- Junit, Cucumber, AssertJ


## References
<details>
  <summary>API Gateway VS Load Balancer</summary>

API Gateway is tailored for API management, serverless applications, and advanced API features (like security, rate limiting, etc.), while Load Balancers are more focused on distributing traffic to backend servers, typically for traditional web applications or microservices that are server-based (EC2, ECS).
### Summary of Differences:

| Feature | **API Gateway** | **Load Balancer** (ALB/NLB) |
| --- | --- | --- |
| **Purpose** | Manage and expose APIs | Distribute traffic across servers or instances |
| **Protocols Supported** | HTTP/S, WebSocket | HTTP/S, TCP, UDP (ALB, NLB) |
| **Serverless Support** | Deep integration with AWS Lambda | Not typically serverless-focused |
| **Traffic Routing** | API-specific routing, path, method, query params, headers | Based on availability, host, and path |
| **Advanced Features** | Request/response transformation, authentication, caching, rate limiting | Basic load balancing, health checks |
| **Use Case** | REST APIs, WebSocket APIs, serverless apps | Web applications, microservices, EC2 instances, containers |

</details>

<details>
  <summary>API Gateway HTTP API VS  REST API </summary>

- HTTP API (newer, simpler, cheaper)
- REST API (older, more powerful, more expensive)

### Summary of Differences:
| Feature | **HTTP API** (Recommended for most new projects) | **REST API** (Advanced use cases) |
| --- | --- | --- |
| **Pricing** | ✅ Cheaper (up to 70% less) | ❌ More expensive |
| **Performance** | ✅ Lower latency | ❌ Slightly higher latency |
| **Ease of Use** | ✅ Simpler, faster setup | ❌ More complex setup |
| **Features** | ❌ Fewer features | ✅ More features (e.g., request/response mapping) |
| **Authorization** | ✅ IAM, JWT (Cognito), Lambda authorizers | ✅ IAM, Cognito, Lambda authorizers |
| **Custom Domain Support** | ✅ Yes | ✅ Yes |
| **WebSockets Support** | ❌ No | ✅ Yes |
| **Caching** | ❌ No | ✅ Yes |
| **API Gateway VPC Links** | ❌ No | ✅ Yes |
| **Use Case** | 💡 Basic APIs, microservices, mobile backends | 💡 Complex APIs with transformations, legacy support |
</details>

<details>
    <summary>Fat JAR vs AWS Lambda Layer </summary>

| Use Case | Recommended Approach |
| --- | --- |
| Simpler projects, fast iteration | ✅ Fat JAR |
| Many functions sharing dependencies | 🔄 Fat JAR + Layers |
| Enterprise-scale, optimized builds | ✅ Layers (with CI/CD) |
### Fat JAR
When you build the Fat JAR, the contents of gson-2.8.8.jar are flattened and merged directly into the root of your Fat JAR. So your Fat JAR will look something like this:
<pre>
my-application.jar
│
├── META-INF/
│   ├── MANIFEST.MF
│
├── com/                        (Your application's classes)
│   └── myapp/
│       └── Main.class
│
├── com/                        (Flattened dependency classes)
│   └── google/
│       └── gson/
│           ├── Gson.class
│           ├── JsonObject.class
│           └── ...
└── ...                         (Other dependencies)
</pre>
</details>




<details>
    <summary>java.time package</summary>

### ✅ 1. **High-Precision Date/Time (Nanoseconds)**

Java’s `java.time` API provides **nanosecond precision** when handling timestamps, making it much more accurate than JavaScript's `Date` (which only offers **millisecond** precision).

Example:

```java
import java.time.Instant;

public class Main {
    public static void main(String[] args) {
        Instant instant = Instant.now();  // Current time with nanosecond precision
        System.out.println("Current instant: " + instant);
    }
}
```

Output:

```
2025-05-22T14:38:19.950446356Z
```

* Java can track **nanoseconds**, while JavaScript `Date.now()` can only give you **milliseconds**.

---

### ✅ 2. **Comprehensive Time Zone Handling (IANA Time Zones)**

Java has **full support** for time zones with the `ZoneId` and `ZonedDateTime` classes, which are part of the modern `java.time` package. You can easily handle **all time zones** using the IANA time zone database, and Java's time zone handling is **more complete** and **accurate** compared to JavaScript’s `Intl.DateTimeFormat`.

Example:

```java
import java.time.ZonedDateTime;
import java.time.ZoneId;

public class Main {
    public static void main(String[] args) {
        ZonedDateTime seoulTime = ZonedDateTime.now(ZoneId.of("Asia/Seoul"));
        System.out.println("Time in Seoul: " + seoulTime);
    }
}
```

* Java uses the full IANA time zone database (e.g., `"Asia/Seoul"`, `"America/Toronto"`), while JavaScript relies on the `Intl` API, which may not cover all edge cases in some browsers.

---

### ✅ 3. **Chrono Units & Advanced Calculations**

Java has rich support for **advanced time calculations** using the `ChronoUnit` class, which allows you to perform time arithmetic in a **precise** and **typesafe** way (e.g., calculating **hours**, **days**, **weeks**, and even **periods**).

Example:

```java
import java.time.LocalDateTime;
import java.time.temporal.ChronoUnit;

public class Main {
    public static void main(String[] args) {
        LocalDateTime now = LocalDateTime.now();
        LocalDateTime later = now.plus(5, ChronoUnit.DAYS);
        System.out.println("5 days later: " + later);
    }
}
```

---

### ✅ 4. **Temporal Adjusters**

Java provides powerful **Temporal Adjusters** for manipulating dates, such as getting the **first day of the next month** or the **last day of the year**.

Example:

```java
import java.time.LocalDate;
import java.time.temporal.TemporalAdjusters;

public class Main {
    public static void main(String[] args) {
        LocalDate date = LocalDate.of(2025, 5, 22);
        LocalDate firstDayOfNextMonth = date.with(TemporalAdjusters.firstDayOfNextMonth());
        System.out.println("First day of next month: " + firstDayOfNextMonth);
    }
}
```

This allows for advanced date manipulation that's much cleaner and more intuitive than using custom JavaScript functions.

---

### ✅ 5. **Immutability and Thread-Safety**

Java's **`java.time`** package was designed to be **immutable** and **thread-safe** from the start. Classes like `LocalDate`, `ZonedDateTime`, and `Duration` are **immutable** by design, meaning their state cannot be changed once they’re created. This makes them **safe** to use in **multithreaded** environments without worrying about synchronization issues.

In contrast, while JavaScript's `Date` object can be mutable and not inherently thread-safe (since JS is single-threaded), Java's immutability guarantees that dates and times will remain consistent across different threads.

---

### ✅ 6. **Comprehensive Period and Duration Handling**

Java provides **periods** (representing **years**, **months**, **days**) and **durations** (representing **seconds**, **milliseconds**, **nanoseconds**), making it easy to calculate intervals between dates/times or represent elapsed time.

Example:

```java
import java.time.Duration;
import java.time.LocalDateTime;

public class Main {
    public static void main(String[] args) {
        LocalDateTime start = LocalDateTime.of(2025, 5, 22, 8, 0);
        LocalDateTime end = LocalDateTime.of(2025, 5, 22, 14, 30);
        
        Duration duration = Duration.between(start, end);
        System.out.println("Duration: " + duration.toHours() + " hours " + duration.toMinutes() % 60 + " minutes");
    }
}
```

Output:

```
Duration: 6 hours 30 minutes
```

This allows for precise **time duration** handling, which is more structured than JavaScript's `Date` functions.

---

### ✅ 7. **Support for Calendar Systems**

Java supports **multiple calendar systems** (e.g., **ISO**, **Japanese**, **Thai Buddhist**) in addition to the **Gregorian calendar**, making it suitable for more diverse, internationalized applications.

Example:

```java
import java.time.chrono.JapaneseDate;
import java.time.LocalDate;

public class Main {
    public static void main(String[] args) {
        LocalDate currentDate = LocalDate.now();
        JapaneseDate japaneseDate = JapaneseDate.from(currentDate);
        System.out.println("Current date in Japanese calendar: " + japaneseDate);
    }
}
```

* Java’s `java.time.chrono` package makes it easier to work with different calendar systems, whereas JavaScript’s native `Date` is limited to the **Gregorian calendar**.

---

### Summary: Java’s Strengths in Date/Time Handling

* **High-precision** (nanoseconds).
* **Comprehensive time zone handling** with full IANA time zone support.
* **Rich calculation and manipulation** tools (e.g., `ChronoUnit`, `TemporalAdjusters`).
* **Thread-safety** and **immutability** in date/time objects.
* Support for multiple **calendar systems**.

---

### When Should You Use Java for Date/Time?

Java is highly efficient for:

* **Enterprise-level applications** needing robust date/time support (e.g., scheduling, internationalization).
* **Backend systems** where high precision, multithreading, and safe date manipulation are critical.
* **Data-heavy applications** like **financial systems**, **scientific calculations**, or any system where accurate time handling is essential.


</details>