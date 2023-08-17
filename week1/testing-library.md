### 학습 키워드
- Jest
- Describe-Context-It 패턴
- React Testing Library

--------------------------------------
## Jest : js 테스트 프레임워크

설치
```
$ npm install --save-dev jest
```

이 예시에서는 sum.js로 저장된 다음 모듈의 테스트 케이스를 작성한다:
```
function sum(a, b) {
  return a + b;
}
module.exports = sum;
```

테스트 케이스의 파일명은 sum.test.js이며 sum.js의 테스트 케이스로서 제스트가 선정한다.

테스트 케이스가 있는 파일의 내용은 다음과 같다

```
const sum = require('./sum');

test('adds 1 + 2 to equal 3', () => {
  expect(sum(1, 2)).toBe(3)
})
```
이때 명령줄에서 다음 명령을 실행한다:
```
$ npm run test
```
이를 통해 테스트를 수행하며 명령줄에서 일치하는 결과가 출력된다.

## Describe-Context-It 패턴

이 패턴은 코드의 행동을 설명하는 테스트 코드를 작성한다.

Describe - 설명할 테스트 대상을 명시. 테스트 대상이 되는 클래스, 메소드 이름을 명시.

Context - 테스트의 대상이 놓인 상황을 설명. 테스트할 메소드에 입력할 파라미터를 설명.

It - 테스트 대상의 행동을 설명. 테스트 대상 메소드가 무엇을 리턴하는지 설명.


