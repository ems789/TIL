# delegate (대리자)
델리게이트는 함수를 가리킬 수 있는 타입이다. (함수 포인터와 비슷한 개념)
```c#
delegate int OnClikced();
```
대리자라는 뜻에서도 알 수 있듯이 함수 호출을 다이렉트로 요청하지 않고 (함수 내부에 들어가서 직접 호출),
대리자를 통해서 나중에 실행할 함수를 넘겨주는 개념이라고 볼 수 있다. 
</br>
</br>
왜 번거롭게 대리자를 통해서 함수를 넘겨줘야 할까?
1. 관리차원의 문제.</br>
   예를 들면 UI 함수 안에 게임 로직을 그대로 넣으면 UI 처리 로직과 게임 로직이 섞이게 되는 문제가 발생한다. 이 둘을 분리하는게 관리 차원에서 좋다.

2. 라이브러리처럼 내부 코드를 수정할 수 없는 경우.</br>
   이 경우에는 어쩔 수 없이 델리게이트를 넘겨줘야 한다.

3. 함수를 다양한 방식으로 동작하고 싶은 경우</br>
   예를 들면 정렬 함수에 대리자를 넘겨줌으로써 경우에 따라 오름차순 혹은 내림차순으로 실행되게 할 수 있다. 
</br>
</br>
</br>

## 델리게이트 체인
델리게이트 체인은 하나의 델리게이트 안에 여러개의 함수를 연결하여 연쇄적으로 호출하는 방식이다.
```c#
delegate int OnClikced();

static void ButtonPressed(OnClicked clikcedFuncton)
{
    clikcedFunction();
}

static int Delegate1()
{
    Console.WirteLine("Delegate 1");
    return 0;
}

static int Delegate2()
{
    Console.WirteLine("Delegate 2");
    return 0;
}

static void Main(string[] args)
{
    OnClikced clicked = new Onclicked(Delegate1);
    clicked += Delegate2;

    ButtonPressed(clicked);
}

```