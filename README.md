# motion-hub
스포츠 동호회 커뮤니티

## project
    JAVA 17
    Spring Boot 3.2.2

## entity

    user
        - id
        - account_id
        - name
        - password
        - reg_date

    category
        - id
        - name

    notice ( user: 1 = notice: N, category: 1 = notice: N )
        - id
        - title
        - content
        - user_id
        - category_id
        - reg_date

    comment ( notice:1 = comment: N )
        - id
        - author
        - content
        - notice_id
        - user_id
        - reg_date

    room ( user:1 = room: N, category: 1 = notice: N )
        - id
        - title
        - description
        - user_id
        - category_id
        - reg_date
        
    roomUsers ( room: 1 = roomUsers: N )
        - id
        - user_id
        - reg_date
    

## 기능 정리

    1. 로그인
    - 회원가입, 로그인
    
    2. 공지사항
    - (관리자) 공지사항 글 작성, 수정, 삭제
    - 공지사항 글 조회
    - 공지사항 댓글 작성 및 조회
    
    3. 동호회
    - room 조회, 생성, 수정, 삭제
    - 실시간 채팅