---
layout: post
title:  "$set, keys, forEach 활용예시"
date:   2021-06-21 00:00:00 +0900
categories: study
tags: [study, vuejs, javascript]
---
기능 설명 : 버튼을 클릭해서 레이어 a를 열 때 b와 c는 닫히고, b를 열 때는 a와 c가 닫혀야 함

```html
<el-button @click="toggleShow(shop_obj, shop_key)">{{shop_value.breed_name}}</el-button>
```

방법 1 (keys와 forEach 사용 - 배열을 계속 돌리기 때문에 데이터 양이 많으면 비효율적)

//데이터(a,b,c 배열 안에 각각의 프로퍼티가 있음)
```javascript
 data() {
    return {
      shop_obj: {}
    }
  },
```

//메소드
```javascript
  methods: {
    toggleShow(target, key) {
      console.log(target);

      Object.keys(target).forEach(el => { 
        console.log(target[el])
        if(el != key) {
          target[el].show = false;
        }
      });
      //Object.keys() : 객체의 프로퍼티 불러오기. 여기서는 target 객체의 프로퍼티를 모두 가져 올 수 있음
      //forEach() : 배열순회. 여기서는 target의 배열을 순회하여 el 이라는 이름을 부여하여 함수 실행.
      //            el => 다음 실행할 함수가 여러줄일 경우 { } 사용.
      //console.log(target[el]) : el 콘솔 뽑아보기 
      //if 이하 : el 값과 key가 다르면 (열린 레이어가 열려고 버튼을 누른 레이어와 다르면) 
      //          target[el]에서 show프로퍼티를 찾아 false로 만든다(누른 거 빼고 나머지 다 닫는다)

      let obj = Object.assign({}, target[key]); // Object.assign({}, key) : 타겟의 key의 값을 빈 배열에 복사하고
      obj.show = !obj.show; //toggle
      this.$set(target, key, obj); //$set : target의 key에서 변한 obj 값을 현재 타겟에 전달(배열의 내부에서 변한 걸 모르기 때문) 

    }
  }
```

방법 2 (데이터 값만 비교하면 되기 때문에 제일 효율적)  

//데이터(방식은 위와 동일)
```javascript
  data() {
    return {
      openTransitionKey: '', //현재 상태를 알기 위한 데이터값
      shop_obj: {}
    }
  },
```

//메소드
```javascript
 methods: {
    toggleShow(target, key) {
      console.log(target);
      console.log(this.openTransitionKey, key)


      if(this.openTransitionKey != key) {
        let new_obj = Object.assign({}, target[this.openTransitionKey]);
        new_obj.show = false;
        this.$set(target, this.openTransitionKey, new_obj)
      }
      // 데이터 openTransitionKey 의 값이 key와 다를 때 (누른 것과 열린 것이 다를 때 - 토글 때문에 해당 조건 필요)
      // target의 openTransitionKey의 값을 new_obj라는 이름으로 저장
      // .show 프로퍼티에 false(안보이게) 부여 - 누른 거 빼고 나머지 레이어 다 안보이게
      // 그리고 $set을 통하여 target에 openTransitionKey에 new_obj 값을 전달.
      


      let obj = Object.assign({}, target[key]);
      obj.show = !obj.show; //toggle
      this.$set(target, key, obj);


      this.openTransitionKey = key //openTransitionKey값을 key값과 동일하게 맞춰서 누른 것만 열리게끔.
    }
  }
}
```

