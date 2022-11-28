데이터베이스 정의

데이터의 구조화된 정보 모음

연결된 애플리케이션과 함께 데이터와 데이터베이스관리시스템(DBMS)을 하나로 묶어 데이터베이스라고도 함

​

데이터베이스의 특징

실시간 접근성

지속적인 변화

동시 공유

내용에 대한 참조

데이터 논리적 독립성

자기기술성

중복의 최소화

RAM, ROM 같은 주기억장치가 아닌 컴퓨터에서 사용할 수 있는 보조기억장치에 저장

 

​

데이터베이스 유형

​

관계형 데이터베이스

열과 행이 있는 테이블 집합으로 항목 구성 

정형 정보에 액세스하는 가장 효율적이고 유연한 방법 제공

데이터베이스에 삽입되는 모든 데이터의 구성 방식 정의

객체 지향 데이터베이스

객체 형태로 표현

분산 데이터베이스

서로 다른 사이트에 위치한 둘 이상의 파일로 구성 

데이터 웨어하우스

데이터의 중앙 저장소

빠른 쿼리 및 분석을 위해 특별히 설계된 데이터베이스 유형

NoSQL 데이터베이스

비정형 및 반정형 데이터를 저장, 조작 가능

그래프 데이터베이스

엔티티 및 엔티티 간의 관계 측면에서 데이터를 저장

OLTP 데이터베이스

여러 사용자가 수행하는 많은 수의 트랜잭션을 위해 설계된 고속 분석 데이터베이스

오픈 소스 데이터베이스

소스 코드가 오픈 소스인 시스템

클라우드 데이터베이스

프라이빗, 퍼블릭 또는 하이브리드 클라우드 컴퓨팅 플랫폼에 상주하는 정형 또는 비정형 데이터 모음

다중 모델 데이터베이스

서로 다른 유형의 데이터베이스 모델을 단일 통합 백엔드로 결합

다양한 데이터 유형 수용

문서/JSON 데이터베이스

문서 지향 정보를 저장, 검색 및 관리하도록 설계

자율 운영 데이터베이스

클라우드를 기반

머신러닝을 사용하여 데이터베이스 튜닝, 보안, 백업, 업데이트 및 기타 데이터베이스 관리자가 전통적으로 수행해 온 일상적인 관리 작업을 자동화

​

데이터베이스(Database, DB) 용어

 

스키마(Schema)

데이터베이스를 구성하는 데이터 개체(Entity), 속성(Attribute), 관계(Relationship) 등 데이터베이스 구조를 정의 한 것을 말한다. 사용자의 관점에 따라 외부 스키마, 개념 스키마, 내부 스키마로 구분한다. 데이터베이스관리시스템(DBMS)는 외부 스키마에 명세된 사용자의 요구를 개념 스키마 형태로 변환하고, 이를 다시 내부 스키마 형태로 반환한다. 

외부 스키마(사용자 뷰): 사용자의 입장에서 정의한 데이터 베이스의 논리적 구조. 데이터들을 어떤 형식, 구조, 화면을 통해 사용자에게 보여줄 것인가에 대한 명세를 말하며 하나의 데이터베이스에는 여러개의 외부 스키마가 있을 수 있다. 일반 사용자는 SQL을 이용하여 DB를 쉽게 사용할 수 있다. 응용 프로그래머는 C, 자바 등의 언어를 사용하여 DB에 접근한다. 

개념 스키마(전체적인 뷰): 데이터베이스의 전체적인 논리적 구조. 모든 이용자가 필요로 하는 데이터를 총합한 조직 전체의 데이터 베이스로 하나만 존재한다. 개체 간의 관계와 제약조건, 데이터 베이스의 접근 권한, 보안 등에 관한 명세를 나타낸다. 데이터 베이스 관리자에 의해서 구성된다. 

내부 스키마: 물리적 저장장치의 입장에서 본 데이터베이스 구조. 실제로 데이터베이스에 저장될 레코드의 물리적인 구조, 저장 데이터 항목의 표현 방법, 내부 레코드의 물리적 순서 등을 나타낸다.

​

표(Table)

Relation(= Table): 관계형 데이터 베이스에서 정보를 구분하여 저장하는 기본 단위

Tuple(=Record): 테이블에서 행을 의미. 튜플은 릴레이션에서 같은 값을 가질 수 없다. 튜플의 수는 카디날리티(Cardinality)라고 한다. 

Attribute( =Field): 테이블에서 열을 의미. 같은 말로는 칼럼이라고도 하며 어트리뷰트의 수는 디그리(Degree)라고도 한다. 

식별자(Identifier): 관계형 데이터 베이스에서 각각을 구분할 수 있는 논리적인 개념

​

Key

데이터베이스에서 조건에 만족하는 테이블행(Tuple)을 찾거나 순서대로 정렬할 때 테이블행(Tuple)을 서로 구분할 수 있는 기준이 되는 테이블열(Attribute)

​

후보키(Cardidate Key)

테이블열(Attribute)을 구성하는 속성들 중에서 테이블행(Tuple)을 유일하게 식별하기 위해 사용하는 속성들의 부분집합

기본 키로 사용할 수 있는 속성들을 의미

모든 Relation에는 반드시 하나 이상의 후보키가 존재

​

기본키(Primary Key)

후보키 중에서 선택한 Main Key

한 Relation에서 특정 Tuple을 유일하게 구별할 수 있는 속성

null 값 없음

동일한 값이 중복되어 저장될 수 없음

​

슈퍼키(Super Key)

한 Relation 내에 있는 속성들의 집합으로 구성된  키

유일성을 만족시키지만, 최소성을 만족시키지 못함

ex. 학번 + 주민번호를 사용하여 슈퍼키를 만들면 유일성은 만족하지만, 학번이나 주민번호 하나만 가지고도 다른 튜플들을 구분할 수 있으므로 최소성은 만족시키지 못한다. 

외래키(Foregin Key)

다른 Relation의 기본키를 참조하는 속성의 집합

테이블들 간의 관계를 나타내기 위해서 사용

외래키의 속성의 도메인과 참조되는 기본키 속성의 도메인이 같아야 연관성 있는 투플을 찾기 위한 비교 연산 가능

null값 가질 수 있음 

서로 다른 투플이 같은 값을 가질 수 있음

​

데이터베이스 언어 종류

​

DML, Data Multipulation Language (데이터 조작 언어): 저장된 데이터를 생성 및 변경, 제거하여 처리

DDL, Data Definition Langauge(데이터 정의 언어): 데이터베이스 안의 값들을 변경, 수정, 입력하여 정의

DCL, Data Control Language(데이터 제의 언어): 데이터베이스에 접근하거나 객체에 권한 등을 수정

​

reference

데이터베이스란 | Oracle 대한민국 / 데이터베이스 - 위키백과, 우리 모두의 백과사전 (wikipedia.org) / 데이터베이스 - 나무위키 (namu.wiki) / 코딩의 시작, TCP School / TTA정보통신용어사전