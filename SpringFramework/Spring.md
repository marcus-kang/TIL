<h1>[Spring Framework]</h1>
<h2>2020-12-07 TIL</h2>
<h3>mybatis - VO 컬럼 자동매핑</h3>
* sql-mapper-config.xml 파일 설정을 통해 DB의 컬럼명이 camel case 형식으로 변경
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN" "http://mybatis.org/dtd/mybatis-3-config.dtd">

<configuration>
	<settings>
  		<setting name="mapUnderscoreToCamelCase" value="true"/>
  		<setting name="callSettersOnNulls" value="true"/>
  		<setting name="jdbcTypeForNull" value="VARCHAR"/>
	</settings>
	
    <typeAliases></typeAliases>
<typeHandlers>
        <typeHandler handler="kr.co.wizi.kywa.comm.hndlr.MyBatisClobHndlr" javaType="String" jdbcType="CLOB"/>
    </typeHandlers>
</configuration>

* 참고 (https://mine-it-record.tistory.com/259)
