## 조인

#### Q: INNER JOIN과 OUTER JOIN의 차이는 무엇인가요?
INNER JOIN은 양쪽 테이블에서 일치하는 데이터만 반환하는 조인 방식입니다. 반면, OUTER JOIN은 한쪽 테이블에만 있는 데이터도 포함할 수 있습니다. 

 

#### Q: 조인이 무엇인지 간단하게 설명하고, 왜 조인이 필요한지 설명해주세요.
조인은 두 개 이상의 테이블을 결합하여 원하는 데이터를 조회하는 방식입니다.

데이터베이스에서 정규화를 수행하면, 하나의 테이블만으로는 필요한 데이터를 얻기 어려운 경우가 많습니다.

이때 조인을 사용하면 필요한 데이터를 하나의 결과로 합칠 수 있습니다. 그래서 보다 직관적으로 데이터 조회가 가능합니다.

#### Q: 조인 알고리즘의 종류에는 무엇이 있나요?
조인 알고리즘에는 중첩 루프 조인, 병합 조인, 해시 조인 등이 있습니다.

중첩 루프 조인은 작은 테이블을 먼저 읽고, 각 행마다 큰 테이블에서 매칭되는 행을 찾는 방식입니다. 인덱스가 있다면 효율적이지만, 없으면 성능이 떨어질 수 있습니다. OLTP 환경에서 자주 사용됩니다.

병합 조인은 두 테이블이 정렬된 상태에서 병합하며 조인하는 방식입니다. 정렬 비용이 발생할 수 있지만, 이미 정렬된 상태라면 매우 효율적입니다. OLAP 환경에서 많이 사용됩니다.

해시 조인은 작은 테이블을 해시 테이블로 변환한 후, 큰 테이블의 데이터를 해시 테이블과 비교하여 매칭하는 방식입니다.

인덱스가 없을 때도 빠르게 조인할 수 있지만, 해시 테이블을 만들기 위한 추가적인 메모리가 필요합니다. OLAP 환경에서 많이 사용됩니다.

#### Q: OLTP 환경에서 가장 많이 사용되는 조인 방식은 무엇이며, OLTP의 특성과 연관 지어 설명해주세요
OLTP(Online Transaction Processing) 환경에서는 중첩 루프 조인이 가장 많이 사용됩니다.  OLTP 시스템은 실시간 트랜잭션을 처리하는 것이 목적이기 때문에, 빠른 응답 속도가 중요합니다. 중첩 루프 조인은 인덱스를 잘 활용하면 작은 테이블의 데이터를 기반으로 큰 테이블을 빠르게 조회할 수 있기 때문에 OLTP 환경에서 적합합니다.

#### Q: OLAP 환경
OLAP 환경에서는 대량의 데이터를 분석하는 것이 목적이므로, Hash Join이나 Merge Join이 더 적합합니다.

 

#### Q: 드라이빙 테이블과 드리븐 테이블이 존재할 때 결과 집합이 작은 테이블은 둘 중 어떤 테이블로 들어가는 것이 좋을까요?
일반적으로 결과 집합이 작은 테이블을 드라이빙 테이블(Driving Table)로 설정하는 것이 좋습니다.

조인 과정에서 드라이빙 테이블의 각 행을 반복하며, 드리븐 테이블에서 일치하는 데이터를 찾기 때문입니다.

 

#### Q: 작은 쪽 테이블에서 확인해야 하는 레코드 수가 n개이고, 큰 쪽 테이블에서 확인해야 하는 레코드 수가 m개라면, 결국 확인하는 횟수는 n x m이 될 것 같은데 작은 쪽 테이블을 드라이빙 테이블로 사용하는 것이 어째서 성능에 영향을 미치나요?
중첩 루프 조인에서 드라이빙 테이블이 작은 경우 반복 횟수가 줄어듭니다. 드라이빙 테이블이 100개, 드리븐 테이블이 10,000개라면, 100번 반복하며 드리븐 테이블을 조회하는 것이 10,000번 반복하는 것보다 빠릅니다.

