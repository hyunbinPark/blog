---
title: "Browserify 나 Webpack 을 사용해 bundle 하는 이유 "
date: 2019-01-24 13:14:21 -0400
categories: Study
---
Webpack과 Browserify는 Javascript module Dependency를 관리하는 도구이다.
NodeJS 코드를 다루는 상황이 많아지고 있어 모듈관리를 한가지 스타일로 유지하고 싶을때 사용한다.

이것을 사용할 경우, 
  또한 추가적으로 여러개의 javascript 파일을 브라우져에서 로딩하는 것은 그만큼 네트워크 비용이 많아진다.하지만 위와같은 빌드툴을 통해 여러개의 js 파일을 하나의 js 파일로 
  bundle하여 로드할경우 네트워크 비용을 절약할수 있다. 또한 다수의 js 파일을 개발자의 실수로 잘못 작성할 경우 서로의 스코프를 침범하여 변수 충돌의 위험이 있다.

