▶️my notion (kakao login -oauth2 study) :
https://whispering-shoemaker-e1d.notion.site/Kakao-Login-18245e7562a5808eb3a8efcdaea8bcbb?pvs=4

<img width="648" alt="스크린샷 2025-02-01 오후 11 15 36" src="https://github.com/user-attachments/assets/1a37e00c-5f8e-4175-b8b5-d3be75069949" />

##카카오서버 (OAuth2) 

→ user의 인증 처리를 위한 또 하나의 서버 

  즉 **user는 카카오에서 한번 , 서버단에서 한번 총 2번**의 인증을 거치는 거임

##### 카카오에서 보낸 토큰 :  본인 인증 (신원 확인 수단 )

ex) 신분증 (주민등록증/운전면허증)

###### 서버에서 받은 토큰 :  우리 싸이트 회원 인증 (회원 인증 수단)

ex) 회사 출입증 



### ##server 에서  구현해야 할 것

1. 클라이언트에서 받은 인가 코드를 kakao OAuth2 에게 보내어 엑세스 토큰을 받아오는 로직 
2. 받아온 엑세스 토큰을 다시 kakao OAuth2 에게 보내어 user의 email 을 받아오는 로직 
3. 사용자 정보 처리 로직
"받아온 email로 userEntity 조회 후 기존사용자면 필요한 정보 업데이트 , 새로운 사용자면 회원가입 처리
Optional<User> existingUser = userRepository.findByKakaoId(kakaoUserInfo.getId());
4. jwt 토큰 발급 로직(login)
5. 리프레쉬 토큰 갱신 로직 + 더 강한 보안을 원한다면
db에 리프레쉬 토큰을 저장하여 이를 조회하고 비교하는 식으로
유효성을 검증할 수 있다고 함
(로그아웃시 db에서 리프레쉬 토큰도 함께 삭제되도록 구현)

