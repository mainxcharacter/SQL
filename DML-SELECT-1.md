<h1>기본검색 SELECT</h1>

예제1. <사원>테이블의 모든 튜플을 검색하시오

<pre><code>SELECT *FROM 사원;
SELECT 사원* FROM 사원;
SELECT 이름,부서,생일,주소,기본급 FROM 사원
SELCT 사원.이름,사원.부서,사원.생일,사원.주소,사원.기본급 FROM 사원;
</code></pre>

예제2. <사원>테이블에서 '주소'만 검색하되 같은 '주소'는 한번만 출력하시오.
<pre><code>SELECT DISTINCT 주소
FROM 사원;
</code></pre>

예제3. <사원>테이블에서 '기본급'에 특별수당 10을 더한 월급을 "XX부서의 XXX의 월급 XXX"형태로 출력하시오.
<pre><code>SELECT 부서 + '부서의' AS 부서2, 이름 + '의 월급' AS 이름2, 기본급+10 AS 기본급2
FROM 사원;
</code></pre>

<h1>조건 지정 검색 WHERE</h1>
WHERE절에 조건을 지정하여 조건에 만족하는 튜플만 검색한다!

예제1. <사원>테이블에서 '기획'부의 모든 튜플을 검색하시오.
<pre><code>SELECT *
FROM 사원
WHERE 부서='기획';
</code></pre>

예제2. <사원>테이블에서 "기획" 부서에 근무하면서 "대흥동"에 사는 사람의 튜플을 검색하시오.
<pre><code>SELECT *
FROM 사원
WHERE 부서 = '기획' AND 주소= '대흥동';
</code></pre>

예제3. <사원>테이블에서 '부서'가 "기획"이거나 "인터넷"인 튜플을 검색하시오.
<pre><code>SELECT *
FROM 사원
WHERE 부서='기획' OR 부서='인터넷';
</code></pre>

예제4. <사원>테이블에서 성이 '김'인 사람의 튜플을 검색하시오
<pre><code>SELECT *
FROM 사원
WHERE 이름 LIKE "김%";
</code></pre>

예제5. <사원> 테이블에서 '생일'이 '01/01/69'에서 '12/31/73' 사이인 튜플을 검색하시오
<pre><code>SELECT *
FROM 사원
WHERE 생일 BETWEEN #01/01/69# AND #12/31/73#;
</code></pre>

예제6. <사원>테이블에서 '주소'가 NULL인 튜플을 검색하시오.
<pre><code>SELECT *
FROM 사원
WHERE 주소 IS NULL;
</code></pre>

<h1>정렬 검색</h1>
OREDER BY 절에 특정 속성을 지정하여 지정된 속성으로 자료를 정렬하여 검색한다.

예제1. <사원> 테이블에서'주소'를 기준으로 내림차순 정렬시켜 상위 2개 튜플만 검색하시오
<pre><code>SELECT TOP 2*
FROM 사원
WHERE 주소 DESC;
</code></pre>

예제2. <사원>테이블에서 '부서'를 기준으로 오름차순으로 정열하고, 같은 '부서'에 대해서 '이름'을 기준으로 내림차순 정렬시켜서 검색하시오.
<pre><code>SELECT *
FROM 사원
WHERE 부서 ASC, 이름 DESC;
</code></pre>

<h1>하위 질의</h1>
하위질의는 <h3>조건절에 주어진 질의를 먼저 수행</h3>하여 그 검색 결과를 조건절의 피연산자로 사용한다.

예제1)"취미"가 나이트댄스인 사원의 이름과 주소를 검색하시오.
<pre><code>SELECT 이름, 주소
FROM 사원
WHERE 이름 = (SELECT 이름 FROM 여가활동 WHERE 취미='나이트댄스');
</code></pre>

예제2)취미활동을 하지 않는 사원들을 검색하시오.
<pre><code>SELECT *
FROM 사원
WHERE 이름 NOT IN (SELECT 이름 FROM 여가활동);
//NOT IN( ) 은 포함되지 않는 데이터를 의미한다. 즉 사원 테이블에서 모든 자료를 검색하는데, 여가활동 테이블에 이름이 있는 자료는 제외하고 검색
</codE></pre>

예제3) 취미활동을 하는 사원들의 부서를 검색하시오.
<pre><code>SELECT *
FROM 사원
WHERE EXIST (SELECT 이름 FROM 여가활동 WHERE 여가활동.이름=사원.이름);
</codE></pre>

<h1>복수 테이블 검색</h1>
여러 테이블을 대상으로 검색을 수행한다.
예제1) "경력"이 10년 이상인 사원의 '이름','부서','취미','경력'을 검색하시오.

<pre><code>SELECT 사원.이름, 사원.부서, 여가활동.취미, 여가활동.경력
FROM 사원, 여가활동
WHERE 경력 >= 10 AND 사원.이름=여가활동.이름;</code></pre>
