# NeoflexCalcPractice
## _*Создание контроллера*_
<br>
  В папке src/main/java/ru/neoflex/practice создаём папку controller. <br>
  В ней (/controller) создаём файл CalcController.java <br>
  Над классом указываем аннотацию @RestController <br>
  Создаём 2 public метода с аннотациями @GetMapping("/plus/{a}/{b}")  и @GetMapping("/minus/{a}/{b}"), которые принимают 2 аргумента, типа Integer, а возвращают их сумму/разность соответственно. Перед каждым аргументом метода необходимо поставить @PathVariable("a или b соответственно для каждого аргумента") <br>
    
```
package ru.neoflex.practice.Controller;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class CalcController {
    @GetMapping("/plus/{a}/{b}")
    public Integer Sum (@PathVariable("a") Integer a, @PathVariable("b") Integer b){
        return a+b;
    }
    @GetMapping("/minus/{a}/{b}")
    public Integer Min(@PathVariable("a") Integer a, @PathVariable("b") Integer b){
        return a-b;
    }
}
```
<br>Запускаем сервис, по зеленой кнопке сверху справа в окне Intellij IDEA<br>
Тестируем своё приложение по адресу http://localhost:8080/<адрес_и_параметры_для_2х_созданных_АПИ_из_п.9> 
<br> Сложение <br>
  ![work+](https://github.com/VeithVanJ/NeoflexCalcPractice/blob/main/screenshot/img1.png)<br>
  ![work1+](https://github.com/VeithVanJ/NeoflexCalcPractice/blob/main/screenshot/img1.png)<br>
 Вычитание<br>
  ![work-](https://github.com/VeithVanJ/NeoflexCalcPractice/blob/main/screenshot/img3.png)<br>
  ![work1-](https://github.com/VeithVanJ/NeoflexCalcPractice/blob/main/screenshot/img4.png)<br>

   ## _*Подключение Swagger 3.0.0*_
   <br> Добавляем в pom.xml необходимую зависимость<br>
   ```
    <dependency>
			<groupId>org.springdoc</groupId>
			<artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
			<version>3.0.0</version>
		</dependency>
   ```
<br>Тестируем своё приложение по адресу http://localhost:8080/swagger-ui/index.html
  ![work](https://github.com/VeithVanJ/NeoflexCalcPractice/blob/main/screenshot/img5.png)<br>
Сложение<br>
  ![work2+](https://github.com/VeithVanJ/NeoflexCalcPractice/blob/main/screenshot/img6.png)<br>
Вычитание<br>
  ![work2-](https://github.com/VeithVanJ/NeoflexCalcPractice/blob/main/screenshot/img7.png)<br>
  
## _*Создание тестов на проект*_
<br>Измененный код pom.xml<br>
 ```
   <dependencies>
			<dependency>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-starter-web</artifactId>
			</dependency>
			<dependency>
				<groupId>javax.persistence</groupId>
				<artifactId>javax.persistence-api</artifactId>
				<version>2.2</version>
			</dependency>
			<dependency>
				<groupId>org.projectlombok</groupId>
				<artifactId>lombok</artifactId>
				<optional>true</optional>
			</dependency>
			<dependency>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-starter-test</artifactId>
				<scope>test</scope>
			</dependency>
			<dependency>
				<groupId>org.springdoc</groupId>
				<artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
				<version>2.0.2</version>
			</dependency>
			<dependency>
				<groupId>org.testng</groupId>
				<artifactId>testng</artifactId>
				<version>RELEASE</version>
				<scope>test</scope>
			</dependency>
			<dependency>
				<groupId>org.mockito</groupId>
				<artifactId>mockito-core</artifactId>
				<scope>test</scope>
			</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-data-jpa</artifactId>
		</dependency>
	</dependencies>
   ```
<br>
Код тестов
<br>

   ```
package ru.neoflex.practice;

import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.get;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.content;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.status;
import static org.springframework.test.web.servlet.result.MockMvcResultHandlers.print;

import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.servlet.AutoConfigureMockMvc;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.web.servlet.MockMvc;

@SpringBootTest
@AutoConfigureMockMvc
public class PracticeApplicationTests {

	@Autowired
	private MockMvc mockMvc;

	@Test
	public void sum() throws Exception {
		this.mockMvc.perform(get("/plus/3/2"))
				.andDo(print())
				.andExpect(status().isOk())
				.andExpect(content().string("5"));
	}

	@Test
	public void min() throws Exception {
		this.mockMvc.perform(get("/minus/5/3"))
				.andDo(print())
				.andExpect(status().isOk())
				.andExpect(content().string("2"));
	}
}
   ```

Результаты тестов<br>
  ![test](https://github.com/VeithVanJ/NeoflexCalcPractice/blob/main/screenshot/img8.png) <br>

## _*Подключение in-memory БД*_
<br>
Добавляем в pom.xml необходимые зависимости <br>

```
<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-data-jpa</artifactId>
		</dependency>
		<dependency>
			<groupId>com.h2database</groupId>
			<artifactId>h2</artifactId>
			<scope>runtime</scope>
		</dependency>
```

<br>
Добавляем в файл application.properties строки 
<br>

```
spring.application.name=practice
spring.h2.console.enabled=true
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=pestoivino
spring.datasource.password=5MBA-987aseF
spring.jpa.database-platform=org.hibernate.dialect.H2Dialect
spring.jpa.defer-datasource-initialization=true

```

<br>
Создаём файлы базы данных (DatabaseRes) и репозитория (RepositoryRes)<br>
Код базы данных<br>

```
package ru.neoflex.practice.database;

import jakarta.persistence.*;
import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

@NoArgsConstructor
@AllArgsConstructor
@Data
@Entity
@Table(name = "DatabaseRes")
public class DatabaseRes {
    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    @Column(name = "ID", nullable = false)
    private int ID;

    @Column(name = "first_number")
    private int firstNum;

    @Column(name = "action")
    private String action;

    @Column(name = "second_number")
    private int secondNum;

    @Column(name = "result")
    private int result;

    public DatabaseRes(int firstNum, String action, int secondNum, int result) {
        this.firstNum = firstNum;
        this.action = action;
        this.secondNum = secondNum;
        this.result = result;
    }
}

```

<br>Код репозитория<br>

```
package ru.neoflex.practice.repository;

import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.data.jpa.repository.Query;
import org.springframework.stereotype.Repository;
import ru.neoflex.practice.database.DatabaseRes;

import java.util.List;

@Repository
public interface RepositoryRes extends JpaRepository<DatabaseRes, Integer> {
    @Query("Select db from DatabaseRes db")
    List<DatabaseRes> findAllRes();
}

```

<br>Изменнёный код контроллера<br>

```
package ru.neoflex.practice.controller;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RestController;
import ru.neoflex.practice.database.DatabaseRes;
import ru.neoflex.practice.repository.RepositoryRes;

import java.util.List;

@RestController
public class CalcController {

    @Autowired
    public RepositoryRes repositoryRes;

    @GetMapping("/plus/{a}/{b}")
    public Integer sum(@PathVariable("a") Integer a, @PathVariable("b") Integer b) {
        repositoryRes.save(new DatabaseRes(a, "+", b, a + b));
        return a + b;
    }

    @GetMapping("/minus/{a}/{b}")
    public Integer min(@PathVariable("a") Integer a, @PathVariable("b") Integer b) {
        repositoryRes.save(new DatabaseRes(a, "-", b, a - b));
        return a - b;
    }

    @GetMapping("/TableAll")
    public List<DatabaseRes> getAllRes() {
        return repositoryRes.findAllRes();
    }
}

```

<br>Результат без записей<br>
   ![testdb](https://github.com/VeithVanJ/NeoflexCalcPractice/blob/main/screenshot/img9.png)<br>
Результат с записями<br>
  ![resultdb](https://github.com/VeithVanJ/NeoflexCalcPractice/blob/main/screenshot/img10.png)<br>
  ![resultdb1](https://github.com/VeithVanJ/NeoflexCalcPractice/blob/main/screenshot/img11.png)
  
## _*Реализация GET-запроса*_ 
<br>Переходим по ссылке http://localhost:8080/h2-console и вводим данные из application.properties<br>
  ![result](https://github.com/VeithVanJ/NeoflexCalcPractice/blob/main/screenshot/img12.png)<br>
Выполняем Get-запрос<br>
  ![registr](https://github.com/VeithVanJ/NeoflexCalcPractice/blob/main/screenshot/img13.png)<br>
Выполнила: Виноградова Софья Матвеевна
