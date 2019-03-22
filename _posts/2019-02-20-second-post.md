---
title: "Jpa Repository field underscore ( _ ) 처리"
date: 2019-02-20 10:47:45 -0400
categories: error
---


Jpa Repository 에서 Query를 사용할 때, 테이블의 field 이름에 underscore(_) 이 붙어있을 경우 Jpa interface 에서 에러가 야기된다. 
따라서 실제 field name 과 내부 처리용 field를 model에서 재정의해서 해결한다.
 

 
```
  @Column(name = "municipal_id", nullable = false)
  private Integer municipalId; // <-- field was renamed
  
```
