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