---
layout: post
title:  "엘리먼트 width(or height)값 조절"
date:   2021-06-07 00:00:00 +0900
categories: study
tags: [study, vuejs]
---

##### 이미지 4:3 비율 유지

```javascript
  data() {
    return {
      elementHeight: ''
    }
  },
```
데이터 정의 (초기값 부여)

```javascript
  mounted() {
    this.$nextTick(function(){
      window.addEventListener('resize', this.getElementHeight);
      //윈도우 리사이즈 시에 함수 실행
      this.getElementHeight()
      //윈도우 로드 시에 함수 실행
    });
  },


  beforeDestroy(){
    window.removeEventListener('resize', this.getElementHeight);
  },


  methods: {
    getElementHeight(event) {
      
      this.elementHeight = document.getElementsByClassName('el-upload--picture-card')[0].offsetWidth;
      this.elementHeight = this.elementHeight /4 * 3; //4:3 비율
      console.log('need width', this.elementHeight)
      // el-upload-list__item
      document.getElementsByClassName('el-upload--picture-card')[0].style.height = this.elementHeight + 'px';
      //class는 배열로 가져와야 함
      var setHeight = document.getElementsByClassName('el-upload-list__item');
      console.log('setHeight.length', setHeight.length)
      for(var i = 0; i < setHeight.length; i++) {
        console.log(i)
        setHeight[i].style.height  = this.elementHeight + 'px';
      }
    }
  }
```


