# DDL Data Define Language
DB구조, 데이터 형식, 접근 방식 등 DB를 구축하거나 수정할 목적으로 사용하는 언어.
DDL은 번역한 결과가 데이터 사전(Data Dictionary)이라는 특별한 파일에 여러개의 테이블로서 저장된다.
DDL에는 CREATE SCHEMA, CREATE DOMAIN CREATE TABLE, CREATE VIEW, CREATE INDEX, ALTER TABLE, DROP등이 있다.<br>

<h1>CREATE SCHEMA</h1>

스키마를 정의하는 명령문이다. 스키마 이름과 소유권자나 허가권자를 정의한다.<br>
<pre><code>CREATE SCHEMA 스키마명 AUTHORIZATION 사용자_id;</code></pre> 
EX) 소유권자의 사용자 ID가 "홍길동"D인 스키마 "대학교"를 정의하는 SQL문
<pre><code>CREATE SCHEMA 대학교 AUTHORIZATION 홍길동;</code></pre>

<h1>CREATE DOMAIN</h2>
도메인을 정의하는 명령문
*임의의 속성에서 취할 수 있는 값의 범위가 SQL에서 지원하는 전체 데이터 타입의 값이 아니고 일부분 일때, 사용자는 그 값의 범위를 도메인으로 정의할 수 있다.
*정의된 도메인명은 일반적인 데이터 타입처럼 사용한다.
<pre><code>CREATE DOMAIN 도메인명 [AS]* 데이터_타입
[DEFAULT 기본값]
[CONSTRAINT 제약조건명 CHECK(범위값)];</code></pre> 

데이터 타입: SQL에서 지원하는 데이터 타입 <br>
기본값: 데이터를 입력하지 않았을 때 자동으로 입력되는 값

EX)성별을 남또는 여와 같이 정해진 1개의 문자로 표현되는 도메인 SEX를 정의하는 SQL문

