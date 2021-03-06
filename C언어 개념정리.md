#### <u>C 프로그램을 작성하고 실행하는 절차</u>

1. 편집기를 이용하여 C 프로그램을 pgm**.c라는 문서 파일로 만든다**. 파일명은 반드시 .c로 끝나야 하는데, 이는 **이 파일이 C 원시 코드를 포함하는 파일**임을 나타낸다. 예를 들어, UNIX 시스템에서 vi 편집기를 사용할 경우 다음과 같이 명령을 실행하면 된다.

> **vi pgm.c**

2. 프로그램을 컴파일한다. 컴파일 하는 명령어는 다음과 같다

> cc pgm.c

**cc** 명령은 **전처리기**, **컴파일러**, 그리고 **로더**를 차례대로 호출한다. **<u>전처리기</u>는**  원시코드를 복사한 후 전처리 지시자에 따라 그 사본을 수정하여, **번역 단위라는 것을 생성**한다. <u>**컴파일러**</u>는 **번역 단위를 목적 코드로 변환**한다. 여기서 오류가 발생하면, 프로그래머는 원시 파일을 수정하기 위해 1 단계부터 다시 시작해야만 한다. 이 단계에서 발생하는 오류를 구문 오류 또는 **컴파일 에러**라고 한다. 만일 오류가 없다면, **<u>로더</u>**는 컴파일러에 의해 생성된 목적 코드와 시스템이 제공하는 다양한 라이브러리의 목적 코드를 사용하여 **실행 파일 a.out을 생성**한다. 이제 이 프로그램은 실행될 수 있다.

3. 프로그램을 실행한다. 실행하는 명령어는 다음과 같다.

> a.out

실행 중에 발생하는 오류를 **런타임 에러**라고 한다.

cc명령의 출력은 -o 옵션을 사용하면 다른 파일에 저장할 수도 있다.

> cc -o sea sea.c

이 명령은 cc의 결과를 **a.out**이 아니라 **sea**에 바로 저장하게 한다.

<hr/>
#### `getchar()`

: 키보드로부터 **한 문자를 읽어** 들여 배정하기 위해 사용한다.

#### `putchar()`

: 매개변수로 들어온 **문자 c를** 표준출력에 문자로 **출력해주는 함수**



#### `strcpy(char* Dest, char const* Source)`

: **Source** 문자열을 **Dest**로 복사



#### `putc(int char, FILE* stream)`

: 스트림에 문자를 쓴다.



#### 일차원 배열

배열은 **일종의 집합**을 의미합니다. 지금까지 배운 것으론 변수 하나에는 하나의 값 밖에 담지 못했지만, 배열을 이용하면 하나의 변수에 여러 개의 값을 넣을 수 있게 됩니다.

<br/>

**배열 초기화하기**

```c
int main() {
	int arr1[5] = {1, 33, 47, 102, 155}; // 선언과 동시에 초기화
	int arr2[5] = {}; // 모두 0으로 초기화
	int arr3[] = {11, 22, 33, 44}; // 배열 크기 4로 자동 초기화
}
```

<br/>

**배열의 주소**

일반적으로 우리가 사용하는 변수들은 모두 메모리의 특정한 주소에 저장되어 있습니다. &가 주소값을 나타낸다고 했었던 것 기억하시나요? scanf를 사용할 때 주소값을 알려주기 위해 &를 사용한다고 했었는데요.

각 변수들은 선언될 때 메모리에 무작위로 저장됩니다.

<br/>

#### Call by value & Call by reference

#### `Call by value`

기본적으로 C언어에서 지원 방식.

함수에서 값을 복사해서 전달하는 방식으로, 인자로 전달되는 변수를 함수의 매개변수에 복사합니다.

이렇게 복사되면 인자로 전달한 변수와는 별개의 변수가 되며, 매개변수를 변경해도 원래의 변수에 영향을 미치지 않습니다.

```c
#include <stdio.h>

void swap(int a, int b) {
    int temp;
    
    temp = a;
    a = b;
    b = temp;
}

int main(){
    int a, b;
    
    a = 10;
    b = 20;
    
    printf("swap 전 : %d %d \n", a, b);
    swap(a, b);
    printf("swap 후 : %d %d \n", a, b);
    return 0;
}
```

> swap 전 : 10 20
>
> swap 후 : 10 20

<br/>

#### `call by reference`

함수에서 값을 전달하는 대신 주소값을 전달하는 방식을 **call by reference**라고 합니다.



```c
#include <stdio.h>

void swap(int *a, int *b) {
    int temp;
    
    temp = *a;
    *a = *b;
    *b = temp;
}

int main(){
    int a, b;
    
    a = 10;
    b = 20;
    
    printf("swap 전 : %d %d \n", a, b);
    swap(&a, &b);
    printf("swap 후 : %d %d \n", a, b);
    return 0;
}
```

> swap 전 : 10 20
>
> swap 후 : 20 10

<hr/>
#### 구조체 포인터와 ->

```c
#include <stdio.h>

typedef struct {
    int s_id;
    int age;
} Student;

int main(){
    Strudent goorm;
    Student *ptr;
    
    ptr = &goorm;
    
    (*ptr).s_id = 1004;
    ptr->age = 20;
    
    printf("goorm의 학번 : %d, 나이 : %d\n", goorm.s_id, goorm.age)
}
```

 <hr/>

#### 조건부 컴파일

전처리기는 조건부 컴파일을 위한 지시자를 가지고 있다.

>  **#if** 와 **#endif** 사이의 코드가 컴파일되기 위해서는 **#if** 다음의 상수 수식이 <u>영이 아닌 값(참)</u>을 가져야 한다.
>
> **#ifdef**나 **#if defined**와 **#endif** 사이의 코드가 컴파일 되기 위해서는 #ifdef나 #if defined 다음의 <u>identifier가 이미 #define으로 정의되어 있어야 한다</u>.
>
> 
>
> 그리고 **#ifndef**와 **#endif** 사이의 코드가 컴파일 되기 위해서는 **#ifndef** 다음의 **identifier**가 <u>현재 정의되어 있지 않아야 한다</u>.

< `#if - #elif - #endif ` 구조도 가능하다.

```c
#include "everything.h"
#undef PIE
#define PIE "I like apple."

주석 대신
statements
#if 0
more statements
#endif
```







