#### 데이터베이스 기본

##### 1. 릴레이션과 관게의 차이점은 무엇인가요?
- 릴레이션은 데이터의 집합 즉 테이블 자체를 의미하지만, 관계는 테이블 간의 연결 즉 외래키 등으로 연결되는 개념을 의미합니다.

##### 2.기본 키와 후보 키의 차이점은 무엇인가요?
- 기본 키는 테이블에서 각 행을 유일하게 식별할 수 있는 속성이고 후보 키는 기본 키가 될 수 있는 가능한 모든 키의 집합입니다. 기본 키는 후보 키 중에서 하나를 선택한 것입니다.

##### 3. 기본 키와 대체 키의 차이는 무엇인가요?
- 대체 키는 후보 키 중에서 기본 키로 선택되지 않은 키입니다. 기본 키가 id라면, 다른 후보 키인 email은 대체 키가 될 수 있습니다.


---


#### ERD와 정규화

##### 4. ERD는 무엇이며, 왜 중요한가요?
- ERD는 데이터베이스의 구조를 시각적으로 표현한 다이어그램으로, 엔터티, 속성, 관계를 보여줍니다. 데이터 모델링 시 데이터 구조를 명확하게 설계하고, 팀원 간의 협업을 원활하게 하기 위해 사용됩니다.

##### 5. 그렇다면 ERD를 설계할 때 고려해야 할 요소는 무엇인가요?
- 주요 요소는 엔터티, 속성, 관계, 키입니다. 또한 정규화 과정을 거쳐 중복을 최소화해야 합니다.

##### 6. 정규화란 무엇이며, 왜 필요한가요?
- 정규화는 데이터의 중복을 최소화하고, 일관성을 유지하기 위해 테이블을 분해하는 과정입니다. 이를 통해 데이터 무결성을 보장하고, 저장 공간을 효율적으로 사용할 수 있습니다.

##### 7. 그렇다면 정규화의 장점과 단점은 무엇인가요?
- 장점은 중복 데이터 감소, 데이터 무결성 향상, 데이터 변경 시 일관성 유지입니다.
- 단점은 너무 많은 정규화를 하면 조인 연산이 증가하여 성능이 저하될 수 있습니다.


---


#### 트랜잭션과 무결성

##### 8. 트랜잭션의 의미와 ACID 원칙을 설명해주세요.
- 트랜잭션은 데이터베이스에서 하나의 논리적인 작업 단위입니다. 
  - A원자성: 트랜잭션 내의 작업이 모두 수행되거나, 전혀 수행되지 않음
  - C일관성: 트랜잭션이 성공하면 데이터가 일관된 상태로 유지됨
  - I고립성: 트랜잭션은 서로 독립적으로 실행되어야 함
  - D지속성: 트랜잭션이 완료되면 데이터가 영구적으로 저장됨

##### 9. 무결성이란 무엇이며, 이를 보장하는 방법에는 무엇이 있나요?
- 무결성이란 데이터의 정확성과 일관성을 유지하는 것을 의미합니다. 무결성을 보장하는 방법에는 다음이 있습니다.
개체 무결성, 참조 무결성, 도메인 무결성

##### 10. 트랜잭션이 실패한 경우 데이터베이스는 어떻게 원래 상태로 되돌아가나요?
- 트랜잭션이 실패하면 ROLLBACK을 수행하여 변경된 데이터를 원래 상태로 복구합니다.

##### 11. 트랜잭션의 격리 수준과 발생할 수 있는 문제는 무엇인가요?
- 트랜잭션의 격리 수준은 동시에 실행되는 트랜잭션 간의 데이터 접근을 조정하는 방식입니다. 격리 수준이 낮으면 성능은 향상되지만, 데이터 정합성은 떨어질 수 있습니다.

##### 12. 트랜잭션의 커밋과 롤백의 차이점은 무엇인가요?
- 커밋은 트랜잭션이 성공적으로 완료되었을 때 변경 사항을 확정하는 명령이고 롤백은 트랜잭션이 실패했을 때 변경된 데이터를 원래 상태로 되돌리는 명령입니다. 

##### 13. ROLLBACK이 실행될 수 없는 경우는 언제인가요?
- AUTO-COMMIT이 활성화된 상태이거나 DDL (CREATE, DROP, ALTER) 명령어를 실행한 경우 롤백이 불가능합니다.

##### 14. 참조 무결성을 유지하기 위한 ON DELETE CASCADE와 ON DELETE SET NULL의 차이점은 무엇인가요?
- 전자는 부모 테이블의 데이터가 삭제되면 자식 테이블의 관련 데이터도 삭제되고 후자는 부모 테이블의 데이터가 삭제되면 자식 테이블의 외래 키 값을 NULL로 설정한다.

##### 15. 데이터 무결성을 보장하는 트리거의 역할은 무엇인가요?
- 트리거는 특정 이벤트(INSERT, UPDATE, DELETE)가 발생했을 때 자동으로 실행되는 데이터베이스 객체입니다. 주로 무결성을 유지하고, 자동화된 로직을 적용하는 데 사용됩니다. 

##### 16.트리거 사용 시 주의할 점은 무엇인가요?
- 트리거가 과도하게 사용되면 데이터베이스 성능 저하 및 디버깅 어려움이 발생할 수 있습니다.
