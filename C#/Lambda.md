# Lambda (람다식)
람다식은 접근자, 함수 이름, return문 없이 간편하게 만들 수 있는 익명 함수이다.

람다식은 일회성 함수를 만들어 함수의 인자로 넘겨줄 때 유용하다. </br>
익명 함수를 사용하지 않는 경우 함수를 미리 만들어두고 인자로 넘겨야 한다.
```c#
// 함수를 미리 만들어둠
static void PrintMessage()
{
    Console.WriteLine("Print");
}

delegate void Test();

static void ButtonPressed(Test printFunc)
{
    ConsoleKeyInfo info = Console.ReadKey();
    if (info.Key == ConsoleKey.A)
    {
        printFunc();
    }
}

static void Main(string[] args)
{
    while (true)
    {
        ButtonPressed(PrintMessage);
    }
}
```
</br>
</br>
익명 함수를 사용하면 인자를 넘기는 부분에서 함수를 정의할 수 있다. </br>
우선 람다식을 살펴보기 앞서 delegate로 익명 함수를 넘기는 방법을 알아보자.

```C#
static void Main(string[] args)
{
    while (true)
    {
        ButtonPressed(delegate () { Console.WriteLine("Print"); });
    }
}
```
</br>
</br>
이를 더 간단하게 delegate까지 생략된 형태로 익명 함수를 표현하는 것이 람다식이다.

```c#
static void Main(string[] args)
{
    while (true)
    {
        ButtonPressed(() => { Console.WriteLine("Print"); });
    }
}
```
</br>

---
## Func, Action
Func, Action은 C#에서 제공하는 제네릭으로 정의된 델리게이트이다. </br>
Func는 반환 타입이 있는 델리게이트이고, Action은 반환 타입이 없는 델리게이트이다. 

델리게이트를 직접 선언하지 않고 Func, Action을 사용하면 편하다. </br>

