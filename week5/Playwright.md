1. E2E(End to End) Test
2. Headless Chrome
3. Puppeteer
4. Playwright
5. CodeceptJS

![](https://velog.velcdn.com/images/dduone_1/post/21e0219a-5641-46d3-b917-e6fdeb1195c4/image.webp)


## 1. E2E(End to End) Test
> Endpoint 간 테스트로 사용자의 입장에서 테스트 하는 것이다. 보통 Web, App 등에서 GUI를 통해서 시나리오, 기능 테스트 등을 수행한다. 사용자에게 직접 노출되는 부분을 점검한다고 생각하면 된다.

#### 프론트엔드의 테스트
원하는 Text가 제대로 나오는지, A를 클릭했을때 기대하는 동작을 하는지 등을 테스트 한다. 작은 수정에도 테스트가 깨지기 쉽고 Mock Injection해서 UI만 테스트 하는것도 공수가 많이 들어간다.

**설치하기**
```
npm i -D @playwright/test eslint-plugin-playwright
```
**테스트 실행하기**
```
npx playwright test
```

https://ui.toast.com/posts/ko_20210818
https://hyperconnect.github.io/2022/01/28/e2e-test-with-playwright.html
