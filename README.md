# springboot1
김영한-실전! 스프링 부트와 jpa활용 1편

https://start.spring.io를 이용하여 쉽게 스프링부트 프로젝트 생성 가능

@PersitenceContext 스프링부트는 스프링컨테이너에서 동작시키기에 이 어노테이션을 보고 EntityManager를 자동으로 주입시켜줌

@PersistenceContext
private EntityManager em;

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

* 단축키 shift + ctrl + F 특정 단어가 검색된 클래스 공간 찾기

em.find를 할때는 찾을 클래스를 먼저 대입하고 이후에 기본키를 대입 ex : em.find(Member.class, id);

em.createQuery를 할때는 jpql을 먼저 적어주고 이후에 찾을 클래스를 대입 ex : em.createQuery("select m from Member m ", Member.class);

@SpringBootApplication은 ComponantScan의 역할을 하기 떄문에 해당 어노테이션이 적혀있는 클래스의 하위 클래스중 @Component가 있는 클래스들을 자동으로 빈등록함

jpa의 모든 데이터변경이나 로직들은 @Transactional안에서 실행되야함(클래스와 메소드에도 전부  @Transactional 붙여야함!)

@Transactional에서 옵션인 (readOnly = true)를 사용하면 더 최적화된 방법으로 읽어올 수 있음(가급적 읽어오는 메소드에는 무조건 붙여줄것!,데이터 변경에는 쓰면 안됨!)

클래스에 (readOnly = true)를 붙여주고 특정 데이터 변경 메소드에는 단순히 @Transactional을 붙여주면 메소드에 있는 어노테이션이 우선적으로 작동하므로 기본값인 readOnly=false가 적용

@Transactional은 테스트를 할떄 롤백을 시키기 때문에 db에 저장이 안됨 그래서 특정 테스트문에 @Rollback(value = false)을 적용해야함!

@Repository
@RequiredArgsConstructor
public class ItemRepository {

    private final EntityManager em;
       
}
RequiredArgsConstructor가 final인 변수에 자동으로 값을 대입시켜줌 그로인해 @PersitenceContext로 주입시켜줄 필요가 없다.

엔티티를 개발할때 생성메소드, 비즈니스 로직을 구분하여 만드는것이 효율적으로 짜는것이니 실무에서도 이렇게 사용하자!
