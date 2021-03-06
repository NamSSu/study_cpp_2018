# 01. C++에 오신것을 환영합니다.

    2018-11-05 : initial commit

### 1.1 C++의 시작

C++은 C를 계승하는 언어입니다. 비야네 스트롭스트룹이 만들었으며, 아래와 같은 항목에 목적을 두고 만들었습니다.

* C언어와의 호환성
* 객체 지향 개념 도입
    * 캡슐화
    * 상속
    * 다형성
* 재사용성 개념 도입으로 생산성 향상
* 엄걱한 debug & runtime 체크
    * 디버깅의 편리
* 컴파일러의 개선
    * 실행 시간 효율성 개선
        * ex) 함수의 잦은 호출 -> 인라인 함수로 개선

또한 아래와 같은 굵직한 기능이 추가되었습니다.

* 함수 중복(function overloading)
* 기본 파라미터(default parameter)
* 참조(reference)
* 참조에 의한 호출(call_by_reference)
* 제네릭 함수 및 클래스 (데이터 타입 의존성을 해결하기 위한 일반화 타입)
* 연산자 재정의 (new/delete 연산자)

여기서 가장 중요하게 여겨지는 것은, 객체지향 / 제네릭 함수 / 참조에 의한 호출입니다. 참조에 의한 호출은 나중에 다루도록 하고, 먼저 이 2가지를 다루도록 하겠습니다.

##### 1.1.1 객체 지향

객체를 지향한다니, 말이 너무 이상하다고 생각할 수도 있습니다. 하지만 찬찬히 생각하면 그럴 만한 이유에서 나온 말입니다.

C언어를 머리속에서 떠올려 보면, 모든 항목이 __절차지향적__ 인것을 알 수 있습니다. (main 함수에서 벗어나도, 결국에는 main함수에 선언을 하게 해야하니까요.) 이는 곧 __기능__ 만 관심이 있지, __안의 구조가 어떻고 데이터를 어떻게 취급하는지는 관심이 없었습니다.__

이 때문에 많은 차기 프로그래밍 언어에서 문제점이 나오게 되어서, 하나의 방법론으로 이 객체 지향, __수많은 "객체"로 나누어서 서로 상호작용하게 만드는 것이__ 바로 객체지향입니다.

한줄로 요약하면, __프로그램을 수많은 객체로 나누어서 이 객체들의 상호작용으로 작동하게 하는 방법입니다.__

##### 1.1.2 객체 지향의 3개념

객체 지향은 3개념으로 이루어져 있습니다. __캡슐화, 상속, 다형성__ 입니다. 

* 캡술화
    * 캡슐화는 프로그램의 세부 구현을 외부에 보이지 않게 클레스로 감추는 것을 의미합니다.
    * 이는 곧 어떻게 처리과정이 이루어 지는지는 알지 못하게 설계하는 것입니다(정보 은닉)
    * 보통 3종류의 접근 레벨이 있습니다.
        * __public__
            * 모두가 접근 가능하며, 모두에게 노출됩니다.
        * __protected__
            * 일반적으로는 노출이 되지 않지만, 상속이 된 자식 클레스에서 노출되며 접근이 가능합니다.
        * __private__
            * 선언한 클래스 내부에서만 사용 가능하며, 그 이외 모두가 접근과 노출이 되지 않습니다.

* 상속
    * 상속은 __자식 클래스가 부모 클래스의 특성과 기능을 물려 받는것__ 을 의미합니다. 
    * 똑같은 기능을 쓰지만 값이 다르거나 약간의 수정이 필요할 경우 __물려받아 재 정의를 하게 되는데, 이를 재정의(overriding)__ 이라 합니다.
    * 하지만 이는 __정보 은닉(캡슐화) 에 약간 반하는 성격__ 을 지니게 됩니다.
    * 또한 이는 __동적 유연성 (자식이 부모를 마음대로 바꿀 수 없다) 이 떨어지게 됩니다.__
    * 결론적으로, 개발자가 엉뚱하게 상속할 경우 문제를 잡기 어렵습니다.

* 다형성
    * 하나의 변수명이 상황에 따라서 다른 의미로 해석될 수 있는것을 말합니다.
    * 이를 __중복 정의(overloading)__ 라고 합니다.
    * C++은 연산자와 함수가 오버로딩이 가능합니다.

##### 1.1.3 제네릭 함수

제네릭 함수란 __사용자가 전달하는 형식을 매개 변수로 사용하여,__ 내부에서 정의된 형식을 변형하는 것을 말합니다.

