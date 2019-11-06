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
    
# 객체 지향 프로그래밍

    Object Oriented Programming(OOP)
    로직을 상태(state)와 행위(behave)로 이루어진 객체로 만드는 것
    이 객체들을 레고 블럭처럼 조립해서 하나의 프로그램을 만드는 것이 객체지향 프로그래밍
    한 페이지가 글목록, 본문, 댓글로 이루어져있다면, 크게는 세 개의 객체를 만들어서 
    본문 관련 변수와 메소드가 들어있는 객체, 글목록 관련, 댓글 관련 등으로 삼는다. 

# 문법과 설계

    문법은 언어가 제공하는 기능을 익히는 것
    설계는 현실을 중요한 것만 반영해야 한다.
    중요한 것만 반영해서 '추상화'를 만들어야 한다.
    피카소의 소와 같이
    미친 듯이 심플하게
    결국 본질이 중요하다.
    객체지향의 설계 원칙이나 객체 지향의 철학적인 의미는 대단히 중요하지만 
    아직은 지혜를 배울 때가 아니고 지금은 지식을 배우자.

# 부품화
    
    좋은 객체를 만든다는 건 로직을 부품화하는 것
    컴퓨터를 보면 처음에는 모든 출력 기기가 하나였다. 
    그러다가 모니터, 키보드, 마우스 등으로 분류가 되었는데
    그러다가 다시 스마트폰 같이 하나가 되게 되었다.
    부품화도 좋지만 적절함이 먼저인 것이다.
    
    은닉화, 캡슐화

        내부의 동자 방법을 단단한 케이스 안으로 숨기고 
        사용자에게는 그 부품의 사용방법만을 노출하는 것
        제대로된 부푸밍라면 그것이 어떻게 만들어졌는지 몰라도 사용할 수 있다.
    
    인터페이스
        
        USB를 꽂으려면 연결점이 일치해야 한다.
        그러려면 연결점의 모양을 표준에 맞게 만들면 된다.
        이러한 연결점을 인터페이스라고 한다.
        
# 생성자와 new
    
    자바스크립트는 어떠한 객체 지향 언어와도 다른 독특함을 가진다.
    Proto type-based programming 이다.
    
# 객체생성
    서로 연관된 변수와 메소드를 객체라는 그릇에 담는다.
        var person = {}         //객체, 오브젝트
        person.name = 'egoing';         //객체에 담겨진 변수는 프로퍼티
        person.introduce = function() {         //객체에 담겨진 함수는 메소드
            return 'My name is ' +this.name;
        }
        document.write(person.introduce());
        
        다른 방법
        var person = {
            'name' : 'egoing',
            'introduce' : function() {
                return 'My name is '+this.name;
            }
        }
        document.write(person.introduce());
        
    var person1 = {
        'name' : 'egoing';
        'introduce' : function() {
                return 'My name is '+this.name;
            }
        }
        document.write(person.introduce());
        
    var person2= {
        'name' : 'leezhe'
        'introduce' : function() {
                return 'My name is '+this.name;
            }
        }
        document.write(person.introduce());    
        
    중복되는 부분이 있다!
    메소드 부분이 중복된다.
    객체의 구조를 재활용할 방법이 필요하다
    생성자를 사용하면 된다.
    
# 생성자
    
    생성자(constructor)는 객체를 만드는 역할을 하는 함수다.
    
    함수에 new를 붙이면 그 리턴값은 객체다.
    생성자가 객체를 초기화한다.(initialize)
      
        function Person(name){
            this.name = name;
            this.introduce = function(){
                return 'My name is '+this.name; 
            }   
        }
        var p1 = new Person('egoing');
        console.log(p1);   // Person {name: "egoing", introduce: ƒ}

        var p2 = new Person('leezche');
        console.log(p2.introduce());  // My name is leezche
    
    new를 함수에 붙이면 그 함수에 존재하는 변수, 함수들이 객체 속으로 구성원이 되어 들어가는 건가
