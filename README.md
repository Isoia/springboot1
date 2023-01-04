# springboot1
김영한-실전! 스프링 부트와 jpa활용 1편

https://start.spring.io를 이용하여 쉽게 스프링부트 프로젝트 생성 가능

@PersitenceContext 스프링부트는 스프링컨테이너에서 동작시키기에 이 어노테이션을 보고 EntityManager를 자동으로 주입시켜줌

단축키 : shift + ctrl + t = 해당 클래스의 코드에 대한 테스트 클래스 작성

@Transactional은 EntityTransaction tx = em.getTransaction();와 같은것으로 실행할려할때 항상 붙여줘야함 (테스트케이스의 경우는 어노테이션으로)

@Transactional은 테스트케이스에서 동작 시 테스트 이후 db를 원상태로 롤백시킴

데이터가 실제로 들어왓는지 확인하고 싶으면 @Rollback(false)을 추가해준다

Assertions.assertThat(findMember).isEqualTo(member); Assertions는 테스트케이스에서 주로 테스트를 할 때 사용하는 문

