---
title: arguments부터 생성자와 new까지
date: 2019-11-05
categories: 생코
---

# arguments
    a+=1 > a=a+1이라는 의미
    a+=5면 a=a+5라는 의미
    arguments는 함수 인자의 배열(같은 것)
    
# 매개변수의 수
    함수의 이름.length는 함수에 정의된 인자의 (매개변수의 개수)를 보여준다.
    arguments.length는 함수로 전달된 실제 인자의 개수를 보여준다.
    이 두 개의 개수가 다르다는 건,
    인자를 내가 원하지 않 개수만큼 적었다는 의미니까
    (원하는 개수= 매개변수)
    경고창이 뜨도록 활용해볼 수 있다.

# 함수의 호출
    함수를 호출하는 다른 방법으로 apply가 있다.
    함수도 객체이다.
    함수에서 쓸 수 있는 내장 메소드가 있다.
    apply도 그 중 하나다.
        function sum(arg1, arg2){
        return arg1+arg2;
        }
        alert(sum.apply(null, [1,2]))
    이렇게 apply를 쓸 수 있다.
    그런데 이렇게 앞 인자에 null을 쓴 상태로 보면 그냥 함수를 쓰는 거랑 다른 게 없는데도 훨씬 불편하다.
    null이 아닌 걸 쓸 때를 알아보자.
    
# apply의 사용
      o1 = {val1:1, val2:2, val3:3}
      o2 = {v1:10, v2:50, v3:100, v4:25}
      function sum() {
        var _sum=0;
        for(name in this) {
          _sum += this[name];
        }
        return _sum;
      }
      alert(sum.apply(o1)); //6
      alert(sum.apply(o2)); //185
    
    객체를 인자로 쓸 때 apply를 쓰는 것인가?
      
      function sum() {
        var _sum=0;
        for(name in this) {
          if(typeof this[name] !== 'function'
            _sum += this[name];
        }
        return _sum;
      }
      o1 = {val1:1, val2:2, val3:3, sum:sum}
      o2 = {v1:10, v2:50, v3:100, v4:25, sum:sum}
      alert(o1.sum()); //6
      alert(o2.sum()); //185
    apply 없이 쓰는 법
    그러려면 조건문도 추가하는 등 귀찮아지니까 apply를 쓰는 게 더 편하다!
