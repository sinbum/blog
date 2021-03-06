# 기획

누군가와 약속을 잡을떄, 함께 시간을 보내는 것은 중요한 일이다. 그 중 제일 고민되는 것중 하나가 맛집을 찾는것이다.

수많은 광고에 노출되어있는 우리는 신뢰성을 가진 정보를 찾기 힘들다. 그래서 신뢰가능한 진정한 맛집 기록 컨텐츠를 만든다.

# 프로젝트 목표  
**첫째** : 티스토리 API를 통해 나만의 블로그 포스팅을 간편하게 할 수 있도록 앱을 만든다.  
**둘째** : 백엔드 서버를 개발해 신뢰성이 높은 맛집 추천 앱을 만든다.

# 분석,설계

## 티스토리 API 분석
티스토리 API는 Oauth2.0의 인증방식을 채택하고 있다.
API 문서는 해당링크를 참고한다.  
[API 문서 링크](https://tistory.github.io/document-tistory-apis/)

**해당 기능 설명**  
- 블로그 정보
- 글 CURD
  - 글 목록 가져오기
  - 글 읽기
  - 글 작성
  - 글 수정
  - 파일 첨부하기
- 카테고리
- 댓글 CURD
  - 최근 댓글 목록 가져오기
  - 댓글 목록 가져오기
  - 댓글 작성
  - 댓글 수정
  - 댓글 삭제

목표 우선순위)  
1. 해당 블로그 정보를 가져오고 글 쓰기,수정,읽기,삭제(api기능 미지원) 를 우선적으로 기능 구현을 위해 사용한다.
2. 댓글 정보를 가져오고 작성하고 수정하는 작업을 한다.


## 요구사항 분석

우리가 맛집을 찾을 때 가장 신뢰성 있는 글을 확보하는 것이 중요하다.   
맛집이라고 해서 갔는데 실망한 경험들이 많이 있지 않은가? 그런 경험을 최소화 하는 것이 우리의 요구사항이다.  

다음은 유명한 음식 평론가의 인터뷰 사항을 토대로 요구 사항을 분석한다.


### **행동 알고리즘**
다음은 음식평론가가 음식점을 찾는 순간부터 음식을 먹고 나오는 과정을 순번으로 작성한다.
1. 접근성의 유무.
   1. 대중교통으로 접근.
   2. 주차 가능.
   3. 내가 있는 위치에서 거리.
2. 외관을 확인.
   1. 위생상태가 짐작 가능.
   2. 왜 유명한 곳인지 전체적인 느낌.
3. 음식점에 입장.
   1. 테이블 좌석이 편한자리가 있는지.
   2. 쾌적한 환경인지.
   3. 손님응대가 제대로 이루어 지는지.
4. 메뉴판 확인
   1. 메뉴판 디자인이 가독성이 좋은지.
   2. 정보가 상세히 표현되어있는지.
   3. 가격이 적당한지.
5. 주변 사람들의 유형파악
   1. 로컬 피플 인지.
   2. 여행객 인지.
   3. 방문객 나이대.
6. 메뉴 주문 후
   1. 주방의 일하는 직원 수
   2. 멀리서 보이는 위생상태
   3. 테이블 주문대기가 원활히 이루어 지는지.
7. 위생상태 확인
   1. 물컵이나 물 상태 여부.
      1. 가끔 물통을 닦지 않아 물컵 뚜껑에 물곰팡이가 피는 경우 등
   2. 테이블 찐득찐득
   3. 숫젓가락 깨끗.
8. 음식 나올때 까지
   1. 음식이 얼마나 빨리 나오는지.
   2. 음식 모습은 어떤지(플레이팅).
9. 음식 사진 촬영
   1. 전체적인 음식에 대한 상태나 느낌 생각.
   2. 어떤 재료가 들어갔는지.
10. 음식 먹을때
    1. 신선한지.
    2. 식감.
    3. 소금 간.
    4. 건강에 좋을 재료인지.
    5. 양.
       1. 너무 적지 않은지.
       2. 또한 너무 많아 남기기 힘들지 않을지.
    6. 또 먹고싶은지
    7. 얼마나 자주 먹을 수 있는 음식인지.
    8. 다시 와서 먹을만한 음식인지.
11. 음식을 먹은 후
    1. 음식점의 주 타겟팅 분석
       1. 내 주변에서 이음식을 누가 좋아 할 것 같은지.
       2. 어떤 유형의 사람에게 어울릴것 같은지.
       3. 누구랑 같이 오고 싶은지.
    2. 아쉬운 점
       1. 어떤게 보완이 되면 더 좋을것 같아 보이는지.
       2. 실망한 부분이 있는지.
    3. 메뉴 판단.
       1. 추천 메뉴가 있는지.
       2. 시도해 보고 싶은 메뉴가 있는지.
    4. 같은 유형의 경험한 음식점과의 비교.
       1. 예) 파자집 VS 저번주에 간 이태원 피자집.
       2. 내가 알고 있던 곳과 비교함으로써 장,단점 파악.
    5. 이 음식점에 가야 할 이유를 한 마디로 정리.

# 개발