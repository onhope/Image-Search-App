# Image-Search-App
<img src="./image-search.gif" width="400px">

<br>

## 기능  
키워드를 검색하면 해당 이미지가 나오는 사이트   

<br>

## API
https://unsplash.com/developers  

<br>

## 학습  
### 1. html : form 태그  
- 의미   
  정보를 제출하기 위한 대화형 컨트롤을 포함하는 문서 구획  
 
- **사용하는 이유**  
  <u>웹 페이지에서 내 정보를 서버로 보내거나</u> 혹은 서버로 보내지 않더라도 <u>자체 웹 페이지에서 사용자와 상호작용을 하기 위해</u> 입력값이나 버튼과 같은 이벤트 요소가 필요할 때 사용되는 태그  

<br>

### 2. js : event.prevent Default()를 쓰는 이유 
- 의미  
  어떤 이벤트를 명시적으로 처리하지 않은 경우, <u> 해당 이벤트에 대한 사용자 에이전트의 기본 동작을 실행하지 않도록 지정</u>  


- *(예) 링크가 URL을 열지 못하도록 방지* 
     
  `<a>` 태그는 href에 연결된 링크를 통해, 해당 페이지로 이동하는 기능을 하는데, event.prevent Default()를 사용하여 이 기본 동작이 안 되도록 지정하기  

  ```
  <!DOCTYPE html>
  <html>
    <body>
      <a id="myAnchor" href="https://w3schools.com/">Go to W3Schools.com</a>

      <p>The preventDefault() method will prevent the link above from following the URL.</p>

      <script>
        document.getElementById("myAnchor").addEventListener("click", function(event){
          event.preventDefault()
        });
      </script>

    </body>
  </html>
  ```

<br>

### 3. js : 비동기 async, await 
- **동기**   
  코드가 작성한 순서에 따라 실행   

<br>  

- **비동기**   
  요청을 보낸 후 응답의 수락 여부와는 상관없이 다음 태스크가 동작하는 방식이다. <u>a 태스크가 실행되는 시간 동안 b 태스크를 할 수 있으므로 자원을 효율적으로 사용</u>할 수 있다.  
  
  이때, 비동기 요청시 응답 후 처리할 <u>'콜백 함수'</u>를 함께 알려준다. 따라서 해당 태스크가 완료되었을 때, '콜백 함수'가 호출된다.  
  
  하지만 비동기 처리를 위해 콜백 패턴을 사용하면 처리 순서를 보장하기 위해 여러 개의 콜백 함수가 중첩되어 복잡도가 높아지는 <u>콜백 헬(Callback Hell)</u> 이 발생하는 단점

<br>    

- **프로미스(Promise)**  
  ES6에서는 비동기 처리를 위한 또 다른 패턴으로 프로미스(Promise)를 도입  

  프로미스는 후속 처리 메소드인 <u>then이나 catch로 메소드를 체이닝(chainning)</u>하여 여러 개의 프로미스를 연결하여 사용할 수 있다. 이로써 콜백 헬을 해결
  ```
  <script>
    function timer(time) {
      return new Promise(function(resolve) {
        setTimeout(function(){
          resolve(time);
        }, time);
      });
    }
    console.log('start');
    timer(1000).then(function(time){
      console.log('time' + time);
      return timer(time+1000);
    }).then(function(time){
      console.log('time' + time);
      return timer(time+1000);
    }).then(function(time){
      console.log('time' + time);
      return timer(time+1000);
    });
  </script>
  ```

  <br>

- **async, await**  
  비동기 처리 방식인 <u>콜백 함수와 프로미스의 단점을 보완</u>하고 개발자가 읽기 좋은 코드를 작성할 수 있게 도와준다.    

  **기본 문법**  
  ```
  async function 함수명() {
    await 비동기_처리_메서드_명();
  }
  ```
  ```
      async function run() {
      console.log('start');  // 순서 2
      var time = await timer(1000);
      console.log('time' + time);  // 순서  3
      time = await timer(1000);
      console.log('time' + time);  // 순서  4
      time = await timer(1000);
      console.log('time' + time);  // 순서  5
      console.log('end'); // 순서  6
    }

    async function run2() {
      console.log('parent srart');  // 순서  1
      await run();
      console.log('parent end');  // 순서  7
    }
    run2();
  ```

<br>

### 5. js : map() 함수 
- 의미   
   배열 내의 모든 요소 각각에 대하여 주어진 함수를 <u>호출한 결과를 모아 새로운 배열을 반환</u>

  ```
  const array1 = [1, 4, 9, 16];

  // Pass a function to map
  const map1 = array1.map((x) => x * 2);

  console.log(map1);
  // Expected output: Array [2, 8, 18, 32]
  ```

<br>

## 학습 출처  
**Youtube**   
https://www.youtube.com/@JavaScriptKing  
https://www.youtube.com/watch?v=1z5bU-CTVsQ  (생활코딩)

**CSS**  
https://www.w3schools.com/#gsc.tab=0    
https://developer.mozilla.org/ko/  
https://inpa.tistory.com/entry/HTML-%F0%9F%93%9A-%ED%8F%BCForm-%ED%83%9C%EA%B7%B8-%EC%A0%95%EB%A6%AC  
**JS**  
https://velog.io/@hang_kem_0531/JS-event.preventDefault-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0    
https://velog.io/@khy226/%EB%8F%99%EA%B8%B0-%EB%B9%84%EB%8F%99%EA%B8%B0%EB%9E%80-Promise-asyncawait-%EA%B0%9C%EB%85%90    

**키워드**    
- form
- event.prevent Default()  
- 비동기 처리 
- async, await  
- map()