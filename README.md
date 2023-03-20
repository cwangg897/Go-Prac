

### 목차
[1.Go언어 특징정리](#go언어-특징-정리)<br>
[2.함수](#함수)<br>
[3.상수](#상수)<br>
[4.포인터](#포인터)<br>
[5.패키지](#패키지)<br>

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
```
<br>
```
Go모듈은 Go패키지들을 모아놓은 Go프로젝트 단위입니다. 1.16이상부터 모듈 사용이 기본이되었습니다.
모든 Go코드는 Go모듈 아래에 있어야합니다.
go build할려면 반드시 Go모듈 루트 폴더에 go.mod 파일이 있어야 합니다.

```

