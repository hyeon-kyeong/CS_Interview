# TLS/SSL HandShake

HTTPS에서 클라이언트(브라우저)와 서버(웹 서버)가 암호화 통신을 시작할 수 있도록 신분을 확인하고 필요한 정보를 클라이언트와 서버가 주고 받는 과정

### SSL Handshake 동작 과정

<img src="https://user-images.githubusercontent.com/75103526/213598422-a1f32ff7-a365-4158-9c50-deb1ba9936db.png" width=70% height=70%>
<input type="hidden" value="출처 : Cloudflare">

  * 파란색 박스와 노란색 박스는 네트워크 상에서 전달되는 IP Packet을 의미함

  * 파란색 박스인 SYN, SYN ACK, ACK는 TCP Layer의 3 way handshake로 HTTPS가 TCP 기반의 프로토콜이기 때문에 SSL Handshake에 앞서 연결을 생성하기 위해 실시하는 과정임

  * 노란색 박스의 패킷들이 SSL Handshake를 의미함

  1. 클라이언드는 서버에 연결을 시도하며 <b>Client Hello</b> 패킷을 전송함\
      사용 가능한 Cipher Suite 목록, Seesion ID, SSL Protocol Version, Random byte 등을 전달함
      
      Cipher Suite는 SSL Protocol Version, 인증서 검정,데이터 암호화 프로토콜, Hash 방식등의 정보를 담고 있으며 Cipher Suite의 알고리즘에 따라 데이터를 암호화함

  2. 서버는 클라이언트가 보내온 Client Hello Packet을 받아 Cipher Suite 중 하나를 선택한 다음 클라이언트에게 이를 알림\
      또한 Session ID와 CA 공개 인증서를  <b>Server Hello</b>메세지와 함께 담아 응답함

      CA 인증서에는 앞으로 사용하게 될 대칭키가 생성되기 전, 클라이언트에서 handshake 과정 속 암호화에 사용될 공개키를 담고 있음
      
  3. 클라이언트는 서버가 보낸 CA의 개인키로 암호화되어 있는 SSL 인증서를 모두에게 공개된 CA의 공개키를 사용해 복호화함\
      복화화에 성공하면 해당 인증서가 CA에 의해 서명된 것임을 검증할 수 있고, 어떤 암호화 알고리즘과 Hash 알고리즘을 사용했는지 알 수 있음
      
  4. 서버의 공개키가 SSL 인증서 내부에 없는 경우, 서버가 이를 직접 전달함\
      공개키가 SSL 인증서 내부에 있을 경우 이러한 Server Key Exchange는 생략됨
      
  5. 클라이언트는 데이터 암호화에 사용할 대칭키를 생성 후 SSL 인증서 내부에서 추출한 서버의 공개키를 이용해 함호화하여 서버로 전달함
      해당 대칭키는 SSL Handshake의 목적이자 가장 중요한 수단인 클라이언트와 서버가 주고받는 데이터를 실제 암호화하는 역할을 함
      
  6. 클라이언트와 서버는 서로에게 ChangeCipherSpec 패킷을 전송함으로써 교환할 정보를 모두 교환한 뒤, 통신할 준비가 되었음을 알리고 Finished 패킷을 전송해 SSL Handshake를 종료함
    
    
  * 정리 :
  
    서버는 CA에 사이트 정보와 공개키를 전달해 인증서를 받음
    
    -> 클라이언트는 브라우저에 CA 공개키가 내장되어 있다고 가정
    
    -> Client Hello(암호화 알고리즘 나열 및 전달)
    
    -> Server Hello(암호화 알고리즘 선택)
    
    -> Server Certificate(인증서 전달)
    
    -> Client Key Exchage(데이터를 암호화할 대칭키 전달)
    
    -> Client/Server Hello done(정보 전달 완료)
    
    -> Finished(SSL Handshake 종료)
