### My Journey as a Software Engineer: Lessons Learned and Best Practices

By: [Partha Sarathi Kundu](https://www.linkedin.com/in/partha-sarathi-kundu/recent-activity/articles/)

[SQL Database Configuration, Support, and Troubleshooting](/SQL-config-debug-tips-tricks.md)

---

[3 most important skills for SWE](/skills-for-SWE.md)

Over the years, my journey as a software engineer has been filled with challenges, triumphs, and countless lessons. When I started, I often found myself overwhelmed by the sheer breadth of knowledge needed—design principles, frameworks, database optimization, server configurations, and more. But with time, experience, and a lot of trial and error, I’ve developed a toolkit of practices and principles that have consistently helped me deliver high-quality solutions.

Today, I’m sharing what I’ve learned—not from theory, but from real-world experience. These are the practices I wish I knew earlier and the ones I follow every day to build scalable, maintainable, and impactful software systems.

---

## **1. Core Software Design Methods**

When I first encountered poorly designed systems, I realized the importance of strong design principles. I remember one project where a single class handled everything—database access, business logic, and even email notifications. Every change broke something. That’s when I discovered **SOLID principles**.

### **SOLID Principles in Action**
- **Single Responsibility Principle (SRP):** One project involved a file-processing system. Initially, the code to read files, validate them, and save them to the database was all in one function. Refactoring into separate classes for reading, validating, and saving made the code much easier to test and maintain.
- **Open/Closed Principle (OCP):** I worked on an e-commerce platform where we needed to add a new payment method. Because we used interfaces like `IPaymentGateway`, I could add Stripe support without touching the existing PayPal code.
- **Dependency Inversion Principle (DIP):** On a healthcare project, we implemented `ILogger` as an interface and passed it to services through dependency injection. This made it easy to swap our logging provider from a file-based system to cloud-based monitoring.

---

## **2. Best Practices for Programming**

### **Writing Readable and Maintainable Code**
Early in my career, I wrote code that only *I* could understand. This became a bottleneck when teams needed to scale. I learned to prioritize clarity:
- Use descriptive variable names: Replace `int x` with `int patientAge`.
- Add meaningful comments only where necessary. Don’t clutter code with obvious statements.

### **C# and .NET: My Go-To Stack**
.NET with C# has been my primary stack for years, and I’ve learned a few hard-earned lessons along the way:
1. **Organize Your Code:** On one project, I adopted the **Clean Architecture** pattern. Separating the **Domain**, **Application**, **Infrastructure**, and **Presentation** layers made the system easier to understand and extend.
2. **Dependency Injection:** I once worked on a system with tightly coupled classes that were impossible to test. Switching to DI resolved this and made our code modular.
   ```csharp
   services.AddScoped<IUserService, UserService>();
   ```
3. **Async Programming:** Asynchronous methods dramatically improved the performance of an API we built for a logistics company. Tasks that used to block threads were now processed concurrently.

---

## **3. The Art of Database Optimization**

One of the biggest performance challenges I faced was a reporting system that queried millions of rows. Poor database design and inefficient queries made reports unbearably slow. Here’s what I learned:

### **Indexing for Performance**
Indexes saved us. For example, indexing the `created_at` column in our transaction table reduced query times from minutes to seconds.

### **Parameterized Queries for Security**
In one incident, a colleague wrote dynamic SQL that exposed us to SQL injection. Since then, I always use parameterized queries:
```sql
SELECT * FROM Users WHERE Username = ? AND Password = ?;
```

### **Optimizing Joins**
Once, I rewrote a nested query into a JOIN and reduced processing time by 90%. Always prefer joins over subqueries when possible.

---

## **4. Framework-Based Development**

### **ASP.NET Core: A Framework That Stands Out**
I’ve built APIs, web apps, and microservices with ASP.NET Core. One of my favorite features is the middleware pipeline. For instance, I added a custom middleware to log incoming requests and measure response times:
```csharp
app.Use(async (context, next) => {
    var startTime = DateTime.UtcNow;
    await next();
    var duration = DateTime.UtcNow - startTime;
    Console.WriteLine($"Request took {duration.TotalMilliseconds} ms");
});
```

Another project involved integrating **Entity Framework Core** for database interactions. While it’s a powerful ORM, I learned to avoid fetching entire tables by using projections and `.Select()`.

---

## **5. Networking Basics Every Engineer Should Know**

When I first started deploying applications, I was clueless about networking. After a few panicked troubleshooting calls, I made it a point to understand the basics.

### **DNS and IPs**
Configuring DNS for a corporate client taught me how critical it is to map domain names to the correct IP addresses. A simple typo can bring down a system.

### **TLS and HTTPS**
On a retail project, a lack of HTTPS exposed sensitive user data. I quickly learned to configure TLS certificates on IIS to secure our API endpoints.

### **Load Balancers**
One Black Friday, our servers couldn’t handle the traffic spike. Adding an HAProxy load balancer distributed the load across multiple servers, ensuring smooth operations.

---

## **6. Everyday Tools I Rely On**

1. **Visual Studio & VS Code:** Visual Studio is perfect for large .NET projects, while VS Code’s lightweight nature makes it ideal for quick fixes.
2. **Postman:** An indispensable tool for testing APIs. It helped me debug a payment gateway integration that returned cryptic errors.
3. **Git:** Branching strategies like GitFlow have saved me from deployment nightmares. Always use `git pull` with caution in production branches!

---

## **7. Real-World Challenges and Solutions**

### **Debugging in Production**
During one deployment, a critical API started timing out. Using **Application Insights**, I traced the issue to a poorly optimized SQL query. Fixing it required a quick index addition—a reminder to always test queries on production-scale data.

### **Scaling Systems**
For a healthcare app, scaling was a challenge as user numbers grew. Migrating from a monolithic architecture to microservices allowed us to scale individual components independently.

---

## **Conclusion: A Journey of Continuous Learning**

Software engineering is a journey of constant growth. From debugging a crashing system at 2 AM to successfully deploying a flawless feature, every challenge is an opportunity to learn. The practices and lessons I’ve shared here have helped me navigate this journey, and I hope they guide you as well.

Whether you’re a seasoned engineer or just starting, remember: the goal isn’t just to write code—it’s to solve problems, learn continuously, and build systems that make a difference. Keep experimenting, stay curious, and never stop improving.