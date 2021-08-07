#기본검색 SELECT

예제1. <사원>테이블의 모든 튜플을 검색하시오

<pre><code>
SELECT *FROM 사원;
SELECT 사원* FROM 사원;
SELECT 이름,부서,생일,주소,기본급 FROM 사원
SELCT 사원.이름,사원.부서,사원.생일,사원.주소,사원.기본급 FROM 사원;
</code></pre>

예제2. <사원>테이블에서 '주소'만 검색하되 같은 '주소'는 한번만 출력하시오.
<pre><code>
SELECT DISTINCT 주소
FROM 사원;
</code></pre>

예제3. <사원>테이블에서 '기본급'에 특별수당 10을 더한 월급을 "XX부서의 XXX의 월급 XXX"형태로 출력하시오.
<pre><code>
SELECT 부서 + '부서의' AS 부서2, 이름 + '의 월급' AS 이름2, 기본급+10 AS 기본급2
FROM 사원;

#조건 지정 검색 WHERE
WHERE절에 조건을 지정하여 조건에 만족하는 튜플만 검색한다!

예제1. <사원>테이블에서 '기획'부의 모든 튜플을 검색하시오.
<pre><code>
SELECT *
FROM 사원
WHERE 부서='기획'
</code></pre>

d