<pre><code>CREATE DOMAIN [DOMAIN CHAR(1)
[DEFAULT '남'
CONSTRAINT VALID-SEX CHECK(VALUE IN ('남','여); 제약조건명 CHECK(범위값)];</code></pre> 

<h1>CREATE TABLE</h1>
테이블을 정의하는 명령문
<pre><code>CREATE TABLE 테이블명
  (속성명 데이터_타입 [DEFAULT 기본값][NOT NULL],[,PRIMARY KEY(기본키, 속성명)][,UNIQUE(대체키_속성명)]<br>
  [,FOREIGN KEY(외래키_속성명)][REFERENCES 참조테이블(기본키_속성명)][ON DELETE 옵션][ON UPDATE 옵션][,CONSTRAINT 제약조건명][CHECK(조건식)]);</code></pre> 
  
  -PRIMARY KEY:기본키로 사용할 속성 또는 속성의 집합을 지정<br>
  -UNIQUE:대체키로 사용할 속성 또는 속성의 집합을 지정하는 것으로 유니크로 지정한 속성은 중복된 값을 가질 수 없다.<br>
  -FOREIGN KEY ~REFERENCES~ : 참조할 다른 테이블과 그 테이블을 참조할 때 사용할 외래키 속성을 지정한다.<br>
      *NO ACTION:참조테이블에 변화가 있어도 기본 테이블에는 아무런 조취를 취하지 않는다.<br>
      *CASCADE:참조 테이블의 튜플이 삭제되면 기본 테이블의 관련 튜플도 모두 삭제되고, 변경되면 속성 값도 모두 변경
      *SET NULL:참조 테이블에 변화가 있으면 기본 테이블의 관련 튜플의 속성 값을 NULL로 변경
      *SET DEFAULT:참조 테이블에 변화가 있으면 기본 테이블의 관련 튜플의 속성을 기본값으로 변경
      
  -CONSTRAINT : 제약 조건의 이름을 짖정한다. 이름을 지정할 필요가 없으면 CHECK절만 사용하여 속성 값에 대한 제약 조건을 명시한다
  -CHECK: 속성 값에 대한 제약 조건을 정의한다.
  
  <h1>CREATE VIEW</h2>
  뷰를 정의하는 명령문
  <pre><code>CREATE VIEW 뷰명[(속성명[,속성명,...])]
  AS SELECT문;</code></pre>
  
  > VIEW 그게 뭔데... 어떻게 하는건데...?
  > 하나 이상의 기본 테이블로부터 유도되는 이름을 갖는 가상 테이블입니다. <br>
  > 테이블은 물리적으로 구현되어 실제로 데이터가 저장되지만, 뷰는 물리적으로 구현되지 않습니다. 
  <고객> 테이블에서 '주소'가 '안산시'인 고객들의 '성명'과 '전화번호'를 '안산고객'이라는 뷰로 정의하시오.
  <pre><code>
  CREATE VIEW 안산고객(성명, 전화번호)
  AS SELECT 성명, 전화번호
  FROM 고객
  WHERE 주소='안산시'
  </code></pre>
  
  <h1>CREATE INDEX</h1>
  인덱스를 정의하는 명령문
  <pre><code>CREATE [UNIQUE] INDEX 인덱스명
  ON 테이블명(속성명[ASC|DESC][,속성명[ASC|DESC]])
  [CLUSTER];
  </pre></code>
  
  * UNIQE
  > 사용된 경우: 중복값이 없는 속성으로 인덱스를 생성한다
  > 중복값을 허용하는 속성으로 인덱스를 생성한다
  * 정렬여부지정
  >ASC:오름차순 정렬
  >DESC:내림차순 정렬
  >생략된경우:오름차순으로 정렬
  * CLUSTER : 사용하면 인덱스가 클러스터드 인덱스로 설정됨
  
  EX)<고객>테이블에서 UNIQUE한 특성을 갖는 '고객번호' 속성에 대해 내림차순으로 정렬하여 고객번호_ixs라는 이름으로 인덱스를 정의하시오
  <pre><code>CREATE UNIQUE INDEX 고객번호_idx
  ON 고객(고객번호 DESC);</code></pre>
  
  <h1>ALTER TABLE</h1>
  테이블에 대한 정의를 변경하는 명령문입니다...~
  >ALTER TABLE 테이블명 ADD 속성명 데이터_타입 [DEFAULT'기본값'];
  >ALTER TABLE 테이블명 ALTER [SET DEFAULT '기본값'];
  >ALTER TABLE 테이블명 DROP COLUMN 속성명 [CASCADE];
  * ADD :새로운 속성(열)을 추가할 때 사용한다.
  * ALTER :특정 속성의 Default값을 변경할 때 사용한다.
  * DPRO COLUM: 특정 속성을 삭제할때 사용한다.

예제1) <학생>테이블에 최대 3문자로 구성되는 '학년' 속성을 추가하시오
<pre><code> ALTER TABLE 학생 ADD 학 VARCHAR(3);</pre></code>
예제2) <학생>테이블의 '학번' 필드의 데이터 타입과 크기를 VARCHAR(10)으로 하고 NULL값이 입력되지 않도록 변경
<pre><code> ALTER TABLE 학생 ALTER학번 VARCHAR(10) NOT NULL;</pre></code>

<h1>DROP</h1>
DROP은 스키마, 도메인, 기본 테이블, 뷰테이블, 인덱스, 제약 조건등을 <h3>제거</h3>하는 명령문이다
<pre><code>
DROP SCHEMA 스키마명 [CASCADE | RESTRICT];
DROP DOMAIN 도메인명 [CASCADE | RESTRICT];
DROP TALBE 테이블명 [CASCADE | RESTRICT];
DROP VIEW 뷰명 [CASCADE | RESTRICT];
DROP INDEX 인덱스명 [CASCADE | RESTRICT];
DROP CONSTRAINT 제약조건명;
</pre></code>


