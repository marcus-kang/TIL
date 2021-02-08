<h1>[Java]</h1>
<h2>2021-02-08 TIL</h2>
<h3>문자열 공백 확인 및 처리</h3>
* 문자열은 '=='로 비교하지 않고 equals를 사용하여 비교해야 함. 빈 문자열 체크는 Empty와 Blank를 사용 가능하며 차이점은 아래 링크로 확인<br/>
* Empty, Blank 비교 (https://hahaha2016.tistory.com/4)<br/>
* equals와 '=='의 차이점 (https://kmj1107.tistory.com/entry/JAVA-%EB%AC%B8%EC%9E%90%EC%97%B4string-%EB%B9%84%EA%B5%90-equals%EC%99%80-%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90-equals%EC%9D%98-%EB%B0%98%EB%8C%80)<br/>
<hr/>
<h2>2021-02-04 TIL</h2>
<h3>Java 클래스 버전 확인</h3>
* 참고 링크
(https://blog.naver.com/0131v/110131984015)
<hr/>
<h2>2021-01-22 TIL</h2>
<h3>Map을 순서대로 불러올 때</h3>
* 참고 링크
(https://djusti.tistory.com/11)
<hr/>
<h2>2021-01-12 TIL</h2>
<h3>직렬화(implements Serializable)를 하는 이유</h3>
* 참고 링크
(https://okky.kr/article/224715)
<hr/>
<h2>2021-01-08 TIL</h2>
<h3>정규 표현식 패턴 일치여부 체크</h3>
* Pattern.matches(pattern, value)를 이용해서 value가 pattern과 일치하는 지 여부 확인<br/>
* 참고 링크
(https://coding-factory.tistory.com/529)
<hr/>
<h2>2020-12-07 TIL</h2>
<h3>Java 스케줄링(배치) 설정방법 - Quartz + CronTrigger</h3>
* 전자정부 프레임워크를 통해 사용됨
- src/framework/spring/context-job.xml
    <bean name="lessonJob" class="org.springframework.scheduling.quartz.JobDetailFactoryBean"
          p:jobClass="kr.co.wizi.kywa.comm.job.LessonJob"
          p:durability="true">
        <property name="jobDataAsMap">
            <map>
                <entry key="examScoreService" value-ref="examScoreService"/> 
            </map>
        </property>
    </bean>
 
    <bean id="cronTrigger" class="org.springframework.scheduling.quartz.CronTriggerFactoryBean"
          p:jobDetail-ref="lessonJob"
          p:startDelay="1000"
          p:cronExpression="0 0 1,12 * * ?"/>
 
    <bean id="schedulerFactoryBean" class="org.springframework.scheduling.quartz.SchedulerFactoryBean">
        <property name="triggers">
            <list>
                <ref bean="cronTrigger"/>
            </list>
        </property>
    </bean>
    
- 실행대상 : LessonJob bean에서 jobClass가 실행
- 실행주기 : cronTrigger bean에서 cronExpression의 설정주기대로 반복. 주기 정보는 아래 별도 정보 참조
- 스케줄러 생성 지원 : schedulerFactoryBean

* CronTrigger를 통해 스케줄을 설정할 수 있으며, '초 분 시 일 월 요일 년'순으로 설정

* 참고<br/>
(https://blog.cjred.net/entry/%EC%9E%90%EB%B0%94%EA%B8%B0%EB%B0%98-%EC%8A%A4%EC%BC%80%EC%A4%84%EB%A7%81-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D5-Quartz-CronTrigger)<br/>
(https://junspapa-itdev.tistory.com/18)<br/>
