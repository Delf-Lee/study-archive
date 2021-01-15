# Bean 등록하기
## xml 설정 파일
``` xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
 
    <bean id="bookService"
          class="com.atoz_develop.springapplicationcontext.BookService"/>
 
    <bean id="bookRepository"
          class="com.atoz_develop.springapplicationcontext.BookRepository"/>
    
</beans>
```
`<bean>`에 빈을 등록해주면 된다. id, class 속성은 필수이고, 경우에 따라 scope나 autowired 속성을 줄 설정해줄 수 있다.

id에 빈의 id를, class에 빈으로 등록할 클래스의 QName(패키지명을 포함한 전체 이름)을 입력한다.

이렇게 등록한 빈은 주입도 설정파일에서 직접 해줘야한다.

``` xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
 
    <bean id="bookService"
          class="com.atoz_develop.springapplicationcontext.BookService">
        <property name="bookRepository" ref="bookRepository"/>
    </bean>
 
    <bean id="bookRepository"
          class="com.atoz_develop.springapplicationcontext.BookRepository"/>
 
</beans>
```
`<property>`가 주입하기 위한 태그인데, bookService 빈을 보면 bookRepository라는 빈을 주입받고 있다.

name은 주입받을 빈의 (생성자, 혹은 setter의) 파라미터 이름, ref는 주입할 빈의 id를 지정한다.

## xml 설정 파일 + Component Scan

이렇게 등록할 빈을 하나하나 다 적고있으면 코드도 길어지고 시간도 많이 걸린다. 

이걸 해결 할 수 있는게 component scan인데, **지정한 패키지**의 **특정한 클래스**들을 자동으로 읽어들여 빈으로 등록한다.

여기서 '지정한 패키지'는 설정 파일에서 `<context:component-scan>`을 통해 명시해준 패키지 경로를 뜻한다. 
```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">
 
    <context:component-scan base-package="com.atoz_develop.springapplicationcontext"/>
 
</beans>
```
그리고 '특정한 클래스'는 `@Component`와 그 스테레오 타입 어노테이션들(`@Controller`,`@Service`,`@Repository` 등)이 붙은 클래스를 의미한다.

의존성 주입은 `@Autowired`를 통해 가능하다.

## java 설정 파일(클래스)
xml 파일 이외에도 java 파일(클래스)로 설정값을 줄 수 있다.

``` java
@Configuration
public class ApplicationConfig {
 
    @Bean
    public BookRepository bookRepository() {
        return new BookRepository();
    }
 
    @Bean
    public BookService bookService() {
        BookService bookService = new BookService();
        bookService.setBookRepository(bookRepository());
        return bookService;
    }
}
```
설정 값을 줄 클래스에 `@Configuration`를 붙여주고, 빈으로 등록할 클래스 객체를 반환하는 메서드를 정의하면 된다. 이 때 메서드에 `@Bean`을 붙여줘야한다.

다음과 같이 외부에서 의존성을 주입할 수 있다.
``` java
@Bean
    public BookService bookService(BookRepository bookRepository) { // 주입할 객체
        BookService bookService = new BookService();
        bookService.setBookRepository(bookRepository);
        return bookService;
    }
```
이 방법의 장점은 타입 안정성을 유지할 수 있다는 점이다.

다만 xml 설정 파일에서도 나왔던 문제처럼 코드가 길어지고 시간이 걸린다는 단점은 여전히 존재한다.

## java 설정 파일 + Component Scan
java 설정 파일에서도 컴포넌트 스캔을 적용할 수 있다. 설정 클래스 위에 `@Configuration`를 달아주면 된다.

``` java
@Configuration
//@ComponentScan(basePackages = "com.atoz_develop.springapplicationcontext")
@ComponentScan(basePackageClasses = ApplicationConfig.class) // 더 type safe
public class ApplicationConfig {
}
```

이 역시 명시해준 패키지를 스캔하면서 `@Component`, 혹은 그 스테레오 타입 어노테이션이 달린 클래스를 찾아 빈으로 등록해준다.

## Spring boot
java 설정 파일 + Component Scan 방법을 내부적으로 적용하고 있는게 Spring boot의 방법이다.
``` java
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Inherited
@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan(excludeFilters = { @Filter(type = FilterType.CUSTOM, classes = TypeExcludeFilter.class),
		@Filter(type = FilterType.CUSTOM, classes = AutoConfigurationExcludeFilter.class) })
public @interface SpringBootApplication {
    // ...
}
```
`@SpringBootConfiguration`, `@ComponentScan`이 있는걸 확인할 수 있다.