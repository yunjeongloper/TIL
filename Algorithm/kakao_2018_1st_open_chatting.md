# 2019 카카오 신입 공채 1차 코딩 테스트 1. 오픈채팅방

[2018 카카오 신입 공채 알고리즘 문제&해설](http://tech.kakao.com/2018/09/21/kakao-blind-recruitment-for2019-round-1/)
바로 코드를 짰으나 테스트 예제에서만 성공하는 코드가 완성되었다. (안습) 해설을 보고나서야 놓친 부분을 찾았다. ㅠㅠ
js 알고리즘을 짜기 위해선 object, array에 대한 이해가 더 필요할 것 같다. 조금 더 익숙한 Java와 javascript 사이에서 고민했으나 스크립트 언어가 너무너무 좋은 나는 js로 결정!
먼저 내가 테스트를 통과시킨 코드이다

```javascript
function solution(record) {
    var answer = [];

    var recordSplited = record.map(i => i.split(" "));
    var rule = [{eng: 'Enter', kor : '들어왔습니다.'},
                {eng: 'Leave', kor: '나갔습니다.'}];
    var name = {};

    // push lastest name by id
    recordSplited.slice().reverse().map(i => {
        if(i[2] && !name[i[1]]) {
            name[i[1]] = i[2]
        }
    })

    // push answer
    recordSplited.map(i => {
        let str = "";
        if(i[0] !== 'Change') {
            str = name[i[1]]+ "님이 "
                + rule.find(k => k.eng === i[0]).kor;
            answer.push(str);
        }
    });

    return answer;
}
```

통과는 했지만 문제가 많았다. 넘나 초심자의 코드
- var 사용을 지양한다는 것을 그냥 써버렸다. 
- 반복함수를 너무 제멋대로 써버렸다. forEach, map, filter함수를 적재적소에 사용하지 못했다.
- 처음에 name을 배열로 선언하여서 ```[{id:'asd',name:'윤정'}, ...] ``` 이렇게 선언하였었는데 배열 내부의 객체에 접근할 때 find를 사용하게 되면서 시간 초과 테스트에서 모두 탈락하게되었다. object의 key와 value를 잘 다루지 못해서 편한대로 했더니 이런 문제가 발생하였다. 더 생각하자 !!!!!
- rule도 object로 선언하면 find함수를 제거할 수 있을것이다.
- <b>더 간결한 코드를 짜기 위해 노력하자.</b>

