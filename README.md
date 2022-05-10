# Задача "Исследование JVM через visualVM"

## Описание

Предлагаем вам изучить использование памяти через VisualVM при загрузке новых классов и создании новых объектов Описание и инструкция к выполнению выше.

## Результат исследования
### Сведения из консоли

Gradle Daemon started in 6 s 481 ms  
> Task :compileJava  
> Task :processResources NO-SOURCE  
> Task :classes  
> 
> > Task :JvmExperience.main()   
Please open 'ru.netology.JvmExperience' in VisualVm  
15:29:24.023632: loading io.vertx  
15:29:24.779071600: loaded 529 classes  

В момент начала работы программы подсистема загрузчиков классов ClassLoader выделяет память в metaspace для информации о константах,полях, методах и имени класса.  
Загрузка классов из пакета io.vertx, рост metaspace, загружено 529 классов:
![image](https://user-images.githubusercontent.com/100822694/167636956-54a0f242-c930-46ba-ad28-4e278a79b56f.png)
И в это время растет использованная память в metaspace:
![image](https://user-images.githubusercontent.com/100822694/167637834-206affe8-cfef-41a8-9c25-0545a9cec18a.png)

15:29:27.791230300: loading io.netty  
15:29:29.237702700: loaded 2117 classes  
Загрузка классов из пакета io.netty, рост metaspace, загружено 2117 классов:
![image](https://user-images.githubusercontent.com/100822694/167640124-a6f872e6-0317-400d-b058-083c6888ef48.png)
![image](https://user-images.githubusercontent.com/115:29:32.244453700: loading org.springframework00822694/167640307-d79a78d4-0df2-475f-89bf-d08708441d88.png)
![image](https://user-images.githubusercontent.com/100822694/167640640-4a878e77-00f7-48c9-81bc-94ba9cf62dbc.png)

15:29:32.244453700: loading org.springframework  
15:29:32.806137100: loaded 869 classes  

При запуске spring количество классов возросло:
![image](https://user-images.githubusercontent.com/100822694/167641272-ce6d696d-424f-403f-ba51-7bf53a1b96fa.png)

15:29:35.816352300: now see heap  
15:29:35.817353: creating 5.000.000 objects  
15:29:36.395394: created  
Резкий рост памяти в metaspace при создании 5 млн. объектов:
![image](https://user-images.githubusercontent.com/100822694/167644555-2710fec1-3049-4789-81ee-c694cba6ba6d.png)

![image](https://user-images.githubusercontent.com/100822694/167645766-d3cb27cc-4d6a-43f7-a875-dca3708ace5f.png)


15:29:39.409100100: creating 5000000 objects  
15:29:40.046876800: created  
15:29:43.249194100: creating 5000000 objects  
15:29:43.625196: created  
Еще дополнительно 5 млн объектов создано и последний пик в heap появился:  
![image](https://user-images.githubusercontent.com/100822694/167646333-1a2cf584-7ecc-4345-abde-e466bab5cc54.png)


BUILD SUCCESSFUL in 1m 25s  
2 actionable tasks: 2 executed  
15:29:50: Execution finished ':JvmExperience.main()'.  
Программа завершена

 



