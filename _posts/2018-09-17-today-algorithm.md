<h1>프로그래머스 자바스크립트 알고리즘</h1><br>
<h2>1. 완주하지 못한 선수</h2><br>


~~~
function solution(participant, completion) {
    let part_object = builtCharMap(participant);
    let comp_object = builtCharMap(completion);
    console.log(part_object);
    var answer = '';
    
    for(let value in part_object){
        if(part_object[value] !== comp_object[value]){
            return value;
        }    
    }

    return answer;
}

function builtCharMap(array){
    let arrMap = {};
    for(let value of array){
        arrMap[value] = arrMap[value] + 1 || 1;
    }
    return arrMap;
}
~~~


<br><h2>2. 예산</h2><br>


~~~
function solution(d, budget) {
    let count = 0;
    let result = 0;
    d.sort((a,b) => a-b).forEach(function(v){
        budget -= v;
        count++;
        if(budget >= 0) {
            result = count;
        }
        
    })
    
    return result;
}
~~~

