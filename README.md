Got it — you want **ALL answers (1a–1e and 2a–2e)** in a **simple, ready-to-write format**, without changing Docker/Jenkins much. Perfect 👍

From your paper , there are **2 main questions**:

---

# ✅ **QUESTION 1 (a–e): Java Maven App (CI/CD)**

👉 Same setup for all (only logic changes)

---

## 🔹 Common Files (Same for 1a–1e)

### ✔ Maven Structure

```
src/
 ├── main/java/com/example/App.java
 └── test/java/com/example/AppTest.java
```

---

### ✔ `pom.xml` (same for all)

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.example</groupId>
  <artifactId>demo</artifactId>
  <version>1.0</version>

  <dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.13.2</version>
      <scope>test</scope>
    </dependency>
  </dependencies>
</project>
```

---

## 🔸 1(a) Addition

```java
public class App {
    public static int add(int a, int b) {
        return a + b;
    }
}
```

### Test

```java
@Test
public void testAdd() {
    assertEquals(5, App.add(2, 3));
}
```

---

## 🔸 1(b) Even/Odd

```java
public class App {
    public static boolean isEven(int n) {
        return n % 2 == 0;
    }
}
```

### Test

```java
@Test
public void testEven() {
    assertTrue(App.isEven(4));
}
```

---

## 🔸 1(c) Multiplication

```java
public class App {
    public static int multiply(int a, int b) {
        return a * b;
    }
}
```

---

## 🔸 1(d) Factorial

```java
public class App {
    public static int factorial(int n) {
        int result = 1;
        for(int i=1;i<=n;i++)
            result *= i;
        return result;
    }
}
```

---

## 🔸 1(e) Prime Number

```java
public class App {
    public static boolean isPrime(int n) {
        if(n<=1) return false;
        for(int i=2;i<=n/2;i++)
            if(n%i==0) return false;
        return true;
    }
}
```

---

# 🔁 Jenkins Pipeline (Same for all 1a–1e)

```groovy
pipeline {
 agent any

 stages {

  stage('Clone') {
   steps {
    git 'https://github.com/yourrepo.git'
   }
  }

  stage('Build') {
   steps {
    bat 'mvn clean package'
   }
  }

  stage('Test') {
   steps {
    bat 'mvn test'
   }
  }

  stage('Docker Build') {
   steps {
    bat 'docker build -t java-app .'
   }
  }
 }
}
```

---

# 🐳 Dockerfile (Same for all 1a–1e)

```dockerfile
FROM openjdk:17
COPY target/demo.jar app.jar
ENTRYPOINT ["java","-jar","/app.jar"]
```

---

# ✅ **QUESTION 2 (a–e): Static Web Pages (CI/CD + Kubernetes)**

👉 Only HTML changes, rest SAME

---

## 🔹 Common Files (Same for all)

### ✔ Dockerfile

```dockerfile
FROM nginx:latest
COPY index.html /usr/share/nginx/html/
```

---

### ✔ Jenkinsfile (same)

```groovy
pipeline {
 agent any

 stages {
  stage('Clone'){ steps{ git 'repo-link' } }
  stage('Build'){ steps{ bat 'docker build -t webapp .' } }
  stage('Deploy'){
   steps{
    bat 'kubectl apply -f deployment.yaml'
    bat 'kubectl apply -f service.yaml'
   }
  }
 }
}
```

---

### ✔ Kubernetes (same)

#### deployment.yaml

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: webapp
spec:
  replicas: 2
  selector:
    matchLabels:
      app: web
  template:
    metadata:
      labels:
        app: web
    spec:
      containers:
      - name: web
        image: webapp
        ports:
        - containerPort: 80
```

#### service.yaml

```yaml
apiVersion: v1
kind: Service
metadata:
  name: web-service
spec:
  type: NodePort
  selector:
    app: web
  ports:
    - port: 80
      nodePort: 30007
```

---

# 🔸 2(a) Student Results

```html
<h1>Student Results</h1>
<ul>
<li>John - Pass</li>
<li>Ravi - Fail</li>
</ul>
```

---

# 🔸 2(b) Rivera Events

```html
<h1>Rivera Events</h1>
<ul>
<li>Dance</li>
<li>Music</li>
<li>Drama</li>
<li>Quiz</li>
<li>Gaming</li>
</ul>
```

---

# 🔸 2(c) Conference Info

```html
<h1>Conference</h1>
<p>Date: 10 Aug</p>
<p>Venue: Chennai</p>
<p>Topic: AI & ML</p>
```

---

# 🔸 2(d) Price List (YOURS)

```html
<h1>Price List</h1>
<ul>
<li>Laptop - 50000</li>
<li>Mobile - 20000</li>
</ul>
```

---

# 🔸 2(e) Timetable

```html
<h1>Timetable</h1>
<ul>
<li>Math</li>
<li>Physics</li>
<li>CS</li>
</ul>
```

---

# 📸 What to Submit (IMPORTANT)

From your paper :

✅ Jenkins Stage View
✅ Console Output
✅ GitHub Link


<!DOCTYPE html>
<html>
<body>

<h2>Timetable</h2>

<table border="1">
    <tr>
        <th>Day</th>
        <th>Subject</th>
    </tr>
    <tr>
        <td>Monday</td>
        <td>Math</td>
    </tr>
    <tr>
        <td>Tuesday</td>
        <td>Physics</td>
    </tr>
</table>

</body>
</html>
