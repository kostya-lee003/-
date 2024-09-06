## Задачка №1
Сделать кастомный NotificationCenter.
```
class NotificationCenter {
  typealias ClassName = String
  typealias NotificationName = String
  typealias NotificationClosure = (String, Any) -> Void

  static let shared = NotificationCenter()
  private init() {
    notificationsStorage = [:]
  }

  private var notificationsStorage: [ClassName: [NotificationName: [NotificationClosure]]]

  func addObserver(_ _class: Any, name: NotificationName, closure: @escaping NotificationClosure) {
    guard let inputClass = type(of: _class) as? AnyClass else {
       return
    }
    let className = String(describing: inputClass)
    if notificationsStorage[className] != nil && notificationsStorage[className]?[name] != nil {
        notificationsStorage[className]?[name]?.append(closure)
    } else {
        notificationsStorage[className] = [name: [closure]]
    }
  }

  func removeObserver(_ _class: Any) {
    guard let inputClass = type(of: _class) as? AnyClass else {
      return
    }
    let className = String(describing: inputClass)
    guard notificationsStorage[className] != nil else {
      print("Notification not found")
      return
    }
    notificationsStorage.removeValue(forKey: className)
  }

  func postNotification(_ name: NotificationName, object: Any) {
      for (_, notificationData) in notificationsStorage {
          for (notificationName, closures) in notificationData {
              guard notificationName == name else { continue }
              for closure in closures {
                  closure(name, object)
              }
          }
      }
  }
}
```

## Задачка №2
Спроектировать логику тикток скролла: Есть дизайн, есть документация по запросам, есть техническое задание. Моменты пронумерованные по важности
1) Общение между компонентами в архитектуре MV_X_
2) Оптимизировать логику запросов. Сделать максимально быстрый респонс для юзера и минимальную нагрузку на бэк.
3) Реализовать логику скролла, обработку нажатий
