# 데이터베이스 part2

# 3장 SQL

## 데이터 베이스 언어

데이터 베이스를 효과적으로 다룰 수 있게 하는 언어.

기능의 관점에서 보면 3가지 종류로 나뉠 수 있다.

- DDL(Data-definition language): **스키마를 정의**하는 기능. `Data dictionary`에 스키마의 설정 값들을 테이블의 형태로 저장한다.
  - CREATE: 정의
  - ALTER: 수정
  - DROP: 삭제
  - TRUNCATE: DROP 후 CREATE
- DML(Data-manipulation language): 데이터 인스턴스를 검색하고 조작하는 기능. `Query language`라고도 한다.
  - SELECT: 조회
  - INSERT: 추가
  - DELETE: 삭제
  - UPDATE: 변경
- DCL(Data-control language): 위의 두개에 속하지 않는 기능들을 제공.
  - COMMIT: 트랜잭션의 작업 결과를 반영
  - ROLLBACK: 트랜잭션의 작업을 취소 및 원래대로 복구
  - GRANT: 사용자에게 권한 부여
  - REVOKE: 사용자 권한 회수
  - Translation Start / End
  - Session Start / End
  - Backup / Recovery
  - User account management

또 객체를 표현하는 관점으로 보면 2가지로 나뉜다.
- 절차형 언어(Procedural language)
- 비절차형 언어(= 선언적 언어): 데이터를 어떻게 얻을지 명시하지 않음.

## SQL의 특성

- DDL의 특성을 가지고 있음
  - `스키마`, `도메인` 정의
  - 무결성 제약 조건
  - 각 `릴레이션`에서 유지하여야 할 `인덱스`들의 집합
  - 각 `릴레이션`의 보안과 권한 정보
  - 각 `릴레이션`의 디스크에서의 물리적인 저장 구조
- SQL 이름은 **대소문자를 가리지 않는다**. 그러나 `single/double quotation`에서는 가림.

## Drop vs. Delete

- `Drop`: DDL 부분으로 테이블의 스키마 자체가 삭제.
- `Delete`: DML 부분으로 인스턴스가 삭제된다.

> DDL 부분의 키워드에는 `CREATE`, `ALTER`, `DROP`이 있다.
> DML 부분의 키워드에는 `SELECT`, `INSERT`, `DELETE`, `UPDATE`가 있다.

## 기본 구조

SQL 문의 기본 구조는 `select`, `from`, `where`의 세 개의 절로 이루어진다.

- select: 관계 대수에서 `추출(projection)` 연산과 일치. 쿼리 결과 **나타나길 바라는 속성**들을 나열할 때 사용.
- from: 관계 대수의 `카티션곱(Cartesian product)`에 해당. 쿼리문에서 **찾아보기를 원하는 릴레이션**을 나열.
- where: 관계 대수에서 `선택 조건`에 해당. from 절에 나타나는 **릴레이션들의 속성들의 조건**으로 구성.

> SQL은 `set`을 기반으로 만들어져 이론적으로는 중복을 허용하면 안되지만, **성능상의 이유**로 중복을 허용한다. 중복을 원치 않으면 `distinct`를 사용.

## SQL 수행 모델

1. FROM: "from"절에 명시된 특정 테이블로부터 **하나의 튜플씩** 뽑아낸다.
2. WHERE: 조건에 맞는 데이터(튜플)만 가져온다.
3. GROUP BY: 어떤 조건에 따라 자료를 그룹화한다.
4. HAVING: 그룹화된 데이터에서 조건에 맞는 것만 추출한다.
5. SELECT: 추출된 릴레이션에서 "select"절에 명시된 속성의 `컬럼`을 선택하고
6. ORDER BY: 기준에 따라 정렬한다.

다 마친 후 사용자에게 데이터가 보이게 된다.

## Null 값

모든 튜플은 `null` 값을 가질 수 있다. 이것의 의미는 **알지 못하는 값** 또는 **존재하지 않는 값**이라는 뜻이다.

`null` 값이 들어감에 따라 특징이 몇 가지 있다.

- arithmetic 연산에서 `null` 값이 들어갈 경우 항상 `null`을 반환.
- `is null` predicate를 통해 null 값을 체크 할 수 있다.
- 비교 연산에서는 항상 `unknown`을 반환.
