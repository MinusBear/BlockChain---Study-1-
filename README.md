# BlockChain---Study-1-

### SW빌리지 - 블록체인 기초 강의기록 1일차 
2019.01.14 강의기록

##### 블록체인이란?
---------------------------------------
블록체인 -> '분산장부'
모든 구성원이 동일한 장부를 소지할 수 있는 분산된 장부.

##### 블록체인의 종류
---------------------------------------
퍼블릭 블록체인 / 프라이빗 블록체인

##### 데이터베이스란?
---------------------------------------
여러 사람에 의해 공유되어 사용될 목적으로 통합하여 관리하는 데이터 집합
(출처 : 네이버 지식백과)

##### 블록체인 도입 이전 단계
--------------------------------------
기존에는 거래 장부용 데이터베이스에 데이터를 저장했다. 데이터베이스의 인덱스(자료구조) 테이블( 영어 : index table )은  데이터를 쉽고 빠르게 찾을 수 있도록 한다.

##### 블록체인 도입 - 블록체인 특징: 안정성, 투명성 
-------------------------------------
블록체인은 데이터베이스와 다르게 먼저 블록(데이터를 저장할 수 있는 공간/단위)을 만들고 데이터를 담는다. 여기서 블록에 담는 데이터 '트랜잭션'이라 부른다. (1000~2000개가 한 블록에 보통 담긴다. 

- 블록체인으로 풍부하고 포괄적인 거래 기록을 남길 수 있다. (불필요한 추가로 인해 데이터 용량이 커짐으로써 네트워크 오버헤드가 발생할 수 있다는 주장이 있다.)

- 최대 블록 크기의 제약 - 1메가바이트(Megabyte)
- 블록 발생 시간 - 약 10분의 확인 지연

블록에 담은 뒤에는 SH256해시값(데이터를 가지고 난수를 만든다.)을 뽑는다. 한 블록에 규칙성이 없는 해시값이 생성되어 이 값을 블록에 같이 저장하면 첫번째 블록이 완성된다. > Block#1

두번째 블록도 같은 방법으로 블록을 생성하고 전 블록에 해시값을 복사하고 저장하면 두번째 블록에 해당하는 해시값이 생성된다. > Block#2...(반복)

블록이 해시값들로 체인형태로 연결된 것이 블록체인이다.

<안정성>

이 방식에서 유추할 수 있는 것은 한 블록에 기록을 변경하게 된다면 해시값이 일치하지 않아 블록이 깨진다는 점이다. 따라서 블록체인은 수정이 힘들다. 이러 특성으로 인해 해킹이 어려워 안정적으로 데이터를 관리할 수 있다.
(해시값을 유추해내기 어렵다.)

데이터 기록 (무제한) > 해시값 (제한)

<투명성>

중앙관리형 <-> 분산장부
기존의 거래 방식은 한 기관이 모든 장부를 관리하고 있다면 블록체인은 분산화된 장부를 통해서 투명한 거래 내역을 유지시킨다. (오히려 공개적으로 관리하는 것이 훨씬 더 안전할 것이라 본다. 관리자의 속임수 방지)

##### 블록체인 해킹 (51% 공격)
------------------------------------------
앞서 언급했듯이 해커는 데이터를 고치기는 쉽지만 해시값으로 강화된 보안을 이기기는 어려울 것이라 본다.

해커가 블록체인 내에서 잘못된 오류를 만들어내고 이 주장이 과반수가 넘는다면 데이터를 수정할 수는 있다.

> 전체 네트워크의 51% 이상의 지분을 해커가 갖게 된다면?
진짜와 가짜를 구별하기가 어렵다.

전체 채굴대 N 만대에서 N/2 + a가 해커가 갖게된다면 해킹이 가능.

51% 공격은 실제로 일어나고 있으며 현재를 기준으로도 계속 피해사례가 증가하면서 블록체인 기술 도입에 걸림돌이 되고 있다.

##### Uncle Block
--------------------------------------
[문제상황]
2명의 채굴자(주로 업무: 거래 확인 및 정보 패키징)가 동시에 Nonce 값을 맞췄을 때

앞서 언급하였듯이 블록체인에는 관리자 없이 운영된다. 
채굴자가 Nonce값을 찾았을 시 공표(여러 사람에게 값을 찾은 정보가 전달됨)되어 브로드캐스팅(데이터가 네트워크에 연결된 모든 채굴자에게 전송되는 방식)으로 다른 채굴자가 신호를 받게된다.

2명의 채굴자가 공표한 블록으로 이어지던 블록이 두 갈래로 나뉘어진다. 블록이 살아남기 위해서는 상대적으로 자신의 블록에 더 많은 블록이 생성되야한다. (더 많은 채굴자가 모이면 확률적으로 살아남을 가능성이 높아진다.)

살아남지 못한 블록들의 경우 약 12.5% 깎인 보상을 받게 된다. 그 다음 이어진 블록 또한 같은 비율로 보상이 줄어든다. 이러한 블록들을 'Uncle Block'이라 부른다. 

채굴자는 더 높은 보상을 받기 위해서 긴 줄에 블록을 붙인다. 따라서 자동으로 블록이 정리된다. 경쟁자가 없어보이는 Uncle Block이라도 채굴하는 시간은 같기 때문에 굳이 Uncle Block에 잇지 않아 상용화되지 않는다.

##### 코인전송이 느린 이유
---------------------------------
- 블록 생성 타임
1. 비트코인: 10분
2. 이더리움: 15초

생성 타임을 낮출 시, 더 많은 엉클블록 발생한다. 
- Confirm 
1. Uncle Block 영향
2. 해커가 가짜 블록을 계속 붙인다