그리고 인덱스를 활용할 수 있습니다. 작은 테이블의 데이터를 먼저 조회하고, 해당 데이터를 기반으로 큰 테이블에서 빠르게 검색하면 성능이 향상됩니다.

그리고 캐시 효율성이 높아집니다. 작은 테이블을 먼저 메모리에 로드한 후, 큰 테이블을 검색하면 I/O 부하를 줄일 수 있습니다.

#### Q: 테이블 간 조인을 수행하면 성능이 저하된다고 하는데, 이 서술이 타당한가요? 그에 대한 근거를 들어 설명해주세요.
조인은 기본적으로 연산량이 증가하기 때문에 성능이 저하될 가능성이 있으나 최적화할 수 있습니다.

조인이 성능 저하를 일으키는 이유는 데이터 양이 많아질수록 연산 비용이 증가하고 조인 과정에서 중간 결과 집합을 저장할 때 메모리 사용량이 증가하기 때문입니다.

이를 최적화하려면 먼저 인덱스를 적절히 활용하고, 조인 순서를 최적화해 불필요한 반복을 줄일 수 있습니다.

그리고 필요한 컬럼만 조회하도록 SELECT 절 최적화 조인 전에 WHERE 절을 통해 불필요한 데이터를 미리 걸러내면 성능이 향상됩니다.

***

## 인덱스

#### Q: 인덱스란 무엇이고, 장단점은 무엇인가요?
인덱스는 데이터베이스에서 검색 성능을 향상시키기 위해 사용하는 자료구조입니다. 

인덱스의 장점은 조회 성능을 개선할 수 있다는 점입니다. 특히 WHERE, JOIN, ORDER BY 같은 연산이 포함된 쿼리에서 테이블 전체를 스캔하는 것이 아니라, 인덱스를 활용하여 빠르게 필요한 데이터를 찾을 수 있습니다.

단점은 먼저 쓰기 연산의 성능 저하입니다. 데이터를 삽입, 수정, 삭제할 때마다 인덱스도 함께 업데이트되어야 하기 때문에 오버헤드가 발생합니다.

그리고 추가적인 저장 공간이 필요하다는 점입니다. 인덱스를 저장하기 위한 별도의 공간이 필요하며, 테이블에 인덱스가 많아질수록 관리 비용이 증가할 수 있습니다.

따라서 무조건 많은 인덱스를 추가하는 것이 아니라, 적절한 개수를 유지하는 것이 중요합니다.

 

#### Q: DBMS는 인덱스를 어떻게 관리하나요?
DBMS에서 인덱스는 주로 B-Tree 구조를 사용해서 관리됩니다.

B-Tree는 균형이 유지되는 트리 구조로, 검색, 삽입, 삭제 연산을 수행할 때도 일정한 성능을 유지할 수 있습니다. 

그리고 해시 인덱스 방식이 있습니다. 이 방식은 컬럼 값으로 생성된 해시를 기반으로 인덱스를 구현하기 때문에 특정 키 값에 대해 빠르게 데이터를 찾을 때 사용됩니다. 하지만 연속적인 데이터의 순차 검색이 불가능하기 때문에 이 외의 경우에는 사용에 적합하지 않습니다.

 

#### Q: 인덱스를 사용할 때 유의해야 할 점은 무엇인가요?
먼저 너무 많은 인덱스를 만들면 안 됩니다. 조회 성능은 향상되지만, 삽입/수정/삭제 연산에서 성능 저하가 발생할 수 있습니다.
그리고 컬럼의 선택도가 낮으면 인덱스의 효과가 떨어집니다. 예를 들어, Boolean처럼 값이 두 개뿐인 컬럼에 인덱스를 걸면, 테이블의 절반을 읽어야 하는 경우가 많아 오히려 비효율적일 수 있습니다.
또한, 인덱스는 정렬과 범위 검색을 고려해서 생성해야 합니다. 잘못된 방식으로 만들면 인덱스를 사용하지 못하는 경우가 발생할 수 있습니다.

 

