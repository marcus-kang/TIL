<h1>[OracleDB]</h1>
<h2>2022-01-26 TIL</h2>
<h3>특정 데이터 우선 정렬방법</h3>
* 링크 참고(https://mjn5027.tistory.com/107)
<hr/>
<h2>2021-11-02 TIL</h2>
<h3>시간대/일자/요일/월별 통계 카운트</h3>

* 시간대별<br>
SELECT TO_CHAR(DATE컬럼, 'HH24') AS 시간대,<br>
      COUNT(TO_CHAR(DATE컬럼, 'HH24')) AS 숫자<br>
FROM 데이터테이블<br>
WHERE #{searchStartDate} <= TO_CHAR(DATE컬럼, 'YYYYMMDD') <br>
AND #{searchEndDate} >= TO_CHAR(DATE컬럼, 'YYYYMMDD')  <br>
GROUP BY TO_CHAR(DATE컬럼, 'HH24') <br>
ORDER BY TO_CHAR(DATE컬럼, 'HH24') ASC <br>

* 일자별<br>
SELECT T1.일자,<br>
     NVL(T2.Y_CNT, 0) AS 숫자<br>
FROM<br>
     (SELECT 일자<br>
       FROM<br>
            (SELECT LPAD(DD, 2, 0) AS 일자<br>
              FROM<br>
                   (SELECT LEVEL AS DD<br>
                     FROM DUAL CONNECT BY LEVEL <= 31<br>
                   )<br>
             WHERE DD <= TO_CHAR(LAST_DAY(TO_DATE(#{searchYear}||#{searchMonth},'YYYYMM')),'DD')<br>
            )<br>
     ) T1, <br>
     (SELECT TO_CHAR(DATE컬럼, 'DD') AS 일자, <br>
               COUNT(TO_CHAR(DATE컬럼, 'DD')) AS 숫자<br>
          FROM 데이터테이블<br>
         WHERE TO_CHAR(DATE컬럼, 'YYYY')  = #{searchYear} <br>
               AND TO_CHAR(DATE컬럼, 'MM')  = #{searchMonth}  <br>
         GROUP BY TO_CHAR(DATE컬럼, 'DD')<br>
        ) T2 <br>
  WHERE T1.일자 = T2.일자(+) <br>
ORDER BY T1.일자 ASC<br>

* 요일별<br>
SELECT TO_CHAR(DATE컬럼, 'D') AS 요일, <br>
      COUNT(TO_CHAR(DATE컬럼, 'D')) AS 숫자<br>
FROM 데이터테이블<br>
WHERE TO_CHAR(DATE컬럼, 'YYYY') = #{searchYear} <br>
AND TO_CHAR(DATE컬럼, 'MM') = #{searchMonth} <br>
GROUP BY TO_CHAR(DATE컬럼, 'D') <br>
ORDER BY TO_CHAR(DATE컬럼, 'D') ASC  <br>

* 월별<br>
SELECT TO_CHAR(DATE컬럼, 'MM') AS 월, <br>
      COUNT(TO_CHAR(DATE컬럼, 'MM')) AS 숫자<br>
FROM 데이터테이블<br>
WHERE TO_CHAR(DATE컬럼, 'YYYY') = #{searchYear}  <br>
GROUP BY TO_CHAR(DATE컬럼, 'MM') <br>
ORDER BY TO_CHAR(DATE컬럼, 'MM') ASC<br>
<hr/>
<h2>2021-02-03 TIL</h2>
<h3>USER 비밀번호 변경방법</h3>
* 링크 참고(https://kyome.tistory.com/6)
<hr/>
<h2>2021-01-18 TIL</h2>
<h3>PLAN, TRACE 읽는 법</h3>
* 링크 참고(https://devstarsj.github.io/devlopment/2016/02/20/Oracle.read.plan.trace/)
<hr/>
<h2>2020-12-20 TIL</h2>
<h3>2개 이상의 SELECT 결과 합치기</h3>
컬럼의 수와 데이터타입이 같은 2개 이상의 SELECT 결과는 UNION 명령어를 추가하여 합칠 수 있다.<br/>
* 링크 참고(https://dpdpwl.tistory.com/98)
<hr/>
<h2>2020-12-18</h2>
<h3>MyBatis like 쿼리문 검색시 처리방법</h3><br/>
* 링크 참고(https://fruitdev.tistory.com/60)
<hr/>
<h2>2020-12-16</h2>
<h3>ORA-06502 에러</h3><br/>
* 프로시저 실행시 선언된 변수의 크기보다 더 큰 값을 담으려 할 때 발생하는 에러<br/>
* 링크 참고(https://shxrecord.tistory.com/26) (https://jungmina.com/714)
<hr/>
<h2>2020-12-15 TIL</h2>
<h3>!= 연산자</h3>
오라클에서 != 연산자는 <>로도 표현 가능
<br/>
* 링크 참고 (https://okky.kr/article/150761)
