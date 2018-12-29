<h2>1. 문자열 내 마음대로 정렬하기</h2><br>


~~~
function solution(strings, n) {
    strings.sort((a,b)=>{
        if(a[n] == b[n]) solution(strings, ++n);
        return (!a[n] || !b[n])? 0 : +(a[n]>b[n]);
    }
    );
    
    return strings;
}
~~~

<br><p>다음에 재도전 할 것.</p><br>

<br><h2>2. 자연수 뒤집어 배열로 만들기</h2><br>


~~~
function solution(n) {
    return `${n}`.split("").reverse().map((v)=> {return parseInt(v)});
}
~~~