#### Q: 인덱스가 있음에도 불구하고 인덱스를 타지 않는 경우는 어떤 것이 있나요?
먼저 LIKE 연산에서 앞부분에 와일드카드(%)가 있는 경우가 있습니다. 

그리고 데이터 타입이 맞지 않는 경우가 있습니다. VARCHAR 컬럼을 INT로 변환하여 비교하는 경우에는 인덱스를 사용할 수 없습니다.

그리고 컬럼에 함수가 적용된 경우 입니다. 이 경우에는 인덱스가 무효화됩니다.

또한 데이터가 적을 경우, 옵티마이저가 판단하기에 테이블 전체 스캔이 더 빠르다면 인덱스를 사용하지 않을 수 있습니다.

 

#### Q: 결합 인덱스란 무엇인가요?
결합 인덱스(Composite Index)는 두 개 이상의 컬럼을 묶어서 만든 인덱스입니다. 예를 들어 (A, B, C)라는 결합 인덱스를 만들면, A 단독 검색뿐만 아니라 (A, B), (A, B, C) 조합으로도 인덱스를 활용할 수 있습니다. 하지만 왼쪽부터 순서대로 사용하는 원칙이 있어, B나 C만 단독으로 검색하면 인덱스를 활용할 수 없습니다. 

#### Q: 클러스터형 인덱스와 넌클러스터형 인덱스의 차이점은 무엇인가요?
클러스터형 인덱스(Clustered Index)는 데이터가 인덱스의 정렬 순서에 따라 저장되는 방식입니다. 그래서 인덱스의 정렬 순서대로 물리적인 데이터가 배치됩니다. MySQL의 InnoDB에서 기본 키는 자동으로 클러스터형 인덱스로 설정됩니다.

반면, 넌클러스터형 인덱스(Non-Clustered Index)는 실제 데이터와 별도로 저장되는 인덱스입니다. 인덱스를 통해 찾은 후 다시 실제 데이터가 저장된 곳을 한 번 더 조회해야 합니다.

 

#### Q: 데이터베이스 인덱스를 선택하는 기준은 무엇인가요?
인덱스를 선택할 때는 조회 성능 향상을 고려해야 합니다.

조회 빈도가 높은 컬럼인지, WHERE, JOIN, ORDER BY에 자주 사용되는 컬럼인지 확인합니다.

그리고 값이 다양한 컬럼, 선택도가 높은 컬럼을 우선적으로 인덱싱합니다.

#### Q: MySQL에서 적절한 인덱스 개수는 어떻게 정하나요?
일반적으로는 한 테이블당 3~5개 정도의 인덱스가 적절하다고 합니다. 하지만 테이블 크기와 쿼리 패턴에 따라 다를 수 있습니다.

너무 많은 인덱스를 추가하면 데이터 변경 작업의 성능이 저하될 수 있으므로, 반드시 필요한 인덱스만 유지하도록 해야합니다.

 

#### Q: Boolean 컬럼에도 인덱스를 거는 것이 좋을까요?
보통 Boolean 컬럼은 값의 개수가 적기 때문에 인덱스의 효과가 크지 않습니다.

만약 WHERE 조건에서 해당 컬럼이 자주 사용되고, 데이터 분포가 한쪽으로 치우치지 않은 경우라면 인덱스가 도움이 될 수도 있습니다.

 

#### Q: 트리 기반 인덱스와 해시 기반 인덱스의 차이점은 무엇인가요?
트리 기반 인덱스(B-Tree)는 범위 검색, 정렬이 필요한 경우에 적합합니다.

반면, 해시 기반 인덱스(Hash Index)는 정확한 값 하나를 빠르게 찾을 때 사용됩니다. 
