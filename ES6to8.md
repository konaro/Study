##ECMAScript_2015

### 01.02_Environment setup

- 透過 nodejs 的 npm 套件管理工具將 TypeScript 編譯器安裝到系統環境中

  ```bash
  $ npm install -g typescript
  ```

- 透過 TypeScript 的 tsc 指令，將 .ts 編譯成 javascript 檔案

  ```bash
  $ tsc {file}.ts
  ```

- 在專案方式管理的考量下，透過 package.json 可以有效管理專案使用的相關套件，透過 npm init 能建立專案相關的資訊，另外透過 -y 參數自動產生預設的 package 資訊

  ```bash
  $ npm init -y
  ```

- 使用 lite-server 建置開發伺服器及監看專案並即時反應

- 透過 tsc —init 初始化 TypeScript 設定檔 tsconfig.json，之後使用編譯器時，即會依照設定檔進行編譯





### 03_Let Const

- 透過 let 宣告的變數僅存在於該 block `{}` 中
- 透過 const 來宣告常數，若試圖在宣告後變更常數值，則會出現編譯錯誤

> 詳細內容可以參考 **Appendix_ECMAScript** [Block-Scoped Constructs Let and Const](#es6-block-scoped)



###04_Template literal 

- 透過 backsticks 會將 `` 內的內容視做 template literals，可在 template literals 串接字串與變數以及撰寫多行字串

> 詳細內容可以參考 **Appendix_ECMAScript** [Template Literals](#es6-template-literals)



### 05_Arrow Function

- ES6 之後的版本提供 arrow function 語法，簡化 function 定義

> 詳細內容可以參考 **Appendix_ECMAScript** [Arrow Functions](#es6-arrow-functions)



### 06_Default parameter

- ES6 之後的版本在宣告 function 時，可以定義預設的參數值，並且可以在使用其他參數進行運算
- 若是在參數使用其他參數運算時，則需要注意參數順序的設置

> 詳細內容可以參考 **Appendix_ECMAScript** [Default Parameters](#es6-default-parameters)



### 07.08_Spread & rest

- spread：在呼叫方法時，透過 `...` 將陣列中的元素拆開分成數個參數傳入方法

  ```typescript
  var arr = [1, 2, 3, 4];
  Math.max(arr); // syntax error
  Math.max(...arr); // 4
  ```

- rest：在定義方法時，透過 `...` 定義該方法可擁有數個參數，則該方法可傳入不限數量的參數

  ```typescript
  var sum = (...numbers) => {
    let result = 0;
    numbers.forEach(item => result += item);
    return result;
  }

  sum(3, 4, 2); // 9
  ```

  > 需注意如方法宣告使用 rest，則後方不可再定義其他參數

- 透過 spread 可以讓陣列結合變得更容易

  ```typescript
  // former
  let arr = [3, 4, 5];
  console.log([1, 2].concat(arr)); // [1, 2, 3, 4, 5]
  // es6
  console.log([1, 2, ...arr]); // [1, 2, 3, 4, 5]

  // former
  let arr2 = [10, 20];
  console.log(arr2.push.apply(arr2, arr)); // [10, 20, 3, 4, 5]
  // es6
  let arr3 = [30, 40];
  arr3.push(...arr); // [30, 40, 3, 4, 5]
  ```

- 透過 rest 與解構語法的結合，在陣列中可以取得剩餘元素，在物件中可以取得剩餘屬性

  ```typescript
  let arr = [10, 11, 12, 13];
  let [a, b, ...rest] = arr;
  console.log(rest); // [12, 13]

  let obj = {a: 10, b: 'text', c: true, other: {}};
  let {a, b, ...rest} = obj;
  console.log(rest); // {c: true, other: {}}
  ```

  > 解構語法可以參考 **Appendix_ECMAScript** [Destructuring Assignment](#es6-destructuring-assignment)




### 09_Homework

*試著將下列 Javascript 語法改以 ES6 以上的標準重新撰寫*

```javascript
// Exercise 1
var double = function(value) {
    return value * 2;
};
console.log(double(10));

// Exercise 2
var greet = function (name) {
    if (name === undefined) { name = "Max"; }
    console.log("Hello, " + name);
};
greet();
greet("Anna");

// Exercise 3
var numbers = [-3, 33, 38, 5];
console.log(Math.min.apply(Math, numbers));

// Exercise 4
var newArray = [55, 20];
Array.prototype.push.apply(newArray, numbers);
console.log(newArray);

// Exercise 5
var testResults = [3.89, 2.99, 1.38];
var result1 = testResults[0];
var result2 = testResults[1];
var result3 = testResults[2];
console.log(result1, result2, result3);

// Exercise 6
var scientist = {firstName: "Will", experience: 12};
var firstName = scientist.firstName;
var experience = scientist.experience;
console.log(firstName, experience);
```

- Answer

```javascript
// Exercise 1
let double = (value: number) => value * 2;
console.log(double(10));

// Exercise 2
let greet = (name: string = 'Max') => console.log(`Hello, ${name}`);
greet();
greet('Anna');

// Exerciese 3
let numbers = [-3, 33, 38, 5];
console.log(Math.min(...numbers));

// Exercise 4
let newArray = [55, 20];
newArray.push(...numbers);

// Exercise 5
let testResults = [3.89, 2.99, 1.38];
let [result1, result2, result3] = testResults;
console.log(result1, result2, result3);

// Exercise 6
let scientist = {firstName: 'Will', experience: 12};
let {firstName, experience} = scientist;
console.log(firstName, experience);
```







## Appendix_ECMAScript Features

###ES 2015（ES6）Features

- <span id="es6-default-parameters">Default Parameters：</span>

  - 在呼叫 function 時沒有提供參數時，提供設定預設值，避免出錯

    ```javascript
    var foo = function(height = 100) { ... }
    ```

- <span id="es6-template-literals">Template Literals：</span>

  - 透過新的語法 `${val}` 組合字串，注意使用的符號為 backticks ``

    ```javascript
    // es5
    // var name = 'Mr.' + lastNamae + '.'
    var name = `Mr. ${lastName}.`
    ```

- Multi-line Strings：

  - 透過 backticks `` 能宣告多行字串

    ```javascript
    // es5
    // var name = 'first line'
                  + 'sceond line'
    var name = `first line
                second line`
    ```

- <span id="es6-destructuring-assignment">Destructuring Assignment：</span>

  - 透過 value assignment ，把 array 中的值 assign 到對應位置的變數

    ```javascript
    var [a, b, ...rest] = [1, 2, 3, 4, 5]
    console.log(a) // 1
    console.log(b) // 2
    console.log(rest) // [3, 4, 5]
    ```

  - 或是 object 內對應的屬性 assign 到變數

    ```javascript
    var o = {p: 42, q: true, r: 'text', other: []}
    var {p, q, ...rest} = o
    console.log(p) // 42
    console.log(q) // true
    console.log(rest) // {r: 'text', other: []}
    ```

  - 若是要對 object 設定對應屬性的變數名稱，則可以如下宣告

    ```typescript
    var o = {p: 42, q: true}
    var {p: customP, q: customQ} = o
    console.log(customP) // 42
    console.log(customQ) // true
    ```

- Enhanced Object Literals：

  - 加強 object 定義，提供屬性縮寫語法

    ```javascript
    function Car(product, value) {
      return {
        product, // same as product: product
        value, // same as value: value
      }
    }
    ```

  - 提供物件實字的初始值運算（computed property keys）

    ```javascript
    function Car(product, value) {
      return {
        ...,
        // computed values now work with object literals
        ['make' + product]: true 
      }
    }
    ```

  - 提供方法的縮寫語法，去除 function 關鍵字及冒號

    ```javascript
    function Car(product, value) {
      return {
        ...,
        // Method definition shorthand syntax omits `function` keyword & colon
        depreciate() {
          return this.value
        }
      }
    }
    ```

- <span id="es6-arrow-functions">Arrow Functions：</span>

  - 透過 Arrow function expression，this 只會對當前 function 內容有效（而不再對應到外部物件）

    ```javascript
    // basic
    (param1, param2, ..., paramN) => { statements }

    // same as => { return expression; }
    (param1, param2, ..., paramN) => expression

    // omit parenthesis when only one parameter included
    (singleParam) => { statements }
    singleParam => { statements }

    // with no parameter
    () => { statements }
    ```

- Promises：

  - ES6 針對 Promises 製訂了一套標準，在方法中創建 Promise，透過執行 Promise 建構式時帶入的 resolve 與 reject callback function 完成

    ```javascript
    var newPromise = () => new Promise((resolve, reject) => {
    	if (expression)
    	  resolve(`success.`)
    	else
    	  reject(`error.`)
    })
    ```

- <span id="es6-block-scoped">Block-Scoped Constructs Let and Const：</span>

  - let 宣告的變數僅存活在該 block `{}` 中，不允許重複宣告、不允許宣告前使用
  - const 宣告的變數僅存活在該 block `{}` 中，同 let 且不能再改變值

  > let / const / class 不為 hoisted，因此當試圖在宣告值前叫用 let / const / class 會出現 ReferenceError

- Classes：

  - 可定義及實體化 Classes
  - 通過 extends 創建 subclasses
  - 通過 super 呼叫 parent object
  - 四個重要的 methods
    - Constructors
    - Static methods
    - Prototype methods
    - Symbol methods：Symbol 為唯一性

- Modules：

  - 將物件、變數模組化，使用 import, export 載入、匯出模組

    ```javascript
    export function getModule(){
      ...
    }
      
    import { getModule } from 'module'
      
    getModule();
    ```



###ES 2016（ES7）Features

- Array.prototype.includes

  - 判斷陣列中是否含有指定的值，用來代替 Array.prototype.indexOf

    ```javascript
    let arr = ['react', 'angular', 'vue']
    // former
    if (arr.indexOf('react') !== -1) {
      console.log('Can use React!')
    }

    // current
    if (arr.includes('react')) {
      console.log('Can use React!')
    }
    ```

- Exponentiation Operator

  - 透過 `**` 簡化指數運算語法

    ```javascript
    // former
    let calculateExponent = Math.pow(7, 12)

    // current
    let calculateExponent = 7 ** 12
    ```



###ES 2017（ES8）Features

- Object.values / Object.entries

  - 與 Object.keys 類似，用以取得 Object 中各屬性 value 及各屬性 key value

    ```javascript
    let obj = {a: 1, b: 2, c: 3}
    // Object.keys to get value
    for (let key of Object.keys(obj)) {
      console.log(key, obj[key])
    }
    // a 1, b 2, c 3

    // Object.values to get value
    for (let value of Object.values(obj)) {
      console.log(value)
    }
    // 1, 2, 3

    // Object.entries to get key value pairs
    for (let [key, value] of Object.entries(obj)) {
      console.log(`${key} is ${value}`)
    }
    // a is 1, b is 2, c is 3
    ```

- String padding

  - 使用 String.prototype.padStart / String.prototype.padEnd 來為字串設定固定長度，並以設定的參數字元填入不足的部分

    ```javascript
    // padStart: insert pads at the beginning
    console.log('react'.padStart(10))          // "     react"
    console.log('backbone'.padStart(10, '_'))  // "__backbone"

    // padEnd: insert pads at the end
    console.log('react'.padEnd(10))			   // "react     "
    console.log('backbone'.padEnd(10, '_'))    // "backbone__"
    ```

- Object.getOwnPropertyDescriptors

  - 用以取得 object 中所有 properties 的內容，包含對應的 prototype 等

- Trailing commas in function parameter lists and calls

  - 陣列及物件中，在最後一個元素/屬性後含有 commas `,` 也沒有問題

    ```javascript
    var arr = [1, 2, 3,]   // ok
    var obj = {a: 1, b: 2, c: 3,} // ok
    ```

- Async Functions

  - 建立在 Promise 上的 async / await 處理非同步方法