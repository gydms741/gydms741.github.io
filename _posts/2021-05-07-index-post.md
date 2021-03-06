---
title: "sql에서의 index"
date: 2021-05-07 23:40:28 -0400
categories: sql
---

### index란?

- index는 RDBMS에서 검색 속도를 높이기 위한 기술이다. 다시 말해 데이터를 빠르게 찾을 수 있는 수단으로서, 테이블에 대한 조회 속도를 높여 주는 자료구조를 일컫는다.

### Index 사용이유

- Where 구문과 일치하는 열을 빨리 찾기 위해
- 특정 열을 고려 대상에서 빨리 없애기 위해
- 조인을 실행할 때 다른 테이블에서 열을 추출하기 위해
- 특정하게 인덱스된 컬럼을 위한 MIN() 또는 MAX() 값을 찾기 위해

Index 장점

- 키 값을 기초로 하여 테이블에서 검색과 정렬 속도를 향상시킨다
- 질의나 보고서에서 그룹화 작업의 속도를 향상시킨다
- 인덱스를 사용하면 테이블 행의 고유성을 강화시킬 수 있다.

Index 단점

- Index 생성시 .mdb 파일 크기가 증가한다.
- 한 페이지를 동시에 수정할 수 있는 병행성이 줄어든다.
- Index 된 Field에서 Data를 업데이트하거나, Record를 추가 또는 삭제시 성능이 떨어진다.
- 데이터 변경 작업이 자주 일어나는 경우, Index를 재작성해야 하므로 성능에 영향을 미친다.
- Index를 생성하는데 시간이 많이 소요될 수 있다.

### Index 생성 문법

CREATE [UNIQUE] INDEX <index_name> ON <table_name> (<column(s)>);
