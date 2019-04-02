<h2>Array.prototype.map()</h2>
<p>The map() method is used to apply a function on every element in an array. A new array is then returned.</p>
<p>map 메소드는 배열의 모든 인자에 적용되며 새로운 배열을 리턴한다.</p>

~~~
let oldArr = [1,2,3,4];
let newArr = oldArr.map((value, index, array) => {
  return {
    value,
    index,
    array
  }
})
~~~

<p>newArr : 반환된 결과 배열을 받는 변수</p>
<p>oldArr : 참조할 배열</p>
<p>value : 참조한 배열의 각 인자를 순차적으로 반환한다.</p>
<p>index : 순차적으로 인덱스를 반환한다.</p>
<p>array : 참조한 배열</p>
<p>Allow function을 사용할 시 'return'을 붙이지 않아도 된다. 조건의 끝에 ';'를 붙이지도 않는다.</p>

<h2>Array.prototype.filter()</h2>
<p>The filter() method returns a new array created from all elements that pass a certain test preformed on an original array.</p>
<p>filter 메소드는 배열의 모든 인자에 적용되며 조건이 맞는 인자들로 새로운 배열을 리턴한다.</p>

~~~
let newArr = oldArr.filter((value, index, array) => {
  return {
    //something
  }
});
~~~



<h2>Array.prototype.reduce()</h2>
<p>The reduce() method is used to apply a function to each element in the array to reduce the array to a single value.</p>
<p>reduce 메소드는 각 인자들의 연관성으로 무언가 새로운 값을 만들때 사용한다.</p>

~~~
let newArr = oldArr.reduce((accumulator, value, index, array) => {
  return {
    //something
  }
}, initValue);
~~~

<p>accumulator : 콜백 함수에 의해 리턴된 값이다.</p>
