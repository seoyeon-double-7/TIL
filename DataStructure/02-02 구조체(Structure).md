# 구조체
## 구조체 정의
> **타입이 다른**  자료 원소를 하나로 묶은 자료형  

<br/>

## 구조체 선언
### <구조체 정의와 선언 따로>
```
struct book{
  char title[30];
  char writer[20];
  int value;
  char publisher[30];
};
struct book book1, book2, book3;
```
### <구조체 정의와 선언을 동시에>
```
struct book{
  char title[30];
  char writer[20];
  int value;
  char publisher[30];
} book1, book2, book33;
```
* 이름은 정의되는 구조체를 대표하는 *명칭* 이다.
* 구조체 변수를 선언하여야 비로소 정의된 구조체를 **사용** 할수 있다.
## 구조체 초기값 설정
### 하나의 구조체 변수에 초기값 설정
```
struct book book1 = {"유물로 읽는 역사", "이덕일 외", 15000, "세종서적"};
```
bok1.title은 `"유물로 읽는 역사"` 라는 문자열을 가지게 된다.
### 구조체 배열에 초기값 설정
```
struct book books[]={ {“김병호의 문화체험”, “김병호”, 10000, “푸른숲”},
{“인류의 기원”, “아서 니호프”, 12000, “푸른숲”},
{“0교시 문학시간”, “최지성”, 14000, “나라말”}};
```
books[1].title은 `"인류의 기원"`이라는 문자열을 가지게 된다.  
books[2].writer는 "최지성"이라는 문자열을 가지게 된다.

## 중첩 구조체
> 구조체 멤버를 내포하고 있는 구조체를 중첩 구조체라고 한다.

`중첩 구조체의 예`
```
struct personal_info{
 char name[20];
 char address[50];
 char tel_no[16];
 char e_mail[50];
};
struct book{
char title[30];
struct personal_info writer;
int value;
char publisher[30];
}b1;
```
구조형 변수 b1에 대해 그림으로 표현하면!  
![image](https://user-images.githubusercontent.com/83990943/167445652-de38f562-6ae2-4a4d-b637-8fc34382f530.png)

### 사용예
```
b1.title = “0교시 문학시간”;  
b1.writer.name = “이낭희”;  
b1.writer.address = “관악구 호암로 546”;  
b1.writer.tel_no = “872-4072”;  
b1.writer.e_mail = “mirim1@e-mirim.hs.kr”;  
b1.value = 14000;  
b1.publisher = “나라말”;
```
## 구조체 패딩(Padding) 현상
* 구조체는 구성원 중 가장 큰 데이터 타입을 기준하여 배수로 크기가 정해진다.
----
```
struct temp1{
  char ch;
  int value;
}
```
가장 큰 데이터 타입은 int(4byte)이고 구성원이 2개 이므로 4 x 2 = 8byte 크기로 temp1 구조체가 준비된다.
```
struct temp2{
int i1;
double d;
int i2;
};
```
가장 큰 데이터 타입은 double이므로 8byte 단위로 준비됨
따라서 8+8+8=24byte 크기의 temp2 구조체가 준비된다
```
struct temp3{
int i1;
int i2;
double d;
};
```
멤버를 int, int double type으로 순서를 변경하면 8byte에
int(4)를 연속해서 2개 저장하므로 padding이 발생하지 않는다.
temp3 구조체 크기는 8+8=16byte

## 공용체
> 공용체는 구조체와 정의나 사용 면에서 비슷한데,  
근본적인 차이점은 구조체는 구성원들이 각각 그들의 **고유한 기억장소**를 가지는데 비하여,  
공용체는 구성원들이 **같은 기억장소**를 사용한다는 점이다.  
공용의 기억장소는 구성원들 중에서 가장 메모리를 많이 사용하는 구성원이다
```
#include<stdio.h>
#include<string.h>
int main(void){
union uuu{
 int k;
 char c;
 char a[5];
} u1;
strcpy(u1.a, "ABC");
printf("\nk = %d, c = %c, a = %s", u1.k, u1.c, u1.a);
 return 0;
}
```
* 실행경과  
k = 4407873, c = A, a = ABC
* 설명  
  * 공용체 u1의 구성원들 중에서 k는 4바이트, c는 1바이트, a는 5바이트를 사용하므로
k, c, a는 5바이트를 같이 사용하게 된다.  
  * 맨 좌측 1바이트는 char 영역 : A  
  * 좌측 4바이트는 int 영역 : 좌측에서부터 A, B, C가 차례로 들어 있으나, 숫자는 낮은
자리가 우측에 놓이므로 k는 ‘\0’ ‘C’ ‘B’ ‘A’를 갖는다. 
  * ‘\0’는 00000000, ‘C’는
  01000011, ‘B’는 01000010, ‘A’는 01000001 이므로
  이진수 00000000010000110100001001000001를 10진수로 변환하면 4407873
a는 문자열 “ABC”
