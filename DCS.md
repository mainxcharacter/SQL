#DCL

GRANT:권한 부여를 위한 명령어<br>
REVOKE:권한 취소를 위한 명령어<br>
사용자 등급 지정 및 해제<br>

* GRANT 사용자등급 TO 사용자_ID_리스트 [IDENTIFIED BY 암호];
* REVOKE 사용자등급 FROM 사용자_ID_리스트;

예제1) 사용자 ID가 "NABI"인 사람에게 데이터베이스 및 테이블을 생성할 수 있는 권한을 부여하는 SQL문을 작성하시오
<pre><code> GRANT RESOURCETO NABI;<pre></code>
예제2) 사용자 ID가 "STAR"인 사람에게 단순히 데이터베이스에 있는 정보를 검색할 수 있는 권한을 부여하는 SQL문
<pre><code> GRANT CONNECT TO STAR;<pre></code>

테이블 및 속성에 대한 권한 부여 및 취소

* GRANT 권한_리스트 ON 개체 TO 사용자 [WITH OPTION];
* REVOKE [GRANT OPTION FOR] 권한_리스트 ON 개체 FROM 사용자 [CASECAD]; //WITH GRANT OPTION:부여받은 권한을 다른 사용자에게 다시 부여할 수 있는 권한

예제3) 사용자 ID가 NABI인 사람에게 <고객>테이블에 대한 모든 권한과 다른 사람에게 권한을 부여할 수 있는 권한까지 부여하는 SQL문을 작성하시오
GRANT ALL ON 고객 TO NABI WITH GRANT OPTION;

예제4) 사용자 ID가 STAR인 사라에게 부여한 <고객> 테이블에 대한 권한 중 UPDATE권한을 다른 사람에게 부여할 수 있는 권한만 취소하는 SQL문을 작성하시오,.
REVOKE GRANT OPTION FOR UDATE ON 고객 FROM STAR

<h1>COMMIT</h1>
트랜잭션이 성공적으로 끝나면 데이터베이스가 새로운 일관성 상태를 가지기 위해 변경된 모든 내용을 DB에 반영해야됌.
이때 사용하는 명령어가 커밋!

<h1>ROLLBACK</h1>
ROLLBACK은 아직 COMMIT되지 않은 변경된 모든 내용들을 취소하고 데이터베이스를 이전 상태로 되돌리는 명령어!

<h1>SAVEPOINT</h1>
트랜잭션 내에 롤백할 위치인 저장점을 지정하는 명령어이다. 저장점을 지정할때는 이름을 부여하며, rollback시 지정된 저장점까지의 트랜잭션 처리 내용이 취소된다.
