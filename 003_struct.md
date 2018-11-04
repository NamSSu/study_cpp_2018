# 다함께 묶어봅시다, 구조체

    2018-11-04 : initial commit

### 1.1 구조체의 개념

구조체(Structure)란 여러가지 자료형이 섞인 변수를 하나로 묶어서 그걸 자료형으로 활용할 수 있도록 정의한 것을 뜻한다. 

쉽게 설명하자면, 다양한 상품이 있는 마트를 하나 만드는 것과 비슷하다고 생각하면 된다. __(마트 == 구조체 , 상품 == 멤버)__

예를 하나 들어보겠습니다.

* 통장을 만든다고 가정하면,
    * 이름
    * 통장번호
    * 통장 잔액
    
    위의 3가지의 기본적인 정보가 필요할 것입니다.

    * 이를 간단하게 변수로만 코딩해본다면,

         ```c
        #include <stdio.h>
    
        int main(void) {
            char name[20];
            char bank_num[16];
            double present_bank_amount;

            ...
            ...
        }
        ```

    * 아마 위와 같이 하면 사람이 늘어날수록 비슷한 내용을 가진 변수를 몇백개, 몇천개를 생성해야 할겁니다. 

* 이러한 __공통되게 쓰이는 데이터 집합을 묶은 것__ 이 바로 구조체입니다.

    * 위를 다시 구조체로 간단하게 코딩해본다면,

    ```c
    #include <stdio.h>

    struct banking { // 여러가지 타입의 자료형을 묶음
        char name[20];
        char bank_num[16];
        double present_bank_amount;
    };

    int main(void) {
        struct banking user_1;

        ...
        ...
    }
    ```
    * 이와 같이 공통된 정보를 불러올 수 있습니다.

### 1.2 구조체를 기본 형태

* 구조체는 __정의__ 와 __변수 선언__ 이 필수적으로 필요합니다.
    * __정의__ 는 안에 들어갈 내용을 선언하며, 아래와 같은 형태로 정의합니다.
        ```c
        struct structure_name {
            int var1; //구조체 멤버1
            char var2; // 구조체 멤버2
            ...
        };
        ```
    * __변수 선언은__ 사용해야하는 곳에서 정의를 불러오기 위해서 선언하며, 아래와 같은 형태로 변수를 선언합니다.
        ```c
        int main(void) {
            struct structure_name var;
            ...
        }
        ```
    * 또한 __정의__ 하면서 __변수 선언__ 을 하는 것도 아래와 같은 형태로 가능합니다.
        ```c
        struct structure_name {
            int var1;
            char var2;
        }def_var1, def_var2; //별칭이라 생각하면 편하다.
        ```
    * 구조체의 __초기화__ 는 아래와 같이 배열을 초기화 하는 방법과 비슷합니다.
        ```c
        struct structure_name {
            int var1;
            char var2;
        };

        int main(void) {
            struct structure_name def_var = { value1, value2 }; //배열 초기화를 생각하면 된다.
            ...
        }
        ```
    * 마지막으로, 배열을 __정의하면서 초기화를 하는 것__ 도 아래와 같이 할 수 있습니다.
        ```c
        struct structure_name {
            int var1;
            char var2;
        }def_var = { value1, value2 };
        ```
### 1.3 구조체를 쓰는 방법

구조체를 선언하고, 변수를 선언하였으면, 모든 준비는 완료되었습니다. 값을 집어넣으려면 __구조체 멤버 참조__ 를 쓰게 됩니다.

### __.__ 연산자를 활용합니다. 
    def_var.var1 // 변수 선언 . 구조체 안의 변수

* ex)
    ```c
    #include <stdio.h>

    struct banking { // 구조체 선언
        char name[20];
        char bank_num[16];
        double present_bank_amount;
    };

    int main(void) { // 구조체 변수 선언
        struct banking user_1;
        
        user_1.name = "user"; // 구조체 멤버 참조
        user_1.bank_num = "52192819283"; // 구조체 멤버 참조
        user_1.present_bank_amount = 3821.21; // 구조체 멤버 참조

        printf("%s", user_1.name);
        printf("%s", user_1.bank_num);
        printf("%lf", user_1.present_bank_amount);
    }
    ```
    * 위와 같은 예제에서, __.__ 을 활용하여서 구조체 멤버를 참조하여 변수에 값을 집어넣을 수 있는것을 알 수 있습니다.

### 1.4 구조체를 가지고 있는 구조체

정말 신기하게도, 구조체에서 다른 구조체의 항목을 참조해서 가져올 수 있습니다. ~~혼종~~ 

* 아래와 같이 구조체 내에서 다른 구조체 항목을 참조할 수 있습니다.

    ```c
    struct structure_name1 {
        int var1;
        char var2;
    };
    struct structure_name2 {
        int var3;
        char var4;
        struct structure_name1 var5; // structure_name1을 참조하여 넣는다.
    };
    
    int main(void) {
        struct structure_name2 def_var;

        def_var.var5.var1 = 10; // 이럴경우 바뀌는 인자는 int var1의 값이 10으로 바뀌게 된다.
    }
    ```

### 1.5 구조체의 대입과 비교

