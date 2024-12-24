# WebRTC
- WebRTC를 위한 샘플코드 레포지토리

## 학습 목표
- WebRTC에 대해서 학습하고 샘플코드를 작성 및 학습

## WebRTC란?
- WebRTC란, 웹 어플리케이션 및 사이트들이 별도의 소프트웨어 없이 음성, 영상 미디어 혹은 텍스트, 파일 같은 데이터를 브라우져끼리 주고 받을 수 있게 만든 기술입니다. WebRTC로 구성된 프로그램들은 별도의 플러그인이나 소프트웨어 없이 P2P 화상회의 및 데이터 공유를 합니다.
즉, 웹 브라우저 상에서는 어떠한 플러그인도 필요 없이 음성 채팅과 화상채팅, 데이터 교환까지도 가능하게 하는 기술 입니다.

## WebRTC 구조
[출처 : https://www.techtarget.com/searchunifiedcommunications/definition/WebRTC-Web-Real-Time-Communications]  
![캡처](/그림1.png)

## STUN / TURN ?
- Stun Server , Turn Server
Web RTC는 P2P에 최적화 되어 있습니다.
즉 Peer들간의 공인 네트워크 주소(IP)를 알아하고 데이터 교환을 해야하는데, 실제 개개인의 컴퓨터는 방화벽등 여러가지 보호장치들이 존재하고 있습니다. 그래서 Peer들간의 연결이 쉽지 않습니다, 이렇게 서로간의 연결을 위한 정보를 공유하여 P2P 통신을 가능하게 해주는 것이 Stun/Turn Server 입니다.

## Signaling Server?
- 시그널링 서버는 WebRTC 기반 애플리케이션에서 클라이언트 간의 연결 설정 및 메타데이터 교환을 담당하는 중개서버 입니다. WebRTC 자체는 미디어를 전송하기 위한 기술이며, 시그널링 서버는 그러한 미디어 전송을 위한 초기 연결을 설정하고 유지하기 위해 사용됩니다.

---

### SDP ( Session Description Protocol )
[참고 문헌](https://ko.wikipedia.org/wiki/%EC%84%B8%EC%85%98_%EA%B8%B0%EC%88%A0_%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C)  
스트리밍 미디어의 초기화 인수를 기술하기 위한 포맷
기본적으로 제안과 수락 모델(offer/answer)로 정의

### 예시 시나리오 ( 1:1 )
[출처 : https://musma.github.io/2023/08/21/WebRTC-%ED%99%94%EC%83%81%ED%9A%8C%EC%9D%98-%EC%84%9C%EB%B2%84-%EA%B5%AC%EC%B6%95.html]
![캡처](/그림2.png)  
1. Alice는 offer를 생성
2. Alice는 생성한 offer를 LocalDescription에 등록
3. Alice는 생성한 offer를 Bob에게 보낸다.
4. Bob은 받은 offer를 RemoteDescription에 등록
5. Bob은 answer를 생성
6. Bob은 생성된 answer를 LocalDescription에 등록
7. Bob은 생성된 answer를 Alice에게 보낸다.
8. Alice는 Bob에게서 받은 answer를 RemoteDescription에 등록
9. ice candidate를 교환
    * 이때 offer/answer를 주고 받기위한 서버가 시그널링 서버  
    
    [출처 : https://musma.github.io/2023/08/21/WebRTC-%ED%99%94%EC%83%81%ED%9A%8C%EC%9D%98-%EC%84%9C%EB%B2%84-%EA%B5%AC%EC%B6%95.html]
    ![캡처](/그림3.png)  

### 예시 시나리오 (N:M) ( room 개념 도입 )
[출처 : https://musma.github.io/2023/08/21/WebRTC-%ED%99%94%EC%83%81%ED%9A%8C%EC%9D%98-%EC%84%9C%EB%B2%84-%EA%B5%AC%EC%B6%95.html]
![캡처](/그림4.png)
- Alice, Bob, Aiden이 서로 통화하는데 그 장소는 roomA  
    1. Alice는 시그널링 서버에게 roomA에 들어가고 싶다고 request
    2. 시그널링 서버는 room 정보(room에 누가 있는지, 몇명이 있는지 등)와 성공 여부를 Alice에게 response
    
- 
    1. 성공했다면 roomA 접속, 현재는 roomA에 아무도 없기에 혼자있는방
        1. Bob이 roomA에 들어가기 위해 시그널링 서버에 request
        2. Bob도 roomA의 정보와 성공여부 response
        3. Bob은 roomA에 있는 모든이들과 offer/answer 교환을 통한 negociation
        4. Aiden도 Bob과 동일
## 브렌치별 설명
- front
    * WebRTC를 사용하기 위한 FRONT 샘플코드
- main
    * WebRTC를 사용하기 위한 BACKEND 샘플코드