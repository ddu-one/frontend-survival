### 학습 키워드

- Node.js
- NPM(Node Package Manager)
    - package.json / package-lock.json
    - node_modules
    - npx
- ES Modules vs CommonJS

-------------------

## Node.js 
Node.js는 Chrome V8 JavaScript 엔진으로 빌드 된 JavaScript 런타임

즉, 노드를 통해 다양한 자바스크립트 애플리케이션을 실행할 수 있으며, 서버를 실행하는 데 제일 많이 사용된다.

- Node.js는 JavaScript를 서버에서도 사용할 수 있도록 만든 프로그램이다.
- Node.js는 V8이라는 JavaScript 엔진 위에서 동작하는 자바스크립트 런타임(환경)이다.
- Node.js는 서버사이트 스크립트 언어가 아니다. 프로그램(환경)이다.
- Node.js는 웹서버와 같이 확장성 있는 네트워크 프로그램을 제작하기 위해 만들어졌다.


## NPM(Node Package Manager)
자바스크립트 패키지 매니저이다. (마치 앱스토어 느낌? 소프트웨어 창고?)
Node.js에서 사용할 수 있는 모듈들을 패키지화하여 모아둔 저장소 역할과 패키지 설치 및 관리를 위한 CLI(Command line interface)를 제공한다. 
필요한 패키지를 검색하여 사용

// 탄생 배경
- 여러 버전의 동일한 패키지를 한 프로젝트에서 사용할 수 있게 하자
- 설치 방식을 통일하자
- 패키지 관련 정보가 들어잇는 메타 데이터를 간소화 하자
- 누구나 배포할 수 있도록 하자

// 기본 디렉토리 구조
++ node_modules/
++ package-lock.json
++ package.json

### Yarn
npm에 불만을 느껴 yarn이 등장
yarn은 페이스북과 구글 개발자들이 모여서 2016년에 등장함
Yarn은 npm에서 계산하고자 하는 점들이 명확이 있었다.

- 병렬화를 통한 속도 개선
- 자동화 된 lock 파일 생성 (지금은 npm도 자동화 됐지만 yarn에서 생기고 나서 npm 도 적용이 됨)
- 의존성 트리 알고리즘 변경
- 캐시 사용(다운로드 받았던 것을 기억할 수 있음. 이게 왜 좋은가? -> 이미 다운로드되어 잇는 패키지에 대한 정보를 저장해서 더 이상 다운 받지 않도록하고 다운로드 속도를 개선하게 됨)

// 기본 디렉토리 구조
++ .yarn/
    ㄴ cache/
    ㄴ releases/
        ㄴ yarn-1.22.17.cjs
++ node_modules/
++ package.json
++ yarn.lock

## package.json? package-lock.json? 이거 두개 많이 봄
이거 많이 봤다.
근데 차이를 모르겠다.
대충 npm i 로 모듈 설치하면 저기에 모듈 버전 정보가 추가 된다는 정도?

이제 제대로 알고가잣...

### package.json
package.json은 생성한 프로젝트의 메타정보와 프로젝트가 의존하고 있는 모듈들에 대한 정보들을 json 형태로 모아놓은 파일이다.
package.json 파일을 사용하지 않을 경우 여러 문제가 발생할 수 있는데,

- 프로젝트에서 사용하는 외부 모듈들이 많아지게 되면 관리하기 어려워짐
- 패키지들의 버전관리가 어려워짐
- 새로운 프로젝트를 진행할 경우, 필요한 모듈들이 많다면 매번 npm 명령으로 설치해야하는 번거로움이 존재

package.json은 필요한 패키지들의 목록을 파일로 정리해놓고, 목록 파일을 이용하여 단 한번의 명령어로 필요한 패키지들을 모두 설치 할 수 있다. 
즉 package.json은 프로젝트에 대한 메타정보, 그리고 설치한 패키지의 의존성 및 버전을 관리하는 파일이다.
팀 내에서 동일한 개발환경을 구축하려고 할 경우, package.json을 통해 동일한 개발환경을 빠르게 구축할 수 있다.

npm init

명렁어를 통해 package.json의 초기 파일을 생성

실제 의존성 패키지는 dependencies
개발용 패키지는 devDependencies

- 참고 블로그 https://programmingsummaries.tistory.com/385

### package-lock.json
npm 공식문서에 따르면, package-lock.json은 npm이 node_modules트리 또는 package.json이 수정될 때, 자동으로 생성이 된다고 나와있다.