* 같은 구조체 변수끼리는 __대입__ 은 가능하지만 __비교__ 는 불가하다. (값을 집어넣는것은 가능하지만 컴퓨터는 저 항목을 따로따로 비교할줄을 모른다.)

    * ex)
        ```c
        #include <stdio.h>

        struct str {
            int var1;
            int var2;
        };

        int main(void) {
            struct str s1;
            struct str s2;

            s2 = s1; // 대입은 가능하다

            if (s1 == s2) { // 이런식으로 비교하면 비교 대상을 몰라서 비교가 안된다.
                return true;
            }

            if ( (s1.var1 == s2.var1) && (s1.var2 == s2.var2)) { // 올바른 비교 방법.
                return true;
            }
        }
        ```
    * 위와 같이 대입과 비교 방법을 알 수 있습니다.

### 1.6 구조체 배열

구조체는 배열과 비슷한 점이 있듯이, 배열처럼 선언도 가능합니다. 물론 초기화 방법등도 배열과 비슷한 점이 있습니다. 

* 구조체 배열은 아래와 같이 선언합니다.
    ```c
    #include <stdio.h>
    #DEFINE SIZE = 100;

    struct str {
        int var1;
        int var2;
    };

    int main(void) {
        struct str list[SIZE]; // 구조체의 배열 선언

        list[1].var1 = 100; // 배열에 값을 집어넣는 방법과 유사합니다.
        ...
    }
    ```
* 구조체 배열의 초기화는 아래와 같습니다.
    ```c
    #include <stdio.h>
    #DEFINE SIZE = 100;

    struct str {
        int var1;
        int var2;
    };

    int main(void) {
        struct str list[SIZE]; { // 구조체의 배열 선언
            { 100, 200 }
            ...
        };
        
        ...
    }
    ```

### 1.7 구조체의 포인터 활용

구조체가 배열과 비슷(?) 한 점이 있듯이, 포인터를 활용 할 수도 있고, 다른 구조체의 포인터도 참조 할 수 있다.

* 아래와 같이 활용 가능하다.

    ```c
    struct structure_name {
        int var1;
        char var2;
    };

    int main(void) {
        struct structure_name *def_var1;
        struct structure_name def_var2 = { value1, value2 };

        def_var1 = &def_var2;
        cout << (*def_var1).var1 << def.var1->var2 << endl; 
        /* (*var).var방식이나, var->var방식이나 똑같은 결과를 내놓는다.
        -> 은 구조체에서만 쓰이는 포인터.
        */
    }
    ```
    * 처음 보이는 문법중 __->__ 가 있습니다. 이는 (*var).var1 와 같은, 참조와 비슷한 문법입니다. 결국 var->var1 이나 (*var).var1과 같은 결과를 가지게 됩니다.

* __중요! 연산자 우선순위 ( . | > | * ) 때문에 *var.var 은 절대로 안된다! (값이 2번들어가게 된다.)__

* 또한 이전 포인터에서 보았듯이, 포인터를 맴버로 가지는 구조체도 생성이 가능합니다. 

### 1.8 구조체와 함수의 관계

구조체를 함수의 인수로 전달도 가능하고, 포인터를 통해서 전달도 가능합니다. 다만 __인수__ 로 전달할 경우 원본이 훼손되지는 않으나 __구조체의 크기가 커지면 속도저하는 피할 수 없으며__, 포인터로 전달할 경우 시간과 공간은 절약 가능하나 __원본이 훼손될 수도 있습니다.__

### 1.9 우리 type을 바꿔봐요, typedef

* typedef는 이름에서 알 수 있듯이 type을 define 해주는데 쓰인다. 아래를 보면 이해가 쉬울 것이다.

    ```c
    쓰는 방법 : typedef old_type new_type;

    ex)

    int main(void) {
        typedef unsigned int uint;

        uint a; // unsigned int a와 같은 역활을 한다.
    }
    ```
    또한 마찬가지로 구조체도 type을 변경 가능하다.
    ```c
    typedef struct structure_name { //type을 바꾸고....
        int var1;
        char var2;
    }str1; // 그 바꾼 별칭은 str1.

    int main(void) {
        str1 = { value1, value2 };
    }
    ```

* 정의해준다는 점에서 #DEFINE과 비슷하다는 생각을 할 수 있습니다. 맞습니다. 비슷한 효과를 둘다 냅니다. 하지만 __배열을 정의하는 등의__ 효과는 #DEFINE을 통해서는 불가합니다.

### 1.10 이노옴~~ enum(열거형 자료형)

* enum은 enumeration(열겨형)의 함수형 줄임말로, __변수가 가질 수 있는 값을 미리 열거해 놓은 자료형입니다.__

* 기본적인 형태는 아래와 같습니다.
    ```c
    enum str { a, b, c, d ...};
    ```
* 아래와 같이 사용합니다.
    ```c
    #include <stdio.h>
    
    enum str { a, b, c, d ...};

    int main(void) {
        enum str alpabat;

        alpabat = a; //이런식으로 선언해서 사용합니다.
    }
    ```
* 사용하는 이유는 __가독성을 높인다가__ 가장 큰 이유입니다. 다른 이유로는 __의미없는 값을 대입하는걸 사전에 차단__ 하는 이유도 있습니다.

* 초기화는 값을 지정하지 않을경우 0부터 시작하며, 지정하는 것도 가능합니다.