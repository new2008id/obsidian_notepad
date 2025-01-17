
`Наследование в Java` — это механизм, позволяющий создавать новые классы (подклассы или производные классы) на основе существующих (суперклассы или базовые классы). 

Подкласс наследует все поля и методы суперкласса, за исключением конструкторов (хотя подкласс может вызывать конструкторы суперкласса).

### Основные понятия

- **Суперкласс (базовый класс):** Класс, от которого происходит наследование.
- **Подкласс (производный класс):** Класс, который наследует от суперкласса.
- **extends:** Ключевое слово, используемое для объявления наследования. `class Подкласс extends Суперкласс { ... }`
- **Полиморфизм:** Способность объектов разных классов реагировать на один и тот же вызов метода по-разному. Наследование помогает реализовать полиморфизм.
- **Переопределение методов:** Подкласс может переопределить (override) методы суперкласса, предоставляя свою реализацию.

## Пример использования наследования

```java
public class CatFamily {   // родительский класс
    protected int legs;  
    protected int eyes;  
    protected boolean canEatPerson;  
  
    public CatFamily(int legs, int eyes, boolean canEatPerson) {  
        this.legs = legs;  
        this.eyes = eyes;  
        this.canEatPerson = canEatPerson;  
    }  
  
    public int getLegs() {  
        return legs;  
    }  
  
    public int getEyes() {  
        return eyes;  
    }  
  
    public boolean isCanEatPerson() {  
        return canEatPerson;  
    }  
  
    public void setLegs(int legs) {  
        this.legs = legs;  
    }  
  
    public void setEyes(int eyes) {  
        this.eyes = eyes;  
    }  
  
    public void setCanEatPerson(boolean canEatPerson) {  
        this.canEatPerson = canEatPerson;  
    }  
}
```

#### Классы наследники

```java
public class Cat extends CatFamily {  
  
    public Cat() {  
        super(4, 2, false);  
        legs = 5;  
    }  
}

public class Lion extends CatFamily {  
    public Lion() {  
        super(4, 2, true);  
    }  
}
```

[[Модификатор доступа - Protected]]