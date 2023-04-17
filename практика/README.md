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

Диаграмма классов:
```
@startuml
package "Программное обеспечение банкомата" {
  class Bankomat {
    -cardReader: CardReader
    -bankServer: BankServer
    -cashDispenser: CashDispenser
    -display: Display
    -keypad: Keypad
    +insertCard()
    +enterPin()
    +selectTransaction()
    +dispenseCash()
    +printReceipt()
    +showBalance()
  }

  interface CardReader {
    +readCardData(): CardData
  }

  interface BankServer {
    +verifyPin(pin: int): boolean
    +getBalance(cardData: CardData): float
    +dispenseCash(amount: float): boolean
  }

  interface CashDispenser {
    +dispenseCash(amount: float): boolean
  }

  class Display {
    +showMessage(message: String)
  }

  class Keypad {
    +getInput(): String
  }

  class CardData {
    -cardNumber: String
    -expirationDate: Date
    -cvv: String
    +getCardNumber(): String
    +getExpirationDate(): Date
    +getCvv(): String
  }

  CardReader --> CardData
  Bankomat --> CardReader
  Bankomat --> BankServer
  Bankomat --> CashDispenser
  Bankomat --> Display
  Bankomat --> Keypad
}
@enduml
```
Диаграмма последовательности для снятия наличных:
```
@startuml
actor Пользователь as user
participant "Банкомат" as bankomat
participant "Банковский сервер" as bankserver
participant "Кассета с наличными" as cashdispenser
participant "Дисплей" as display
participant "Клавиатура" as keypad

user -> bankomat: Вставить карту
bankomat -> cardreader: Прочитать данные карты
cardreader -> bankomat: Карта прочитана
user -> bankomat: Ввести ПИН-код
bankomat -> bankserver: Проверить ПИН-код
bankserver -> bankomat: ПИН-код верен
user -> bankomat: Выбрать снятие наличных
bankomat -> display: Показать меню
user -> keypad: Ввести сумму для снятия
keypad -> bankomat: Сумма введена
bankomat -> bankserver: Запросить снятие указанной суммы
bankserver ->
```
