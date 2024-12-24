---
title: TCP 3 Way Handshake 4 Way Handshake
date: 2024-11-17 13:00:00 
categories: [Network, TCP]
tags: [Network, Transport, TCP, CS]
order : 2
published: true
---

## 3 Way Handshake

3 Way Handshake는 TCP에서 클라이언트와 서버의 연결을 위해 거치는 과정을 의미합니다.  

### 3 Way Handshake과정

![Desktop View](/assets/img/TCP/tcp_3_way_handshake.png)

1. 클라이언트가 서버에게  
클라이언트의 ISN(Initial Sequence Number)를 담은  SYN을 보낸 후 SYN_SENT 상태가 됩니다.  

2. 클라이언트의 SYN을 받은 서버에서   
서버의 ISN를 담은 SYN과 클라이언트의 ISN에 대한 ACK를 보낸 후 SYN_RCVD 상태가 됩니다.  

3. 서버의 SYN을 받은 클라이언트에서  
서버의 ISN에 대한 ACK를 보낸 후 ESTABLISHED 상태가 되고  
클라이언트의 ACK를 받은 서버도 ESTABLISHED 상태가 되고 연결을 완료합니다.

## 4 Way Handshake

4 Way Handshake는 TCP에서 클라이언트와 서버의 연결 종료를 위해 거치는 과정을 의미합니다.  

### 4 Way Handshake 과정

![Desktop View](/assets/img/TCP/tcp_4_way_handshake.png)

1. 클라이언트가 서버에게 FIN을 보낸 후 FIN_WAIT_1 상태가 됩니다.

2. 클라이언트의 FIN을 받은 서버에서 FIN에 대한 ACK를 보낸 후 CLOSE_WAIT 상태가 되고  
이후 전송 대기 중인 모든 패킷을 전송합니다.

3. 서버에서 전송 대기 중인 패킷이 없다면 클라이언트에게 FIN을 보낸 후 LAST_ACK 상태가 됩니다.

4. 서버의 FIN을 받은 클라이언트에서 FIN에 대한 ACK를 보낸 후 TIME_WAIT 상태가 되고  
일정 시간이 지나면 연결을 종료하고 클라이언트의 ACK를 받은 서버도 연결을 종료합니다.

### TIME_WAIT 상태에서 일정 시간 이후 연결을 종료하는 이유

클라이언트가 서버의 FIN을 수신한 후 일정 시간 이후 연결을 종료하는 이유는  
만약 클라이언트가 FIN을 수신한 후 바로 연결을 종료하였다면  
서버에서 FIN을 보내기 전에 전송하였던 패킷이 FIN보다 늦게 도착하였을 때  
늦게 도착한 패킷이 정상적으로 처리될 수 없기 때문에  
TCP의 안정성 신뢰성을 보장하기 위해 TIME_WAIT 상태에서 일정 시간 이후 연결을 종료합니다.