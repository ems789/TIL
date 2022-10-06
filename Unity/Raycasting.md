# Raycasting
레이캐스팅은 광선을 쏴서 광선에 닿은 물체가 있는지 판별하는 기술이다.

유니티에서는 3D 공간에 있는 물체를 마우스로 클릭해서 선택할 수 있다. </br>
마우스가 클릭한 좌표는 2D 좌표인데 어떻게 그게 가능한걸까? </br>
레이캐스팅을 사용해서 이를 구현할 수 있다. 

이 과정을 이해하기 위해서는 먼저 투영에 대해서 알아야 한다.
</br>
</br>
</br>
## 투영
3차원 공간을 2차원 공간으로 표현하는 것을 투영이라고 한다.
이런 과정이 필요한 이유는 3차원 공간을 출력하는 매체인 모니터가 2D 화면이기 때문이다. 

3D 물체는 아래의 과정을 거쳐서 2D 화면으로 옮겨진다. </br>
Local -> World -> Viewport -> Screen (윈도우 화면)

그럼 스크린 좌표에서 이 변환 과정을 역으로 수행한다면 월드에 있는 물체들과 상호작용 할 수 있을 것이다.
</br>
</br>
</br>
## 레이캐스팅
아래의 과정을 통해서 월드에 있는 물체를 얻어올 수 있다. </br>
1. 마우스로 클릭한 2D 좌표를 z값을 갖는 월드 좌표로 변환한다. </br>
z값은 임의의 깊이를 넣어주면 된다. 카메라에서 월드 좌표로 향하는 방향만 알 수 있으면 되기 때문.

2. 카메라에서 해당 좌표로 광선을 쏘면 목표물을 얻어올 수 있다. </br>


```c#
Vector3 mousePos = Camera.main.ScreenToWorldPoint(new Vector3(Input.mousePosition.x, Input.mousePosition.y, 0.01f)); // 마우스의 위치에 임의의 z값을 넣어 월드 좌표를 얻어냄

Vector3 dir = mousePos - Camera.main.transform.position; 
// 카메라 -> 월드 좌표의 방향을 구함
dir = dir.normalized;

// Debug.DrawRay(Camera.main.transform.position, dir * 100, Color.red);
RaycastHit hit;
if (Physics.Raycast(Camera.main.transform.position, dir, out hit, 100)) // 레이캐스트
{
    Debug.Log($"Raycast, hit : {hit.collider.gameObject.name}");
}
```