package.json 파일에는 의존성 모듈(dependencies)의 version range가 사용된다. 
version range란, 특정 버전이 아닌, 버전의 범위를 의미한다. 
예를 들어, npm install express로 express를 설치하면, package.json에는 ‘^4.10.3’(Caret Ranges)과 같이 버전 범위가 추가된다. 
이 버전의 express가 추가된 package.json을 가지고 npm install을 실행하면, 현재는 4.10.3 버전이 설치되지만, express의 버전이 업데이트된 상태로 publish가 된 후에, 
동일한 package.json 파일로 npm install을 실행했을 경우, 원래 버전이 아닌, 새로 업데이트된 버전으로 express가 변경된다. 
이럴 경우, 기존에 가지고 있던 node_modules(의존성 트리)에 있던 모듈의 버전과 충돌이 일어나, 오류를 발생시킬 수 있다. 
이 문제를 해결하기 위해, package-lock.json을 사용하는 것이다.

package-lock.json은 node_modules(의존성 트리)에 대한 정보를 가지고 있는데, package-lock.json이 업데이트가 되는 시점에 node_modules(의존성 트리)을 재생성할 수 있다. 
그래서, package-lock.json 파일이 있다면, npm install로 package.json과 package-lock.json에 있는 모듈이 새로 업데이트되는 동시에, 
node_modules(의존성 트리)가 새로 생성되어, 각 파일이 가지고 있는 모듈의 버전을 동일하게 맞출 수가 있게 된다.

즉, package.json에 있는 모듈의 버전은 npm install을 수행하는 시점에 따라 달라진다. 
이 말은, npm install을 수행하는 시점에 publish 되어있는 모듈의 버전으로 업데이트가 된다는 뜻이다. 
이렇게 되면, package.json과 package-lock.json에 있는 모듈이 같은 버전으로 업데이트가 되고, 이때 package-lock.json 때문에 node_modules(의존성 트리)가 재생성되어, 
3개의 파일에 있는 모듈이 모두 같은 버전으로 맞춰지게 되어 오류가 안나게 된다.

이런 이유로, git에 커밋할 때, package.json 파일 뿐만 아니라, packge-lock.json 파일 또한 같이 커밋을 해야 한다.

- 참고 블로그 https://cheonmro.github.io/2018/12/23/package-json/

### node_modules

npm을 통해 프로젝트를 생성하게 되면, node_modules라는 디렉토리가 생성되는데, package.json에는 현 프로젝트가 의존하고 있는 모듈들에 대한 정보가 나와있고, 
node_modules 디렉토리 안에는 package.json에 있는 모듈과, 그 모듈들이 의존하고 있는 모든 모듈들을 포함하고 있다. 
그래서 node_modules 디렉토리 안에는 모듈들의 의존성에 의해 정말 많은 모듈들이 포함되게 된다. 
npm으로 새로운 모듈을 설치하게 되면 자동으로 package.json과 node_modules에 추가되게 된다.
git에 커밋할 경우, node_modules는 제외할 수도 있다. 
node_modules가 없어도 package.json에 설치한 패키지들의 정보가 모여있기 때문에, npm install 명령어로 node_modules를 언제든지 추가할 수 있기 때문이다.

실제로 설치된 의존성 모듈들이 모두 들어있는 디렉토리. 애플리케이션이 사용할 코드는 여기서 가져다 쓰게 된다.

### npx 이건 뭐지..?
Node Package eXecute 노드 패키지 실행?
npm은 노드 패키지 매니저 npx는 노드 패키지 실행..

npx는 npm 사용시에 문제점 해결하기 위해 설계 됐다는데 무슨 문제점이 있누?

매일 사용하는 패키지는 아닌데 글로벌하게 설치하고, 용량을 차지, 또다른 문제는 지금 설치해 놓고 나중에 사용하려고 할때 이미 올드버전일 가능성이 있음
- 모듈 업데이트를 까먹음
- 사용없이 글로벌하게 설치해서 용량을 잡아먹음

그래서 "NPX"가 등장..!
이건 npm 패키지들을 컴퓨터 저장없이 사용할 수 있게 해줌 (오?)

(npm 5버전 이상이면 이미 npx는 설치되어있음)

## ES Modules, CommonJS 

JS 모듈을 내보내거나 가져올 때 2가지 방식을 사용한다.
- 첫번째 방법은 export로 모듈을 내보내고 import로 접근하는 ESM(ES Modules) 
- 두번째 방법은 module.exports로 모듈을 내보내고 require()로 접근하는 CJS(CommonJS)

```
// ESM 방법
export.default =()=> { ... }; // 모듈 내보낼 때
import utils from 'utils';    // 모듈 가져올 때  
```

```
// CJS 방법
module.exports = { ... }        // 모듈 내보낼 때
const utils = require('utils'); // 모듈 가져올 때   
```

















