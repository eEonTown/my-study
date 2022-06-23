# this
> Java에서는 객체 자신을 의미하는데 JavaScript에서는 조금 다릅니다.
> JavaScript에서의 this는 "누가 호출했지"를 뜻합니다.
> 즉, 호출방식에 따라서 this가 가리키는게 달라집니다.

<br>

### 호출방식
> 호출방식에는 함수 호출, 메소드 호출, 생성자 함수 호출 등이 있습니다.

##### 함수 호출
> 함수 호출을 하면 this가 가리키는 것은 최상위 객체인 window를 가리키게 됩니다.
```js
function eun(){
    console.log(this); //window가리킴
}

eun(); //함수 호출
```

<br>

##### 메소드 호출
> 메소드 호출을 하면 this가 가리키는 것은 메소드를 호출한 객체를 가리킵니다.
> *객체안에 선언된 함수를 메소드라고 합니다.
```js
const object = {
    name : eun,
    introduce : function(){
        console.log(this); //object가리킴
    }
}

object.introduce(); //메소드 호출
```

<br>

##### 생성자 함수 호출
> 생성자 함수 호출을 하면 this가 가리키는 것은 새로 생성된 객체를 가리킵니다.
> *일반 함수에 new를 붙여 호출하면 생성자 함수로 인식을 하기 때문에 생성자 함수명의 첫글자를 대문자로 기술해 구분합니다.
```js
function Me(name){
    this.name = name; // 생성된 객체를 가리킴
}

let eun = new Me("eun"); //생성자 함수 호출
```
