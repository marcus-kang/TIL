<h1>[Java]</h1>
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

* 참고
(https://blog.cjred.net/entry/%EC%9E%90%EB%B0%94%EA%B8%B0%EB%B0%98-%EC%8A%A4%EC%BC%80%EC%A4%84%EB%A7%81-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D5-Quartz-CronTrigger)
(https://junspapa-itdev.tistory.com/18)
