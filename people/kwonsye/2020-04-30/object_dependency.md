## 의존성 관리하기

- 변경과 의존성
    - 어떤 객체가 협력하기 위해 다른 객체를 필요로 할때 두 객체 간 **의존성**이 생김
    - 의존성은 단방향
    - 의존되는 요소가 변경될 때, 의존하는 요소도 함께 변경될 수 있음
    - 의존성은 변경에 의한 영향의 전파 가능성
    - 의존하고 있는 대상의 변경에 영향을 받을 수 있는 가능성

    - 의존성 전이
        - A가 B에 의존할 경우, A는 B가 의존하는 대상에 대해서도 자동적으로 의존하게 된다.
        - 의존성이 실제로 전이될지 여부는 **변경의 방향과 캡슐화 정도**에 따라 달라짐

    - 런타임 의존성 vs 컴파일 의존성
        - 런타임 의존성
            - 객체 사이의 의존성
        - 컴파일 의존성
            - 클래스 사이의 의존성
        - 유연하고 재사용가능한 설계를 만들기 위해서는 동일한 코드를 가지고 다양한 실행구조를 만들 수 있어야한다.
        - 실제로 협력할 객체는 런타임에 알게 설계해라
        - 런타임 의존성과 컴파일타임 의존성 사이의 거리가 멀수록 설계가 유연해짐
        - 컴파일 타임 의존성을 어떤 런타임 의존성으로 대체하느냐에 따라 달라진다.

    - 컨텍스트 독립성
        - 실행될 컨텍스트에 대한 구체적인 정보를 최대한 적게 알아야함 = 컨텍스트 독립적이어야함
        - 컨텍스트 독립적이라면 변경하기 쉬워짐

    - 의존성 해결하기
        - 컴파일 타임 의존성은 실행 컨텍스트에 맞는 런타임 의존성으로 대체돼야함 = 의존성 해결
        1. 객체를 생성하는 시점에서 생성자를 통해 의존성 해결
        2. 객체 생성 후 setter 메소드로 의존성 해결
            - 객체 생성 이후에도 의존 대상을 변경할 수 있는 가능성을 열어놓고 싶은 경우 유용
        3. 메서드 실행 시 인자를 이용해 의존성 해결

- 유연한 설계
    - 의존성이 나쁜게 아님. 협력을 위해서는 꼭 필요하다
    - 의존성을 바람직하게 만드는게 중요
    - 컨텍스트 독립적인 의존성은 바람직한 의존성
    - 바람직한 의존성은 **재사용성**이 높은 의존성
    - 다른 환경에서 재사용하기 위해 **내부 구현을 바꿔야하는** 의존성은 바람직하지 않은 의존성
    - 의존성이 바람직할 때
        - 느슨한 결합도 & 약한 결합도 
    - 의존성이 바람직하지 못할 때
        - 단단한 결합도 & 강한 결합도
    - 결합도의 정도는 한 요소가 자신이 의존하고 있는 다른 요소에 대해 알고 있는 **정보의 양=지식의 양**으로 결정됨
        - 많은 정보를 알고 있을수록 두 요소는 강하게 결합됨
        - 적은 정보를 알고 있을수록 약하게 결합됨=느슨한 결합도
        - 느슨한 결합도를 위해서는 협력대상에 대해 필요한 정보 외에는 최대한 감춰라
        - 그 방법은? **추상화**
    - **추상화에 의존하라**
        - 추상화란 세부사항,구조,양상을 명확하게 이해하기 위해서 불필요한 정보를 **감춤으로써 복잡도를 극복**하는 방법
        - **의존하는 대상이 더 추상적일수록 결합도는 더 낮아짐**
        - 아래 쪽으로 의존할수록 느슨한 결합도
            - 구체 클래스 의존성
            - 추상 클래스 의존성
            - 인터페이스 의존성
        - 실행 컨텍스트에 대해 알아야하는 정보를 줄일수록 결합도가 낮아진다.
    - 명시적인 의존성
        - 의존성은 명시적으로 **퍼블릭 인터페이스**에 노출됨 = 명시적인 의존성<-> 숨겨진 의존성
        - 의존성은 **퍼블릭 인터페이스에 명시적으로 표현**돼야한다.
        - 의존성을 구현 내부에 숨기지마라
        
        - 의존성이 명시적이지 않으면 의존성을 파악하기 위해 내부구현을 봐야함
        
    - new 는 해롭다
        - new는 결합도를 높이기 때문에 해로움
        - new를 사용하면 구체클래스 이름+인자를 직접 기술해야함
        - new는 구체클래스를 생성하는 데 어떤 정보가 필요한지 알아야함
        - 해결방법
            - 인스턴스를 생성하는 로직과 생성된 인스턴스를 사용하는 로직을 분리해라
            - 생성자 이용, setter 이용, 메소드의 인자 이용해서 인스턴스를 전달만 받는다.
            - 객체를 생성하는 책임을 클라이언트에게 옮겨라
    
    - 사용성이 향상될 수 있다면 생성자 체이닝 기법 or 오버로딩을 통해 인스턴스를 생성해도 괜찮다.

    - 표준 클래스에 대한 의존은 해롭지 않다.
        - 표준 클래스(JDK에 포함된 클래스)는 변경 확률이 없으므로 의존성이 문제되지 않음 -> 인스턴스를 직접 생성해도 ok

    - 컨텍스트 확장하기
        - 코드 내부를 직접 수정하는 것은 버그 가능성을 높임
        - **추상화된 클래스의 구체 클래스를 추가함**으로써 컨텍스트를 확장할 수 있음
        - 결합도를 낮춤으로서 컨텍스트 확장이 쉬워짐
        - 객체가 how 하는지 장황하게 나열x
        - 객체가 what을 하는지 표현하는 클래스들로 구성되어야 유연한 설계
        - 유연한 설계는 **객체들의 조합을 선언적으로 표현**함으로써 객체들이 what을 하는지 표현하는 설계
        - 코드에 드러난 로직을 해석할 필요없이 **객체가 어떤 객체와 연결되었는지 보는 것**만으로 객체의 행동을 **쉽게 예상**할 수 있어야함
        - 유연한 설계는 작은 객체의 행동을 조합함으로써 새로운 행동을 이끌어낼 수 있는 설계임
        - **방법이 아니라 목적**에 집중할 수 있는 설계가 변경에 유연하다.
        

<br>

## 참고 도서
---
오브젝트-코드로 이해하는 객체지향 설계 **8장 의존성 관리하기**