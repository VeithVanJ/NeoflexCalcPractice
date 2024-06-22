# NeoflexCalcPractice
## _*Создание контроллера*_
<br>
  В папке src/main/java/ru/neoflex/practice создаём папку controller. <br>
  В ней (/controller) создаём файл CalcController.java <br>
  Над классом указываем аннотацию @RestController <br>
  Создаём 2 public метода с аннотациями @GetMapping("/plus/{a}/{b}")  и @GetMapping("/minus/{a}/{b}"), которые принимают 2 аргумента, типа Integer, а возвращают их сумму/разность соответственно. Перед каждым аргументом метода необходимо поставить @PathVariable("a или b соответственно для каждого аргумента") <br>
  
