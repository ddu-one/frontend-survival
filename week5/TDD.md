## TDD

1. TDD란
2. Jest
3. Describe - Context - It 패턴
4. 단위테스트란


### 1. TDD란
> Test Driven Development의 약자로 테스트 주도 개발이라고 한다.
생명주기 : Red -> Green -> Refactor

| 키워드 | 설명 |
| ------------ | ------------- |
| Red | 실패하는 테스트 코드를 작성. 인터페이스와 스텍에 집중한다. |
| Green | 재빨리 테스트를 공과시킨다. 올바른 방법이 아니어도 괜찮다. |
| **Refactor **| 리팩터링을 통해 코드를 올바르게 만든다. TDD에서 가장 중요한 부분이지만, 간과될 때가 많다. |

![](https://velog.velcdn.com/images/dduone_1/post/ad171116-648b-4c83-a59e-6ed0ae596c87/image.png)


TDD와 일반적인 개발 방식의 가장 큰 차이점은** 테스트 코드를 작성한 뒤에 실제 코드를 작성**한다는 점이다.

디자인(설계) 단계에서 프로그래밍 목적을 반드시 **미리 정의**해야만 하고,
또 무엇을 테스트해야 할지 **미리 정의(테스트 케이스 작성)**해야한다.

1. 테스트 코드를 작성하는 도중에 발생하는 예외 사항(버그, 수정사항)들을 테스트 케이스에 추가하고 설계를 개선한다.
2. 이후 테스트가 통과된 코드만을 코드 개발 단계에서 실제 코드로 작성한다.

이러한 반복적인 단계가 진행되면서 자연스럽게 코드의 버그가 줄어들고, 소스코드는 간결해진다.
또한, 테스트 케이스 작성으로 인해 자연스럽게 설계가 개선됨으로 재설계 시간이 절감된다.

#### TDD 장점
1. 디버깅 시간을 단축 할 수 있다.
2. 코드가 내 손을 벗어나기 전에 가장 빠르게 피드백 받을 수 있다.
3. 작성한 코드가 가지는 불안정성을 개선하여 생산성을 높일 수 있다.
4. 재설계 시간을 단출 할 수 있다.
5. 추가 구현이 용이하다.

#### TDD 단점
1. 가장 큰 단점은 바로 생산성의 저하이다.
2. 이제까지 자신이 개발하던 방식을 많이 바꿔야 한다.
3. 구조에 얽매힌다.

## 2. Jest
> Jset는 페이스북에서 만들어서 React와 더불어 많은 자바스크립트 개발자들로 부터 좋은 반응을 얻고 있는 테스팅 라이브러리다.
출시 초기에는 프론트앤드에서 주로 쓰였지만 최근에는 백엔드에서도 기존의 자바스크립트 테스팅 라이브러리를 대체하고 있다.

BDD 스타일일때는 spec.ts 보통 test.ts


**Jest 설치**
```
npm i -D jest
```
설치를 완료한 뒤에 Package.json 파일을 열고 script > test 스크립트를 jest로 추가해 주자.
`npm start` 처럼 유명한 예약어라,` npm run test` 대신 바로 `npm test`로 스크립트 실행이 가능하다.

![](https://velog.velcdn.com/images/dduone_1/post/df03e7b7-0742-42cb-997e-c0279ca792aa/image.png)

jest에서 typScript 사용하도록 jest.config.js 파일 작성
```
module.exports = {
    testEnvironment: 'jsdom',
    setupFilesAfterEnv: [
      '@testing-library/jest-dom/extend-expect',
    ],
    transform: {
      '^.+\\.(t|j)sx?$': ['@swc/jest', {
        jsc: {
          parser: {
            syntax: 'typescript',
            jsx: true,
            decorators: true,
          },
          transform: {
            react: {
              runtime: 'automatic',
            },
          },
        },
      }],
    },
  };
```  

**Jest 기본 문법**
```
describe('계산 테스트', () => {
   const a = 1, b = 2;

   test('a + b는 3이다.', () => {
      expect(a + b).toEqual(3);
   });
});

/*
describe('그룹 테스트 설명 문자열', () => {
   const a = 1, b = 2; // 테스트에 사용할 일회용 가짜 변수 선언

   test('개별 테스트 설명 문자열', () => {
      expect(검증대상).toXxx(기대결과);
   });
});
*/
```
`describe`는 테스트 그룹을 묶어주는 역할을 하고, 그안에 콜백함수 내에 테스트에 쓰일 변수, 객체들을 선언하여 일회용으로 사용 할 수 있다.
`toXxx` 부분에서 사용되는 함수를 흔히 Test Mathcher라고 하는데, 위에 사용된 toEqual() 함수는 값을 비교할때 사용한다.
즉, `expect(a + b).toEqual(3);` 이라는 말은 a+b의 기대값이 3과 같으면 true를 의미한다고 보면 된다.

npm test를 실행하면 프로젝트 내에 모든 테스트 파일을 찾아서 테스트를 실행해준다.
jest는 기본적으로 `test.js`로 끝나거나,`_test_`디렉터리 안에 있는 파일들을 모두 테스트 파일로 인식한다.
만약 특정 테스트 파일만 실행하고 싶은 경우에는 `npm test <파일명이나 경로>`를 입력하면 된다.

## 3. Describe - Context - It 패턴
> BDD 테스트 코드 작성 패턴이다
`Describe - Context - It` 은 상황을 설명하기보다는 테스트 대상을 주인공 삼아 행동을 더 섬세하게 설명하는데에 적합하다. 
이 패턴을 사용해 테스트코드를 계층 구조로 만들어 어떤 흐름에서 테스트코드가 실행되는지 알기 쉽게 설명할 수 있다.


| 키워드 | 설명 |
| ------------ | ------------- |
| Describe | 설명할 테스트 대상을 명시한다.  |
| Context | 테스트 대상이 놓인 상황을 설명한다. with 또는 when으로 시작하도록 한다.|
| It | 테스트 대상의 행동을 설명한다. 행동을 심플하게 설명한다.|

**Describe**
```
describe('login', () => {
```
**Context**
```
context('with correct accountNumber and password ', () => {
```
**It**
```
it('load accountNumber information', async () => {
```

## 4. 단위테스트란

> 단위 테스트(Unit Test)는 하나의 모듈을 기준으로 독립적으로 진행되는 가장 작은 단위의 테스트이다. 여기서 모듈은 애플리케이션에서 작동하는 하나의 기능 또는 메소드로 이해할 수 있다. 예를 들어 웹 애플리케이션에서 로그인 메소드에 대한 독립적인 테스트가 1개의 단위테스트가 될 수 있다.
즉, 단위 테스트는 애플리케이션을 구성하나 하나의 기능이 올바르게 동작하는지를 독립적으로 테스트하는 것으로, '어떤 기능이 실행되면 어떤 결과가 나온다' 정도로 테스트를 진행한다.