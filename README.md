# 1. 프로젝트 개요

- 프로젝트명: MVC 회원 관리 웹 애플리케이션
- 목적: 서블릿, JSP, MVC 구조를 이용한 회원관리 웹 어플리케이션 구현하여 기초 다지기
- 개발 범위: **개발 범위**: 순수 서블릿, JSP, Java를 사용한 회원 관리 기능 (Spring Framework 미사용)
- 사용 도구: IntelliJ, Gradle, Tomcat
- 개인 프로젝트: 김태경
- 구현 일정: 2025.08.01 ~ 2025.08.04

# 2. 기획 배경 및 벤치마킹

- 문제 인식: Spring과 같은 웹 프레임워크는 많은 부분을 자동화해주어 편리하지만, 내부 동작 원리를 이해하기 어렵다. 프레임워크 사용에 앞서, 서블릿과 JSP만으로 웹 애플리케이션을 만들어보며 웹의 기본 동작 방식과 MVC 패턴의 역할을 깊이 있게 학습할 필요가 있다.
- 벤치마킹 서비스: 없음
- 구현 목표: 스프링 기능을 사용하지 않고 서블릿, jsp를 통해 MVC 구조의 회원가입 웹 어플리케이션 구현하기

# 3. 요구사항

- 회원 정보

이름: username

나이: age

- 기능 요구사항

회원 저장, 회원 목록 조회

# 4. 기능 명세서

| **기능명** | **설명** | **적용 기술** | **구현 여부** |
| --- | --- | --- | --- |
| **회원 가입 양식** | 회원의 이름과 나이를 입력할 수 있는 HTML 폼 페이지를 제공한다. | Servlet, JSP, HTML | ✅ |
| **회원 가입 양식** | 가입 양식에서 받은 데이터를 MemberRepository에 저장하고, 결과를 JSP 페이지에 출력한다. | Servlet, Java | ✅ |
| **회원 가입 양식** | MemberRepository에 저장된 모든 회원 정보를 조회하여 JSP 페이지에 목록 형태로 출력한다. | Servlet, JSP, Java | ✅ |

# 5. 페이지 구성 및 계층 구조

```xml
servlet
├── .gradle
├── .idea
├── build
├── gradle
├── out
├── src
│   └── main
│       ├── generated
│       └── java
│           └── hello
│               └── servlet
│                   ├── basic
│                   ├── domain
│                   │   └── member
│                   │       ├── Member.java
│                   │       └── MemberRepository.java
│                   └── web
│                       ├── servlet
│                       │   ├── MemberFormServlet.java
│                       │   ├── MemberListServlet.java
│                       │   └── MemberSaveServlet.java
│                       └── servletmvc
│                           ├── MvcMemberFormServlet.java
│                           ├── MvcMemberListServlet.java
│                           ├── MvcMemberLoginFormServlet.java
│                           ├── MvcMemberLoginServlet.java
│                           ├── MvcMemberSaveServlet.java
│                           ├── ServletApplication.java
│                           └── ServletInitializer.java
├── resources
└── webapp
├── basic
├── jsp
│   └── members
│       ├── login.jsp
│       ├── new-form.jsp
│       ├── save.jsp
│       └── members.jsp
└── WEB-INF
└── views
├── login-form.jsp
├── login-result.jsp
├── members.jsp
├── new-form.jsp
└── save-result.jsp
├── basic.html
└── index.html
test
└── java
└── hello
└── servlet
└── domain
└── member
├── MemberRepositoryTest.java
└── ServletApplicationTests.jav
```

# 7. 기술 구현 설명

| **항목** | **설명** |
| --- | --- |
| Java | 회원 정보를 담는 Member 객체와, 회원을 저장하고 조회하는 MemberRepository 비즈니스 로직을 구현한다. |
| Servlet | 클라이언트의 HTTP 요청을 받아 비즈니스 로직을 호출하고, 그 결과를 JSP(View)에 전달하는 **컨트롤러(Controller)** 역할을 수행한다. |
| JSP | 서블릿으로부터 전달받은 데이터를 사용하여 동적인 HTML을 생성하는 **뷰(View)** 역할을 담당한다. EL과 JSTL을 활용하여 간결한 뷰 코드를 작성한다. |
| HTML | 회원 가입 폼과 회원 목록 테이블의 기본적인 구조를 작성한다. |

# 8. 개발 일정 및 기록

| **날짜** | **작업 내용** | **상태** |
| --- | --- | --- |
| 8/1 | 프로젝트 환경 설정(Gradle, Tomcat), 도메인 모델(Member, MemberRepository) 구현 및 테스트 코드 작성 | 완료 |
| 8/2 | 회원 등록 기능 구현 (MVC 패턴 적용: MvcMemberFormServlet, MvcMemberSaveServlet, new-form.jsp, save-result.jsp) | 완료 |
| 8/3 | 회원 목록 조회 기능 구현 (MVC 패턴 적용: MvcMemberListServlet, members.jsp) | 완료 |
| 8/4 | 전체 코드 리팩토링 및 주석 작성, 개발 계획서 최종 정리 | 완료 |

# 9. 개선 및 확장 계획

- 데이터베이스 연동: 현재 메모리 기반의 MemberRepository를 JDBC를 사용하여 실제 데이터베이스(H2, MySQL 등)에 연동하도록 개선한다.
- Front Controller 패턴 도입: 모든 요청을 단일 서블릿(Front Controller)이 받아서 처리하도록 구조를 개선하여 중복 코드를 줄이고 유지보수성을 높인다.
- 회원 수정 및 삭제 기능: 기본적인 CRUD 기능을 완성하기 위해 회원 정보 수정 및 삭제 기능을 추가한다.
- View 분리 개선: RequestDispatcher의 forward를 사용하여 웹 리소스를 WEB-INF 경로 아래에 두어 외부에서 JS

# 10. 결론 및 회고

- 순수 서블릿과 JSP만으로 MVC 패턴을 직접 구현해보면서 웹 애플리케이션의 요청-응답 흐름과 각 구성요소(Model-View-Controller)의 역할을 명확하게 이해할 수 있었다.
- Spring MVC와 같은 프레임워크가 내부적으로 얼마나 많은 편의 기능을 제공하는지 체감하며 프레임워크의 소중함을 깨닫는 계기가 되었다.
- 이번 프로젝트를 통해 다진 웹 기본기 및 MVC 구조에 대한 이해는 향후 Spring 프레임워크를 더 깊이 있게 학습하고 활용하는 데 훌륭한 밑거름이 될 것이다.• 이후 동영상 삽입과 라이트 테마 적용 등 JavaScript를 활용한 동적 기능 개발을 목표로 함
