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