* 이는 곧 유연하게 형식을 바꿀 수 있는 유연성이 제공됩니다.

### 1.2 Hello, world!

아래와 같이 코드를 작성하면, 처음 C++를 짜게 됩니다.

```cpp
#include <iostream>

using namespace std;

int main(void){
    cout << "hello, world!" << endl;
}
```
* ... 위와 같은 코드, 쓰긴했지만 이해는 못하실 수도 있습니다. 차근차근 알아보도록 합시다.

#### 1.2.1 hello, world 해석

* __iostream__ 은 input/output stream 으로 표준 입/출력 을 의미합니다.
* __using namespace std__ 는 namespace(이름 공간)을 standard iostream 을 이용하겠다는 말입니다. 결국 해석하면 표준 C++ stream 을 이용하겠다는 말입니다.
이를 통해서 std:: 와 같은 표준 스트림을 생략 할 수 있습니다.
* __cout__ 은 console output의 약자로, 표준 출력 함수입니다. 
* __<<__ 는 스트림 삽입 연산자 입니다. <<는 우->좌 로 삽입합니다. 

#### 1.2.2 namespace(이름 공간)

* __이름 공간__ 이란 공간을 선언함으로써, 다른 이름공간과 별도 구분이 가능하게 할 수 있다.

* 아래와 같이 생성 할 수 있다.
```cpp
namespace name {
    int fuction() {
        ...
    }
    ...
}
```
* 아래와 같이 사용 할 수 있다.
```cpp
int main(void) {
    name::function();
    ...
}
```

#### 1.2.3 입력과 출력, cin & cout

* cout은 console output의 약자로, 표준 출력 함수입니다.
* 아래와 같이 사용됩니다.
```cpp
int main(void) {
    cout << ... << endl; // endl은 end line 의 줄임말입니다.
}
```
* cin 은 console input의 약자로, 표준 입력 함수입니다.
* 입력 버퍼가 있어서 Enter키가 입력될때 까지 버퍼링합니다.
* 아래와 같이 사용됩니다.
```cpp
int main(void) {
    cin >> ...;
}
```
##### 1.2.3.1 스트림 연산자
* '<<'는 스트림 삽입 연산자로, 우->좌 로 삽입합니다.
* '>>'는 스트림 추출 연산자로, 좌->우로 값을 읽어서 삽입합니다.

### 1.3 C++의 문자열

* 문자열을 입력받는 방법이 C++에서는 2가지 입니다. C-string과 cin.getline() 으로 받는 방법입니다.

#### 1.3.1 C-string으로 입력 받기

* C-string으로 입력 받는것은 C와 비슷합니다. \0으로 끝나는 문자 배열을 C-string방식이라고 합니다.
```cpp
char name1[5] = { 'N', 'a', 'm', 'e', '\0' }; // 문자열
char name2[4] = { 'N', 'a', 'm', 'e' }; // 단순 문자 배열
```

* C-string은 문자열을 C언어에서 썼던 함수를 사용가능합니다. 
* 사용하기 위해서는 <cstring.h> 라는 헤더 파일을 추가해줘야 합니다.
* 입력을 받을때는 빈칸이 없이 입력을 해야합니다.

#### 1.3.2 cin.getline()으로 입력 받기

* 공백이 있는 문자를 받을 수 있으며, Enter키를 입력받으면 다음 줄로 넘어갑니다.
* 아래와 같이 사용합니다.
```cpp
cin.getline(var, input_size, '\n'); // var은 입력받을 변수이며, input_size는 입력받을 개수를 말한다. \n은 입력 안해도 된다.
```

#### + 1.3.3 getline()으로 입력 받기

* 위의 cin.getline() 과 다른점은, 저 함수는 iostream 에 소속된 함수이고, 이 함수는 string 클레스에 소속된 함수이다.
* 장점은 문자열 크기에 따른 제약 없음, 다양한 함수 및 연산자 제공 입니다.
* 사용하기 위해선 <string>을 선언해줘야 합니다.
* 아래와 같이 사용합니다.
```cpp
#include <string>

using namespace std;
...
getline(cin, var, input_method)l // 첫번째는 입력을 불러올 곳이며, 두번째는 입력받을 변수이며, 세번째는 어떤 글자가 들어올시 다음 줄로 넘어갈지 결정한다.
```

### 1.4 헤더 파일

* 헤더 파일은 기본적인 내용(원형) 이 선언된 파일이다.
* 이를 사용하면 불러온 함수의 코드가 출력 파일에 들어가게 된다.
* 사용하는 이유는 호출 구문이 정확한지 컴파일러가 판단하기 위해서이다.