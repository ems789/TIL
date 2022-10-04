# event

event는 특수한 형태의 델리게이트이다. </br>
델리게이트는 외부에서도 호출 가능하기 때문에 안정성이 떨어진다. 그래서 이벤트라는 것을 사용한다.

이벤트는 클래스내에 특정한 일(event)이 일어났음을 외부의 이벤트 구독자(subscriber)들에게 알려주는 기능을 한다.

이벤트에 가입하는 외부 가입자 측에서는 이벤트가 발생했을 때 어떤 명령을 실행할 지를 지정해주는데, 이를 **이벤트 핸들러**라 한다. 이벤트에 가입하기 위해서는 += 연산자를 사용하여 이벤트 핸들러에 이벤트를 추가한다. </br>
(외부에서 구독 신청, 해제는 가능하지만 직접 이벤트를 호출하는 것은 불가능)

```c#
using System;

// 옵저버 패턴
class InputManager
{
    public delegate void OnInputKey();
    public event OnInputKey InputKey;

    public void Update()
    {
        if (Console.KeyAvailable == false)
            return;

        ConsoleKeyInfo info = Console.ReadKey();
        if (info.Key == ConsoleKey.A)
        {
            // 모두에게 알려준다
            InputKey();
        }
    }
}

class Program
{  
    static void PrintMessage()
    {
        Console.WriteLine("Print");
    }

    static void Main(string[] args)
    {
        InputManager inputManager = new InputManager();
        inputManager.InputKey += PrintMessage;          

        while(true)
        {
            inputManager.Update();
        }
    }
}

```