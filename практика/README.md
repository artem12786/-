Диаграмма вариантов использования
```
@startuml
left to right direction
skinparam packageStyle rect

actor Пользователь as user

rectangle "Программное обеспечение банкомата" {
  usecase "Снятие наличных" as withdraw
  usecase "Печать справки об остатке на счете" as print
}

user --> withdraw
user --> print
@enduml
```

