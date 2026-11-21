# Exp 03 - Entity-Student-and-build-a-CRUD-operations-using-Spring-Boot-Hibernate-Configuration

## AIM:
To develop a Spring Boot application that performs CRUD (Create, Read, Update, Delete) operations on a Student entity using Spring Data JPA (Hibernate).

## ALGORITHM:
1. Create Spring Boot Project
2. Add dependencies: Spring Web, Spring Data JPA, H2 Database or MySQL, Spring Boot DevTools
3. Configure application.properties
4. Define database connection
5. Enable Hibernate auto DDL
6. Create Student Entity Class
7. Annotate with @Entity
8. Define fields with @Id, @GeneratedValue, etc.
9. Create StudentRepository
10. Extend JpaRepository<Student, Long> for CRUD methods
11. Create StudentController
12. Handle HTTP methods:
* POST /students → Add student
* GET /students → Get all students
* GET /students/{id} → Get student by ID
* PUT /students/{id} → Update student
* DELETE /students/{id} → Delete student


## PROGRAM CODE

### pom.xml

```
<dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-jpa</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-webmvc</artifactId>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>com.mysql</groupId>
            <artifactId>mysql-connector-j</artifactId>
            <scope>runtime</scope>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-jpa-test</artifactId>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-webmvc-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>


```
 ### application.properties

```
spring.application.name=experiment3
spring.datasource.url=jdbc:mysql://localhost:3306/students?useSSL=false&allowPublicKeyRetrieval=true&serverTimezone=UTC
spring.datasource.username=root
spring.datasource.password=2096
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.jpa.database-platform=org.hibernate.dialect.MySQLDialect
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true
```

### Student.java
```
package com.example.experiment3.model;

import jakarta.persistence.*;

@Entity
public class Student {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;
    private String department;
    private int age;

    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getDepartment() {
        return department;
    }

    public void setDepartment(String department) {
        this.department = department;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}

```
### StudentController.java

```
@RestController
@RequestMapping("/students")
public class StudentController {

    @Autowired
    private StudentRepository studentRepository;

    @PostMapping("/data")
    public Student addStudent(@RequestBody Student student) {
        return studentRepository.save(student);
    }

    @GetMapping
    public List<Student> getAllStudents() {
        return studentRepository.findAll();
    }

    @GetMapping("/{id}")
    public Optional<Student> getStudent(@PathVariable Long id) {
        return studentRepository.findById(id);
    }

    @PutMapping("/{id}")
    public Student updateStudent(@PathVariable Long id, @RequestBody Student studentDetails) {
        Student student = studentRepository.findById(id).orElseThrow();
        student.setName(studentDetails.getName());
        student.setAge(studentDetails.getAge());
        student.setDepartment(studentDetails.getDepartment());
        return studentRepository.save(student);
    }

    @DeleteMapping("/{id}")
    public String deleteStudent(@PathVariable Long id) {
        studentRepository.deleteById(id);
        return "Student with ID " + id + " deleted successfully!";
    }
}

```

### StudentRepository.java
```
package com.example.experiment3.repository;

import com.example.experiment3.model.Student;
import org.springframework.data.jpa.repository.JpaRepository;

public interface StudentRepository extends JpaRepository<Student, Long> {
}
```
### Experiment3Application.java

```
package com.example.experiment3;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Experiment3Application {

    public static void main(String[] args) {
        SpringApplication.run(Experiment3Application.class, args);
    }

}
```

## Output:

# POST /students/data

<img width="1917" height="1006" alt="Screenshot 2026-11-20 115841" src="https://github.com/user-attachments/assets/95c7b09a-5c66-486c-9d2b-1a4487b10841" />


# GET /students

<img width="1917" height="1021" alt="Screenshot 2026-11-20 115934" src="https://github.com/user-attachments/assets/ee648be6-140c-499a-adbf-185864edd0e7" />

# GET /students/:id

<img width="1917" height="1020" alt="Screenshot 2026-11-20 120021" src="https://github.com/user-attachments/assets/119283d6-7950-46bc-b836-95eab145dae6" />

# PUT /students/:id

<img width="1917" height="1017" alt="Screenshot 2026-11-20 120155" src="https://github.com/user-attachments/assets/0baefe20-5e12-4689-ae88-5b9baffadbfa" />

# DELETE /students/:id

<img width="1917" height="1006" alt="Screenshot 2026-11-20 120221" src="https://github.com/user-attachments/assets/a293a3d6-327b-4599-99a8-408543c54e0a" />


### Result:
Thus, The program to develop a Spring Boot application that performs CRUD (Create, Read, Update, Delete) operations on a Student entity using Spring Data JPA (Hibernate) is executed successfully. 




