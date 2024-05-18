# spring ehcache

## java, gradle, spring version
* java 11
* gradle 7.4
* spring boot 2.7.4
* spring.dependency-manangement 1.0.15.RELEASE

## dependencies
* org.springframework.boot:spring-boot-starter-web
* org.mybatis.spring.boot:mybatis-spring-boot-starter:2.3.2
* org.springframework.boot:spring-boot-starter-jdbc
* org.springframework.boot:spring-boot-starter-cache
* net.sf.ehcache:ehcache
* org.bgee.log4jdbc-log4j2:log4jdbc-log4j2-jdbc4.1:1.16
* mysql:mysql-connector-java

### Spring boot ehcache @Cacheable key, condition 사용
* Cache 기능을 처리하는데 페이징 처리를 하는 "NoticeReadMapper.findByPage"와 같은 같은 캐시 이름으로 1, 2 페이지 각각을 어떻게 캐싱 처리를 할 수 있을까?
* @Cacheable의 속성 값으로 key, condition으로 캐시 키의 이름을 더 세부적으로 나누고 조건을 추가할 수 있다.

구현부에 @Cacheable 애노테이션을 사용한다.
key 변수에 원하는 조건으로 캐시 키 이름을 지정이 가능하다. 
contidtion 변수에서는 원하는 조건절을 설정 가능하고 하단 구문에서는 pageNumber가 5이하일 때 5페이지까지만 캐시 기능을 가능하게 설정한 것이다.

```java
@Cacheable(value = "NoticeReadMapper.findByPage", key = "#request.requestURI + '-' + #pageNumber", condition = "#pageNumber <= 5")
```
