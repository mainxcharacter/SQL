#DML
Data Manipulation Language 데이터 조작어

>SELECT 테이블에서 튜플검색
>INSERT 테이블에 새로운 튜플 삽입
>DELETE 테이블에서 튜플 삭제
>UPDATE 테이블에서 튜플 내용 갱신

<h1>INSERT INTO~ 삽입문</h1>
<pre><code>INSERT INTO 테이블명([속성명1, 속성명2, ...])
VALUES(데이터1, 데이터2,...);
</pre></code>

예)<사원>테이블에 이름:홍승현, 부서:인터넷)을 삽입하시오
<pre><code>INSERT INTO 사원(이름,부서) VALUES('홍승현','인터넷');</pre></code>

예)<사원>테이블에 (장보고,기획,05/03/73, 홍제듣, 90)을 삽입하시오.
<pre><code>INSERT INTO 사원 VALUES('장보고','기획',#05/03/73#, '홍제동',90);</pre></code>

예)<사원>테이블에 있는 편집부의 모든 튜플을 편지부원(이름, 생일, 주소, 기본급)테이블에 삽입하시오.
<pre><code>
INSERT INTO 편집부원(이름,생일,주소,기본급)
SELECT 이름, 생일, 주소, 기본급
FROM 사원
WHERE 부서='편집'
</pre></code>

<h1>DELETE FROM~ 삭제문</h1>
<pr><code>
DELETE
FROM 테이블명
[WHERE 조건];
<pr></code>
>모든 레코드를 삭제할 때는 WHERE절 생략
>완전히 제거하는 DROP과는 다르다.

예제1)<사원>테이블에서 "임꺽정"에 대한 튜플을 삭제하시오.
<pre><code>
DELETE 
FROM 사원
WHERE 이름='임꺽정'
</code></pre>

예제2) <사원>테이블에서 "인터넷"부서에 대한 모든 튜플을 삭제하시오
<pre><code>
DELETE
FROM 사원
WHERE 부서="인터넷"
</code></pre>

<h1>UPDATE~ SET~ 갱신문</h1>
갱신문은 기본 테이블에 있는 튜플들 중에서 특정 튜플의 내용을 변경할 때 사용한다.
<pre><code>
UPDATE 테이블명
SET 속성명 = 데이터[,속성명=데이터,...]
[WHERE 조건];

예제1) <사원>테이블에서 "홍길동"의 '주소'를 "수색동"으로 수정하시오
<pre><code>
UPDATE 사원
SET 주소='수색동'
WHERE 이름='홍길동'
</pre></code>

예제2) <사원>테이블에서 "황진이"의 '부서'를 "기획부"로 변경하고 '기본급'을 5만원으로 인상시키시오
<pre><code>
UPDATE 사원
SET 부서='기획부',기본급=기본급+5
WHERE 이름='황진이'
