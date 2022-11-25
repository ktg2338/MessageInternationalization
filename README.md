# MessageInternationalization
메세지 국제화

스프링 메시지 소스 설정<br/>
스프링은 기본적인 메시지 관리 기능을 제공한다.<br/>
메시지 관리 기능을 사용하려면 스프링이 제공하는 MessageSource 를 스프링 빈으로 등록하면 되는데,
MessageSource 는 인터페이스이다. 따라서 구현체인 ResourceBundleMessageSource 를 스프링 빈으로
등록하면 된다.<br/>
![image](https://user-images.githubusercontent.com/69129562/203990963-d5a72f8e-1839-4020-9c22-e3b77597600a.png)
<br/>
스프링 부트<br/>
스프링 부트를 사용하면 스프링 부트가 MessageSource 를 자동으로 스프링 빈으로 등록한다.<br/>
스프링 부트 메시지 소스 설정<br/>
스프링 부트를 사용하면 다음과 같이 메시지 소스를 설정할 수 있다.<br/>
application.properties<br/>
spring.messages.basename=messages,config.i18n.messages<br/>
스프링 부트 메시지 소스 기본 값<br/>
spring.messages.basename=messages<br/>
MessageSource 를 스프링 빈으로 등록하지 않고, 스프링 부트와 관련된 별도의 설정을 하지 않으면
messages 라는 이름으로 기본 등록된다.<br/> 따라서 messages_en.properties ,
messages_ko.properties , messages.properties 파일만 등록하면 자동으로 인식된다<br/>
<br/>
Locale 정보를 기반으로 국제화 파일을 선택한다.<br/>
Locale이 en_US 의 경우 messages_en_US messages_en messages 순서로 찾는다.<br/>
<br/>
타임리프 메시지 적용<br/>
타임리프의 메시지 표현식 #{...} 를 사용하면 스프링의 메시지를 편리하게 조회할 수 있다.<br/>
예를 들어서 방금 등록한 상품이라는 이름을 조회하려면 #{label.item} 이라고 하면 된다<br/>
<br/>
스프링의 국제화 메시지 선택<br/>
앞서 MessageSource 테스트에서 보았듯이 메시지 기능은 Locale 정보를 알아야 언어를 선택할 수 있다.<br/>
결국 스프링도 Locale 정보를 알아야 언어를 선택할 수 있는데, 스프링은 언어 선택시 기본으로 AcceptLanguage 헤더의 값을 사용한다.<br/>
LocaleResolver<br/>
스프링은 Locale 선택 방식을 변경할 수 있도록 LocaleResolver 라는 인터페이스를 제공하는데,
스프링 부트는 기본으로 Accept-Language 를 활용하는 AcceptHeaderLocaleResolver 를 사용한다.<br/>
<br/>
![image](https://user-images.githubusercontent.com/69129562/203994617-6cd09b8d-b8fd-4f5b-a7dc-2ac16d024a9d.png)
LocaleResolver 변경<br/>
만약 Locale 선택 방식을 변경하려면 LocaleResolver 의 구현체를 변경해서 쿠키나 세션 기반의
Locale 선택 기능을 사용할 수 있다. 예를 들어서 고객이 직접 Locale 을 선택하도록 하는 것이다. 
