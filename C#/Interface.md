# 인터페이스
## 추상 클래스

추상 클래스는 말 그대로 어떠한 형태가 없는 추상적인 클래스이다. </br>
추상 클래스는 다음과 같은 특징이 있다.
- new로 생성할 수 없다. 
- 추상 함수를 가질 수 있다.
</br>
</br>
</br>

## abstract vs virtual 
추상 함수는 가상 함수와 달리 자식에서 반드시 재정의 해줘야 한다. </br>
그리고 추상 함수는 가상 함수와 달리 구현부를 가질 수 없다.
</br>
</br>
</br>

## 다중 상속 
여러개의 추상 클래스를 상속 받고 싶은 경우도 있을 것이다. </br>
문제는 C#에서는 다중 상속을 금지한다. (다이아몬드 상속을 방지하기 위함) </br>

다이아몬드 상속의 예시를 살펴보자.

```c#
abstract class Player
{
    public abstract void Attack();
}

class Swordsman : Player
{
    public override void Attack()
    {
        Console.WriteLine("물리 공격");
    }
}

class Magician : Player
{
    public override void Attack()
    {
        Console.WriteLine("마법 공격");
    }
}

class MagicSwordsman : Swordsman, Magician
{

}
```
만약 위와 같은 상속을 허용한다면 MagicSwordsman의 Attack()을 호출했을 때 어떤 Attack()을 호출해야 되는지 알 수 없게 된다.
</br>
</br>
</br>

## 인터페이스
인터페이스는 추상 함수만을 가지는 클래스이다. </br>
인터페이스는 멤버 함수의 정의만을 갖고, 구현은 인터페이스를 상속 받는 쪽에서 한다.

만약 다중 상속을 원한다면 클래스를 상속 받는 방식이 아닌, 인터페이스를 상속 받는 방식을 사용해야 한다. </br>
```c#
interface IFlyable
{
    void Fly();
}

abstract class Player
{
    public abstract void Attack();
}

class FlyableKnight : Player, IFlyable
{
    public override void Attack()
    {
        Console.WriteLine("물리 공격");
    }

    public void Fly()
    {
        Console.WriteLine("비행");
    }
}
```

인터페이스는 구현이 아닌 외형(인터페이스)만을 물려주기 때문에 다중 상속을 받더라도 같은 함수가 다른 구현부를 가지고 있어서 발생하는 모호성 문제는 발생하지 않는다.





