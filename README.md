

### 목차
[1.Go언어 특징정리](#go언어-특징-정리)<br>
[2.함수](#함수)<br>
[3.상수](#상수)<br>
[4.포인터](#포인터)<br>
[5.패키지](#패키지)<br>
[6.슬라이스](#슬라이스)<br>
[7.메서드](#메서드)<br>


## Go언어 특징 정리
- 정적컴파일언어 : 모두 실행하기전 컴파일해서 exe파일을 실행시켜야한다.  속도는 빠르다 그러나 플랫폼에 영향을 받지만, Go는 내부 환경 변수만 바꿔서 다양한 플랫폼에 맞도록 실행 파일을 만들 수 있어서 비교적 쉽게 대응가능
- 최강 타입 언어 : 자바는 타입언어이지만 자동타입변환이있지만 Go는 없다 그래서 최강타입이다
- 가비지 컬렉터 유무 : 가비지 컬렉터 제공, GC제공한것들중 제일빠른 GC다 매우 좋다.

### 코드 실행되기까지
1. 폴더 생성
2. .go파일 생성 및 작성 (확장자는 .go)
3. Go 모듈 생성 - go mod init 모듈이름(주로 폴더명과 같은것사용) 1.16 버전 이후로 Go모듈이 기본 적용됨
4. 빌드 - go build (go 컴파일러 사용) GOOS와 GOARCH환경변수 조정해서 다른 OS와 아키텍처 실행되는 실행파일 생성가능 - go tool dist list
5. 실행


### 함수
```
go에서는 함수중에 멀티 반환함수도 존재한다
반환타입 이름을 명시도 가능하다
```

### 상수
- iota const 소괄호안에서만 유효함 
- 타입없는 상수 (타입오류가 발생안함 왜냐하면 변수에 복사될 때 타입이 정해지기 때문에 여러 타입에 사용되는 상숫값을 사용할 때 편리)

### 느낀점1
```
not used라는걸 통해서 사용하지않는것은 체크해주는것을보면은 go언어는 메모리관리가(gc) 굉장히 뛰어난게 사실인것같다는 생각이든다

```

### 포인터
go lang은 기본적으로 call by value를 사용하고 Call By Reference를 하고 싶으면 포인터로 넘겨주는 방식이다.

### 문자열
char 타입이 없고 rune로 대체한다. len함수는 길이가 아니라 바이트 길이를 반환한다 그래서 문자열을 바로비교하지말고 []rune(str) 해서 배열의 길이를 통해 

### 패키지, Go 모듈
```
컴파일러는 패키지가 main인것을 찾음 main패키지는 시작점이라는 것을 알려주는 패키지
함수로는 코드블록, 구조체로 데이터를, 패키지로 함수와 구조체를 묶습니다.
패키지는 코드를 묶는 단위입니다. 여러 패키지가 많습니다. 이더리움, AI 그렇다면 패키지를 가져다 사용하면 기능을 쉽게 만들 수 있습니다.
패키지를 사용하려면 import한다

main을 제외한 package는 자기마음대로 지을 수 있고 
다른곳에서 가져와 사용할때는 import하면 패키지를 가져와서 사용가능하다 자바랑 다를거없음.

```
<br>


```
Go모듈은 Go패키지들을 모아놓은 Go프로젝트 단위입니다. 1.16이상부터 모듈 사용이 기본이되었습니다.
모든 Go코드는 Go모듈 아래에 있어야합니다.
go build할려면 반드시 Go모듈 루트 폴더에 go.mod 파일이 있어야 합니다.
```

### 슬라이스
```
슬라이스는 go에서 지원해주는 동적배열이다 즉 배열의 종류다 
슬라이스는 append를 통해 동적으로 늘리지만 실제로 내부 구현은 reflect패키지의 SliceHeader구조체로 내부구현이되어있다.
reflect패키지는 자바의 util과 비슷한거같고, slice내부는 배열을 새롭게 만들고 포인터를 통해가리킨다.
배열과 슬라이스의 차이점은 파라미터로 값을 넘겼는데 바뀐다는것이다. 
동작 차이의 원인은 Go는 모든 값의 대입은 복사로 이루어진다. 그래서 call by reference로 직접 접근하는방법이지만 
슬라이스의 내부 구현은 포인터, len, cap 이다 그래서 포인터 값이 그대로 복사되면서 실제배열은 같은곳은 가리키게 되기때문이다.
```
<br>
- 슬라이스 append()사용시 발생하는 문제1 : 모두 같은곳을 가리키지만 포인터만 그렇고 len, cap이 다르기때문에 정합성 문제로 인해 이미 길이가 다 채워져 값 추가가 못하는 경우 변경해버리는 문제가 생긴다. 
- 슬라이스 append()사용시 발생하는 문제2 : 빈공간이 부족하면 새롭게 크기를 만들고 포인터는 다른곳을 바라보게 된다. 

#### 슬라이스 정리
append시에 같은곳을 가리킬때 len, cap이 달라서 발생하는 문제, 길이가 모자라서 새로운곳을 바라보게되어 같은곳을 안바라보는 문제 

### 메서드
```
메서드는 함수의 일종입니다.
그런데 go에는 클래스가없습니다. 그래서 구조체 밖에 메서드를 선언하는데 구조체 밖에 메서드가 있으므로 메서드가 어느 구조체에
속하는지 표시할 방법이 바로 리시버입니다. 리시버는 메서드가 속하는 타입을 알려주는 기법입니다.

메서드는 코드의 응집도를 높이고 재사용성을 높이고 모듈화로 가독성도 높아집니다.
```



