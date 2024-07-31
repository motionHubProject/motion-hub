# motion-hub
스포츠 동호회 커뮤니티

## project

    JAVA 17
    Spring Boot 3.2.2

## entity ( 테이블 모델링 )

    user
        - id
        - email
        - name
        - nickname
        - age
        - social ( kakao, naver, google )
        - role ( ROLE_ADMIN/ROLE_USER )
        - reg_date

    userProfile
        - id
        - user_id (FK)
        - profile_img / optional
        - profile_img_dir / optional
        - introduce / optional : 자기 소개
        - interests / optional : 관심 종목 => ex) category에 있는 name들 탁구, 배드민턴 등

    category
        - id
        - name

    notice ( user: 1 = notice: N )
        - id
        - title
        - content
        - user_id (FK)
        - reg_date

    community ( user: 1 = community: N, category: 1 = community: N  )
        - id
        - title
        - content
        - user_id (FK)
        - category_id (FK)
        - reg_date

    comment ( community: 1 = comment: N )
        - id
        - content
        - community_id (FK)
        - user_id (FK)
        - reg_date

    room ( user: 1 = room: N, category: 1 = room: N )
        - id
        - title
        - description / optional
        - area
        - user_id (FK)
        - category_id (FK)
        - reg_date
    
    roomJoin ( room: 1 = rommJoin: N)
        - id
        - title
        - user_id
        - description / optional => ex) 배드민턴 1년 했습니다.., 탁구 신입입니다..
        - confirmYn
        
    roomUsers ( room: 1 = roomUsers: N, user: 1 = roomUsers: N )
        - id / 빼도 될듯
        - room_id (FK)
        - user_id (FK)
        - reg_date
    : IDX_ROOM_USERS_01: room_id
    
    roomChat ( room: 1 = roomChat: N, user: 1 = roomChat: N )
        - id / 빼도 될듯
        - content
        - room_id (FK)
        - sender ( user_id ) (FK)
        - send_time
    : IDX_ROOM_CHAT_01: room_id
        

## 기능 정리

    1. 회원
        1-1. 소셜연동 회원가입, 로그인
        - OAuth2 : 구글/카카오/네이버
        - spring scurity 및 JWT 활용 ( JJWT 라이브러리 등 )
        - ROLE 생성 -> ADMIN, USER 정도

    2. 마이페이지
        2-1. 회원정보수정
        - 닉네임 수정, 프로필사진, 자기소개, 관심종목, 소셜연동 등
    
    3. 공지사항
        3-1. 공지사항 글 작성, 수정, 삭제
        - 관리자 전용?

        3-2. 공지사항 글 조회
        - 페이징 처리

    4. 커뮤니티
        4-1. 등록, 수정, 삭제
        - 운동 카테고리 분류
        
        4-2. 글 조회
        - 페이징 처리
        
        4-2. 댓글 등록, 조회, 삭제
    
    5. 동호회
        5-1. 조회, 생성, 수정, 삭제
        - 동호회 모집을 위한 방
        
        5-2. 가입 신청
        - 동호회 장에게 신청 넣음
        - 폼 내용 거주지, 경력 등

        5-3. 실시간 채팅
        - 웹소켓 라이브러리 사용
    
        5-4. 동호회 기능(수요조사)
        - 동호회 장 역할 부여
        - 번개 모집, 투표, 정산 등

        5-5. 동호회 장의 공지사항
        

## 디렉토리 구조
```cmd
명령어: tree /F | clip
```


## 규칙

    1. 명명규칙 
        1-1. 디렉토리
        - 소문자

        1-2. 클래스
        - PascalCase
        - 명사로 시작
        - EX) HelloWorld, TestWorld
        
        1-3. 인터페이스
        - PascalCase
        - 형용사를 사용
        - EX) Runnable, Remote
        
        1-4. 메서드
        - kamelCase 사용
        - 동사로 시작
        
        1-5. 메서드명의 여러 접두사
        - 속성에 접근: get/set
        - 데이터 생성: create
        - 데이터 조회: find
        - 데이터 변경: modify
        - 데이터 삭제: delete
        - 데이터 입력: input
        - 데이터 초기화: init
        - 데이터 불러오기: load
        - 데이터 유무 확인: has
        - B를 기준으로 A를 하겠다: By
        - EX) public void getUserByName()
        
        1-6. 변수와 상수
        - 변수: kamelCase
        - 상수: 전부 대문자로 표기, 스네이크 케이스 사용


    2. TDD 작성 서비스 / 컨트롤러
    - 서비스( 단위테스트 ) 선, 컨트롤러( 통합테스트 ) 후

    3. 이슈 발행

    4. 기능 별 마일스톤

    5. merge 전, 코드 리뷰
