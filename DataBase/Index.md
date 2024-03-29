# Index

### DB Index

1. 목적: RDBMS에서 검색 속도를 높이기 위한 기술

    Table의 Column을 색인화 (따로 파일로 저장)

    → 해당 Table의 Record를 Full scan 하지 않음

    → 색인화 된 (B+ Tree 구조) Index 파일 검색으로 검색 속도 향상

<br>

2. 과정: Table을 생성하면, MYD, MYI, FRM 3개의 파일이 생성됨

- FRM: 테이블 구조가 저장되어 있는 파일
- MYD: 실제 데이터가 있는 파일
- MYI: Index정보가 들어가 있는 파일 

<br>

Index를 사용하지 않는 경우, MYI 파일은 비워져 있음. 그러나, 인덱싱하는 경우 MYI 파일이 생성됨. 이후에 사용자가 Select 쿼리로 Index를 사용하는 Column을 탐색 시, MYI 파일의 내용을 검색함.

<br>

3. 단점

- Index 생성시, .mdb 파일 크기가 증가함
- 한 페이지를 동시에 수정할 수 있는 병행성이 줄어듦
- 인덱스 된 Field에서 data를 업데이트하거나, record를 추가 또는 삭제시 성능이 떨어짐
- 데이터 변경 작업이 자주 일어나는 경우, Index를 재작성해야 하므로, 성능에 영향을 미침

<br>

4. 상황 분석

- 사용하면 좋은 경우

    (1) Where 절에서 자주 사용되는 Column

    (2) 외래키가 사용되는 Column

    (3) Join에 자주 사용되는 Column


<br>


- Index 사용을 피해야 하는 경우

    (1) Data 중복도가 높은 Column

    (2) DML이 자주 일어나는 Column



<br>
<br>

5. DML이 일어났을 떄의 상황

- INSERT

    기존 Block에 여유가 없을 때, 새로운 데이터가 입력됨

    → 새로운 Block을 할당받은 후, Key를 옮기는 작업을 수행 (많은 양의 Redo가 기록되고, 유발)

    → Index split 작업 동안, 해당 Block의 Key 값에 대해서 DML이 블로킹 됨. 대기 이벤트 발생

<br>

- DELETE

    [Table과 Index 상황 비교]

    테이블에서 데이터가 delete 되는 경우: 데이터가 지워지고, 다른 데이터가 그 공간을 사용 가능

    Index에서 데이터가 delete 되는 경우: 데이터가 지워지지 않고, 사용 안 됨 표시만 해둠

    → Table의 Data수와 Index의 데이터 수가 다를 수 있음.



<br>

- UPDATE

    Table에서 update가 발생하면 → Index는 Update 할 수 없음

    Index에서는 Delete가 발생한 후, 새로운 작업의 Insert 작업 / 2배의 작업이 소요되어 힘듦

