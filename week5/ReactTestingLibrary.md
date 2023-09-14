1. React Testing Library
2. given - when - then 패턴
3. Mocking
4. Test fixture

## 1. React Testing Library
React Testing Library는 facebook에서 공식적으로 사용을 권장하는 리액트 테스트 고두이다. 이 라이브러리는 사용자가 컴포넌트를 사용하는 것처럼 테스트를 작성할 수 있도록 설계되어있다.

```
npm install --save-dev @testing-library/react
```

## 2. given - when - then 패턴
> 준비 - 실행 - 검증 

| 키워드 | 설명 |
| ------------ | ------------- |
| given | 테스트에서 구체화하고자 하는 행동을 시작하기 전에 테스트 상태를 설명하는 부분  |
| when | 구체화하고자 하는 그 행동|
| then | 어떤 특정한 행동 때문에 발생할거라고 예상되는 변화에 대한 설명  |

```
예시
기능 : 사용자 주식 트레이드

시나리오 : 트레이드가 마감되기 전에 사용자가 판매를 요청

"Given" 나는 MSFT 주식을 100가지고 있다. 
        그리고 나는 APPL 주식을 150가지고 있다. 
        그리고 시간은 트레이드가 종료되기 전이다.

"When"  나는 MSFT 주식 20을 팔도록 요청했다.

"Then"  나는 MSFT 주식 80 가지고 있어야 한다.
        그리고 나는 APPL 주식 150을 가지고 있어야 한다.
        그리고 MSFT 주식 20이 판매 요청이 실행되었어야 한다.
```

## 3. Mocking
> Mocking이란 (mock = 모조품) 뜻 그대로 받아드리면 된디ㅏ.
즉 테스트하고자 하는 코드가 의존하는 function이나 class에 대해 모조품을 만들어 '일단' 돌아가게 하는 것이다. 
한마디로, 단위 테스트를 작성할 대, 해당 코드가 의존하는 부분을 가짜(mock)로 대체하는 기법을 말한다.

#### why??
테스트 하고 싶은 기능이 다른 기능들과 엮여있을 경우(의존) 정확한 테스트를 하기 힘들기 때문이다.

#### mocking 메소드 : jest.fn
> jest는 가짜 함수(nock function)를 생성할 수 있도록 jset.fn() 함수를 제공한다. 이를 이용해서 일회성 테스트용으로 내부의 함수를 진짜 같이 구동해서 코드를 구동 시킬 수 있다.

| 키워드 | 설명 |
| ------------ | ------------- |
| jest.fn() | 개별적으로 하나하나씩 모킹 처리 해줄때 사용|
| jest.mock() | 그룹을 한꺼번에 모킹 처리 해줄때 사용 |


## 4. Test fixture
> 중복 발생되는 행위를 고정시켜 한곳에서 관리하는 개념

#### test fixture 메소드 사용
| 키워드 | 설명 |
| ------------ | ------------- |
| @BeforeAll | 테스트 메소드 시작 전 1번 실행 |
| @AfterAll | 테스트 메서드 종료 후 1번 실행 |
| @BeforeEach | 각 테스트 메소드 시작 전 실행 |
| @AfterEach | 각 테스트 메소드 종료 후 실행 |


https://inpa.tistory.com/entry/JEST-%F0%9F%93%9A-%EB%AA%A8%ED%82%B9-mocking-jestfn-jestspyOn