# spring
스프링 공부 기록
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

# 비즈니스 요구사항과 설계 
## 회원
- 회원을 가입하고 조회할 수 있다.
- 회원은 일반과 VIP 두 가지 등급이 있다.
- 회원 데이터는 자체 db를 구축할 수 있고, 외부 시스템과 연동할 수 있다.
## 주문과 할인 정책
- 회원은 상품을 주문할 수 있다.
- 회원 등급에 따라 할인 정책을 적용할 수 있다.
- 할인 정책은 모든 VIP는 1000원을 할인해주는 고정 금액 할인을 적용해달라.
- 할인 정책은 변경 가능성이 높다. 
## 주문 도메인 협력, 역할 , 책임
1. 주문 생성: 클라이언트는 주문 서비스에 주문 생성을 요청한다.
2. 회원 조회: 할인을 위해서는 회원 등급이 필요하다. 그래서 주문 서비스는 회원 저장소에서 회원을 조회한다.
3. 할인 적용: 주문 서비스는 회원 등급에 따른 할인 여부를 할인 정책에 위임한다.
4. 주문 결과 반환: 주문 서비스는 할인 결과를 포함한 주문 결과를 반환한다. 

# 관심사의 분리
## 관심사를 분리하자
- 배우는 본인의 역할인 배역을 수행하는 것에만 집중해야 한다.
- 디카프리오는 어떤 여자 주인공이 선택되더라도 똑같이 공연을 할 수 있어야 한다.
- 공연을 구성하고, 담당 배우를 섭외하고, 역할에 맞는 배우를 지정하는 책임을 담당하는 별도의 "공연기획자"가 나올 시점이다.
- 공연 기획자를 만들고, 배우와 공연 기획자의 책임을 확실히 분리하자.

## AppConfig
- 애플리케이션의 전체 동작 방식을 구성하기 위해 <b>구현 객체</b>를 생성하고 <b>연결</b>하는 책임을 가지는 별도의 설정 클래스를 만들자!

# 좋은 객체 지향 설계의 5가지 원칙 적용
## SRP 단일 책임 원칙 : 한 클래슨느 하나의 책임만 져야한다
- 클라이언트 객체는 직접 구현 객체를 생성하고, 연결하고, 실행하는 다양한 책임을 가지고 있음
- AppConfig가 구현 객체를 생성하고 연결
- 클라이언트는 실행만
## DIP 의존관계 역전 원칙 : 구체화에 의존하면 안된다
- 기존 클라이언트 코드(OrderServiceImpl)는 DiscountPolicy 추상화 인터페이스에 의존하는 것 같았지만, FixDiscountPolicy 구체화 구현 클래스에도 의존했다.
- AppConfig가 FixDiscountPolicy 객체 인스턴스를 클라이언트 코드 대신 생성해서 클라이언트 코드에 의존 관계를 주입했다.
## OCP : 확장에는 열려있으나, 변경에는 닫혀 있어야 한다.
- AppConfig가 FixDiscountPolicy -> RateDiscountPolicy로 변경해서 클라이언트 코드에 주입하므로 클라이언트 코드는 변경하지 않아도 된다.
- 소프트웨어 요소를 새롭게 확장해도 사용영역의 변경은 닫혀있다.
