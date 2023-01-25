# springboot1
김영한-실전! 스프링 부트와 jpa활용 1편

https://start.spring.io를 이용하여 쉽게 스프링부트 프로젝트 생성 가능

@PersitenceContext 스프링부트는 스프링컨테이너에서 동작시키기에 이 어노테이션을 보고 EntityManager를 자동으로 주입시켜줌

단축키 : shift + ctrl + t = 해당 클래스의 코드에 대한 테스트 클래스 작성

@Transactional은 EntityTransaction tx = em.getTransaction();와 같은것으로 실행할려할때 항상 붙여줘야함 (테스트케이스의 경우는 어노테이션으로)

@Transactional은 테스트케이스에서 동작 시 테스트 이후 db를 원상태로 롤백시킴

데이터가 실제로 들어왓는지 확인하고 싶으면 @Rollback(false)을 추가해준다

Assertions.assertThat(findMember).isEqualTo(member); Assertions는 테스트케이스에서 주로 테스트를 할 때 사용하는 문

예제에서는 lombok의 getter,setter를 다 열어두고 하지만 실무에서는 getter는 열어두되 setter은 필요한 경우에만 열어두도록 하자!

@Embeddable : 값타입 필드를 재사용하기위해 사용, 재사용할 클래스에 @Embeddable을 붙여주고 사용할 필드에 @Embedded를 붙인다

@ManyToOne은 항상 조인할 JoinColumn(일쪽 기본키 이름) 같이 사용!, @OneToMany는 속성으로 mappedby사용(@OneToMany(mappedby=""))

@Inheritance(strategy = InheritanceType.SINGLE_TABLE), 상속테이블일 경우 해당 부모 테이블에 @Inheritance 설정값을 해줘야함

@DiscriminatorColumn(name = "dtype"), 상속테이블에서 상속받고있는 자식 테이블을 구분하기위해 dtype컬럼을 만들고 자식 테이블에 @DiscriminatorValue("B") 을 붙여 dtype의 컬럼값으로 구분함

@Enumerated(EnumType.STRING), jpa에서 enum을 사용할때 enum필드에 @Enumerated 어노테이션을 적어준다, 그리고 Enumerated의 기본속성은 ordinal인데 enum의 값을 1,2,3 이런 숫자로 비교하기에 직접 속성을 EnumType.String으로 지정해줘야 1,2,3이 아닌 enum필드 이름 그대로 컬럼으로 가져가서 비교할 수 있다.

모든 연관관계는 지연로딩으로 설정! XXXToOne 같은 경우는 기본값이 즉시로딩이기 떄문에 옵션값(@ManyToOne(fetch= FetchType.LAZY))을 줘야함(XXXToMany는 기본값이 지연로딩)

* 단축기 shift + ctrl + F 특정 단어가 검색된 클래스 공간 찾기

