# Cheat Sheet - Common Annotations in Spring Boot Applications 

[![PRs Welcome][shield-prs]](https://github.com/gindex/spring-boot-annotation-list/pulls)
[![license][shield-license]](https://github.com/gindex/spring-boot-annotation-list/blob/master/LICENSE)


This document contains non-comprehensive list of frequently used annotations in Spring Boot applications. 
It should rather be used as a quick lookup list, for detailed and comprehensive information please read official javadocs and documentation.  


## Contents
- [Core Spring](#core-spring)
- [Spring Boot](#spring-boot)
- [Spring Boot Tests](#spring-boot-tests)
- [Spring Test](#spring-test)
- [Transactions](#transactions)
- [Spring JPA & Hibernate](#spring-jpa-and-hibernate)
- [Spring Security](#spring-security)
- [Spring AOP](#spring-aop)


## Core Spring

- [@Bean][bean] - Annotated method produces a bean managed by the Spring IoC container
- Stereotype annotations
    - [@Component][component] - Marks annotated class as a bean found by the component-scanning and loaded into the application context
    - [@Controller][controller]  - Marks annotated class as a bean for Spring MVC containing request handler
    - [@RestController][rest-controller] - Marks annotated class as a `@Controller` bean and adds `@ResponseBody` to serialize returned results as messages  
    - [@Configuration][config] - Marks annotated class as a Java configuration defining beans   
    - [@Service][service] - Marks annotated class as a bean (as convention usually containing business logic)  
    - [@Repository][repo] - Marks annotated class as a bean (as convention usually providing data access) and adds auto-translation from `SQLException` to `DataAccessExceptions` 

Bean state
- [@PostConstruct][postconstruct] - Annotated method is executed after dependency injection is done to perform initialization 
- [@PreDestroy][predestroy] - Annotated method is executed before the bean is destroyed, e.g. on the shutdown 

Configuration
- [@Import][import] - Imports one or more Java configuration classes `@Configuration`
- [@PropertySource][propertysource] - Indicates the location of `applicaiton.properties` file to add key-value pairs to Spring `Environment`
- [@Value][value] - Annotated fields and parameters values will be injected 
- [@ComponentScan][componentscan] - Configures component scanning `@Compenent`, `@Service`, etc. 

Bean properties
- [@Lazy][lazy] - Annotated bean will be lazily initialized on the first usage
- [@Profile][profile] - Indicates that beans will be only initialized if the defined profiles are active   
- [@Scope][scope] - Defines bean creation scope, e.g. prototype, singleton, etc.
- [@DependsOn][dependson] - Explicitly defines a dependency to other beans in terms of creation order     
- [@Order][order] - Defines sorting order if injecting a list of beans, but it does not resolve the priority if only a single bean is expected
- [@Primary][primary] - Annotated bean will be picked if multiple beans can be autowired 
- [@Conditional][conditional] - Annotated bean is created only if conditions are satisfied
    - Additionally available in Spring Boot: 
        - [@ConditionalOnBean][conditionalonbean]  
        - [@ConditionalOnMissingBean][conditionalonmissingbean]
        - [@ConditionalOnClass][conditionalonclass]
        - [@ConditionalOnMissingClass][conditionalonmissingclass]
        - [@ConditionalOnProperty][conditionalonproperty]
        - [@ConditionalOnMissingProperty][conditionalonmissingproperty]

Bean injection
- [@Autowired][autowired] - Beans are injected into annotated setters, fields, or constructor params. 
- [@Qualifier][qualifier] - Specifies the name of a bean as an additional condition to identify a unique candidate for autowiring

## Spring Boot

- [@SpringBootConfiguration][springbootconfiguration] - Indicates Spring Boot application `@Configuration`
- [@EnableAutoConfiguration][enableautoconfiguration] - Enables application context auto-configuration to provide possibly needed beans based on the classpath
- [@ConfigurationProperties][configurationproperties] - Provides external binding of key value properties 
- [@ConfigurationPropertiesScan][configurationpropertiesscan] - Enables auto-detection of `@ConfigurationProperties` classes
- [@SpringBootApplication][springbootapplication] - Combination of `@SpringBootConfiguration`, `@EnableAutoConfiguration`, `@ConfigurationPropertiesScan` and `@ComponentScan`
- [@EntityScan][entityscan] - Configures base packages to scan for entity classes 
- [@EnableJpaRepositories][enablejparepositories] - Enables auto-configuration of jpa repositories
 
 ## Spring Boot Tests
 
- [@SpringBootTest][springboottest] - Annotated test class will load the entire application context for integration tests
- [@WebMvcTest][webmvctest] - Annotated test class will load only the web layer (service and data layer are ignored)
- [@DataJpaTest][datajpatest] - Annotated class will load only the JPA components 
- [@MockBean][mockbean] - Marks annotated field as a mock and loads it as a bean into the application context  
- [@SpyBean][spybean] - Allows partial mocking of beans 
- [@Mock][mock]  - Defines annotated field as a mock
 
 ## Spring Test
 
- [@ContextConfiguration][contextconfiguration] - Defines `@Configuration` to load application context for integration test
- [@ExtendWith][extendwith] - Defines extensions to execute the tests with, e.g. MockitoExtension
- [@SpringJUnitConfig][springjunitconfig] - Combines `@ContextConfiguration` and `@ExtendWith(SpringExtension.class)`
- [@TestPropertySource][testpropertysource] - Defines the location of property files used in integration tests
- [@DirtiesContext][dirtiescontext] -  Indicates that annotated tests dirty the application context and will be cleaned after each test  
- [@ActiveProfiles][activeprofiles] - Defines which active bean definition should be loaded when initializing the test application context 
- [@Sql][sql] - Allows defining SQL scripts and statements to be executed before and after tests   

## Transactions

- [@EnableTransactionManagement][enabletransactionmanagement] - Enables annotation-driven transaction declaration `@Transactional`
- [@Transactional][transactional] - Annotated methods will be executed in a transactional manner 

## Spring JPA and Hibernate

- [@Id][id] - Marks annotated field as a primary key of an entity
- [@GeneratedValue][generatedvalue] - Provides generation strategy of primary keys
- [@Entity][entity] - Marks annotated class as an entity
- [@Column][column] - Provides additional configuration for a field, e.g. column name
- [@Table][table] - Provides additional configuration for an entity, e.g. table name
- [@PersistenceContext][persistencecontext] - `EntityManger` is injected into annotated setters and fields  
- [@Embedded][embedded] - Annotated field is instantiated as a value of an `Embeddable` class 
- [@Embeddable][embeddable] - Instances of an annotated class are stored as part of an entity  
- [@EmbeddedId][embeddedid] - Marks annotated property as a composite key mapped by an embeddable class
- [@AttributeOverride][attributeoverride] - Overrides the default mapping of a field  
- [@Transient][transient] - Annotated field is not persistent
- [@CreationTimestamp][creationtimestamp] - Annotated field contains the timestamp when an entity was stored for the first time 
- [@UpdateTimestamp][updatetimestamp] - Annotated field contains the timestamp when an entity was updated last time 
- [@ManyToOne][manytoone] - Indicates N:1 relationship, the entity containing annotated field has a single relation to an entity of other class, but the other class has multiple relations     
- [@JoinColumn][joincolumn] - Indicates a column for joining entities in `@ManyToOne` or `@OneToOne` relationships at the owning side or unidirectional `@OneToMany` 
- [@OneToOne][onetoone] - Indicates 1:1 relationship 
- [@MapsId][mapsid] - References joining columns of owning side of `@ManyToOne` or `@OneToOne` relationships to be the primary key of referencing and referenced entities  
- [@ManyToMany][manytomany] - Indicates N:M relationship
- [@JoinTable][jointable] - Specifies an association using a join table
- [@BatchSize][batchsize] - Defines size to lazy load a collection of annotated entities
- [@FetchMode][fetchmode] - Defines fetching strategy for an association, e.g. loading all entities in a single subquery

## Spring Security

- [@EnableWebSecurity][enablewebsecurity] - Enables web security
- [@EnableGlobalMethodSecurity][enableglobalmethodsecurity] - Enables method security 
- [@PreAuthorize][preauthorize] - Defines access-control expression using SpEL, which is evaluated before invoking a protected method 
- [@PostAuthorize][postauthorize] -  Defines access-control expression using SpEL, which is evaluated after invoking a protected method
- [@RolesAllowed][rolesallowed] - Specifies a list of security roles allowed to invoke protected method 
- [@Secured][secured] -  Java 5 annotation for defining method level security

## Spring AOP

- [@EnableAspectJAutoProxy][enableaspectjautoproxy] - Enables support for handling components marked with `@Aspect`
- [@Aspect][aspect] - Declares an annotated component as an aspect containing pointcuts and advices
- [@Before][before] - Declares a pointcut executed before the call is propagated to the join point 
- [@AfterReturning][afterreturning] - Declares a pointcut executed if the join point successfully returns a result
- [@AfterThrowing][afterthrowing] - Declares a pointcut executed if the join point throws an exception 
- [@After][after] - Declares a pointcut executed if the join point successfully returns a result or throws an exception 
- [@Around][around] - Declares a pointcut executed before the call giving control over the execution of the join point to the advice
- [@Pointcut][pointcut] - Externalized definition a pointcut expression 

[shield-prs]: https://img.shields.io/badge/PRs-welcome-brightgreen.svg
[shield-license]: https://img.shields.io/badge/license-CC0-green

[bean]: https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/context/annotation/Bean.html
[component]: https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/stereotype/Component.html
[controller]: https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/stereotype/Controller.html
[rest-controller]: https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/web/bind/annotation/RestController.html
[config]: https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/context/annotation/Configuration.html
[service]: https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/stereotype/Service.html
[repo]: https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/stereotype/Repository.html

[postconstruct]: https://docs.oracle.com/javaee/7/api/javax/annotation/PostConstruct.html
[predestroy]: https://docs.oracle.com/javaee/7/api/javax/annotation/PreDestroy.html

[import]:https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/context/annotation/Import.html
[propertysource]: https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/context/annotation/PropertySource.html
[value]: https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/beans/factory/annotation/Value.html
[componentscan]: https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/context/annotation/ComponentScan.html

[lazy]: https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/context/annotation/Lazy.html
[profile]: https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/context/annotation/Profile.html 
[scope]: https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/context/annotation/Scope.html
[dependson]: https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/context/annotation/DependsOn.html
[order]: https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/core/annotation/Order.html
[primary]: https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/context/annotation/Primary.html
[conditional]: https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/context/annotation/Conditional.html
[conditionalonbean]: https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/autoconfigure/condition/ConditionalOnBean.html
[conditionalonmissingbean]: https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/autoconfigure/condition/ConditionalOnMissingBean.html
[conditionalonclass]: https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/autoconfigure/condition/ConditionalOnClass.html
[conditionalonmissingclass]: https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/autoconfigure/condition/ConditionalOnMissingClass.html
[conditionalonproperty]: https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/autoconfigure/condition/ConditionalOnProperty.html
[conditionalonmissingproperty]: https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/autoconfigure/condition/ConditionalOnProperty.html

[autowired]: https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/beans/factory/annotation/Autowired.html
[qualifier]: https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/beans/factory/annotation/Qualifier.html

[springbootconfiguration]: https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/SpringBootConfiguration.html
[enableautoconfiguration]: https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/autoconfigure/EnableAutoConfiguration.html
[configurationproperties]: https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/context/properties/ConfigurationProperties.html
[configurationpropertiesscan]: https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/context/properties/ConfigurationPropertiesScan.html
[springbootapplication]: https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/autoconfigure/SpringBootApplication.html
[entityscan]: https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/autoconfigure/domain/EntityScan.html
[enablejparepositories]: https://docs.spring.io/spring-data/data-jpa/docs/current/api/org/springframework/data/jpa/repository/config/EnableJpaRepositories.html

[springboottest]: https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/test/context/SpringBootTest.html
[webmvctest]: https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/test/autoconfigure/web/servlet/WebMvcTest.html
[datajpatest]: https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/test/autoconfigure/orm/jpa/DataJpaTest.html
[mockbean]: https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/test/mock/mockito/MockBean.html
[spybean]: https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/test/mock/mockito/SpyBean.html
[mock]: https://www.javadoc.io/doc/org.mockito/mockito-core/latest/org/mockito/Mock.html

[contextconfiguration]: https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/test/context/ContextConfiguration.html
[extendwith]: https://junit.org/junit5/docs/current/api/org.junit.jupiter.api/org/junit/jupiter/api/extension/ExtendWith.html
[springjunitconfig]: https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/test/context/junit/jupiter/SpringJUnitConfig.html
[testpropertysource]: https://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/test/context/TestPropertySource.html
[dirtiescontext]: https://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/test/annotation/DirtiesContext.html
[activeprofiles]: https://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/test/context/ActiveProfiles.html
[sql]: https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/test/context/jdbc/Sql.html

[enabletransactionmanagement]: https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/transaction/annotation/EnableTransactionManagement.html
[transactional]: https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/transaction/annotation/Transactional.html

[id]: https://docs.oracle.com/javaee/7/api/javax/persistence/Id.html
[generatedvalue]: https://docs.oracle.com/javaee/7/api/javax/persistence/GeneratedValue.html
[entity]: https://docs.oracle.com/javaee/7/api/javax/persistence/Entity.html
[column]: https://docs.oracle.com/javaee/7/api/javax/persistence/Column.html
[table]: https://docs.oracle.com/javaee/7/api/javax/persistence/Table.html
[persistencecontext]: https://docs.oracle.com/javaee/7/api/javax/persistence/PersistenceContext.html
[embedded]: https://docs.oracle.com/javaee/7/api/javax/persistence/Embedded.html
[embeddable]: https://docs.oracle.com/javaee/7/api/javax/persistence/Embeddable.html
[embeddedid]: https://docs.oracle.com/javaee/7/api/javax/persistence/EmbeddedId.html
[attributeoverride]: https://docs.oracle.com/javaee/7/api/javax/persistence/AttributeOverride.html
[transient]: https://docs.oracle.com/javaee/7/api/javax/persistence/Transient.html
[creationtimestamp]: https://docs.jboss.org/hibernate/orm/5.4/javadocs/org/hibernate/annotations/CreationTimestamp.html
[updatetimestamp]: https://docs.jboss.org/hibernate/orm/5.4/javadocs/org/hibernate/annotations/UpdateTimestamp.html
[manytoone]: https://docs.oracle.com/javaee/7/api/javax/persistence/ManyToOne.html
[joincolumn]: https://docs.oracle.com/javaee/7/api/javax/persistence/JoinColumn.html
[onetoone]: https://docs.oracle.com/javaee/7/api/javax/persistence/OneToOne.html
[mapsid]: https://docs.oracle.com/javaee/7/api/javax/persistence/MapsId.html
[manytomany]: https://docs.oracle.com/javaee/7/api/javax/persistence/ManyToMany.html
[jointable]: https://docs.oracle.com/javaee/7/api/javax/persistence/JoinTable.html
[batchsize]: https://docs.jboss.org/hibernate/orm/5.4/javadocs/org/hibernate/annotations/BatchSize.html
[fetchmode]: https://docs.jboss.org/hibernate/orm/5.4/javadocs/org/hibernate/annotations/FetchMode.html

[enablewebsecurity]:https://docs.spring.io/spring-security/site/docs/current/api/org/springframework/security/config/annotation/web/configuration/EnableWebSecurity.html
[enableglobalmethodsecurity]: https://docs.spring.io/spring-security/site/docs/current/api/org/springframework/security/config/annotation/method/configuration/EnableGlobalMethodSecurity.html
[preauthorize]: https://docs.spring.io/spring-security/site/docs/current/api/org/springframework/security/access/prepost/PreAuthorize.html
[postauthorize]: https://docs.spring.io/spring-security/site/docs/current/api/org/springframework/security/access/prepost/PostAuthorize.html
[rolesallowed]: https://docs.oracle.com/javaee/7/api/javax/annotation/security/RolesAllowed.html
[secured]: https://docs.spring.io/spring-security/site/docs/current/api/org/springframework/security/access/annotation/Secured.html

[enableaspectjautoproxy]: https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/context/annotation/EnableAspectJAutoProxy.html
[aspect]: https://javadoc.io/static/org.aspectj/aspectjrt/1.9.5/org/aspectj/lang/annotation/Aspect.html
[before]: https://javadoc.io/static/org.aspectj/aspectjrt/1.9.5/org/aspectj/lang/annotation/Before.html
[afterreturning]: https://javadoc.io/static/org.aspectj/aspectjrt/1.9.5/org/aspectj/lang/annotation/AfterReturning.html
[afterthrowing]: https://javadoc.io/static/org.aspectj/aspectjrt/1.9.5/org/aspectj/lang/annotation/AfterThrowing.html
[after]: https://javadoc.io/static/org.aspectj/aspectjrt/1.9.5/org/aspectj/lang/annotation/After.html
[around]: https://javadoc.io/static/org.aspectj/aspectjrt/1.9.5/org/aspectj/lang/annotation/Around.html
[pointcut]: https://javadoc.io/static/org.aspectj/aspectjrt/1.9.5/org/aspectj/lang/annotation/Pointcut.html

