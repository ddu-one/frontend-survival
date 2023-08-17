### 학습 키워드
- REPL
- TypeScript
    - Interface vs Type
    - 타입 추론
    - Union Type vs Intersection Type
    - Optional Parameter

-------------------

## REPL : Read-Eval-Print-Loop
REPL은 Read-Eval-Print-Loop의 약자로 
애플리케이션 실행 상태에서 사용자가 입력한 명령어(소스코드)를 읽고(Read) 명령어를 평가(Eval)하고 결과를 출력(Print)한 다음 다시 입력을 기다리는 상태로 돌아가는 과정을 반복(Loop)합니다.

=> REPL은 코드 실행 결과를 빠르게 확인하고 싶은 경우 유용합니다.(브라우저 개발 도구(예시: Chrome 개발 도구))

## TypeScript
자바스크립트의 단점을 보완해 만든 언어, 타입을 선언함으로써 컴파일 에러를 잡을 수 있음 (유지보수 측면으로 좋은거같음)

### Interface vs Type
회사에서는 interface를 써서 개인적으로 Type 보단 interface가 쓰기 편하다.

// Interface
interface PeopleInterface {
  name: string
  age: number
}

// Type
type PeopleType = {
  name: string
  age: number
}

차이점 정리!
type-alias는 모든 타입을 선언할 때 사용될 수 있고, 
interface는 객체에 대한 타입을 선언할 때 사용될 수 있다. 
둘 다 객체에 대한 타입을 선언하는 데 사용될 수 있는데, 확장 측면에서 사용 용도가 달라진다. 
확장이 불가능한 타입을 선언하려면 type-alias를 사용하면 되고, 
확장이 가능한 타입을 선언하려면 선언 병합이 가능한 interface를 사용하면 된다.

### 타입 추론 : 타입스크립트가 코드를 해석해 나가는 동작을 의미

let count = 10

count에 타입을 따로 지정하지 않더라도 count는 number로 간주됨


### Union Type vs Intersection Type

## Union Type : | 로 구분하고 Javascript 의 OR 연산자와 비슷한 역할
type Marvel = "IronMan" | "Hulk"
type Dc = "BatMan" | "SuperMan"

type Hero = Marvel | Dc

const hero1: Hero = "Hulk" // ✅ OK
const hero2: Hero = "BatMan" // ✅ OK

## Intersection Type : & 기호를 사용하면 양쪽에 모두 할당할 수 있는 값
type FavoriteSport = "swimming" | "football"
type BallSport = "football" | "baseball"

type FavoriteBallSport = FavoriteSport & BallSport; // 'football'


## Optional Parameter
이거 잘쓰고있음. 필수적으로 받아오는게 아니면 '?'로 옵셔널로 지정할 수 있음.
주의할 점은 옵셔널로 처리하면 undefined 값이 나올 수 있으니 방어 로직이 필요함.

