---
title: TCP Sequence Number와 ACK
date: 2024-11-18 12:00:00
categories: [Network, TCP]
tags: [Network, Transport, TCP, CS]
order : 3
published: true
---

## Sequence Number와 ACK

TCP 프로토콜에서 `패킷의 신뢰성과 순서를 보장`하기 위해 `ACK`와 `Sequence Number`를 사용합니다.

## Sequence Number

`시퀸스 번호(Sequence Number)`는 `데이터의 중복을 방지하고 순서를 식별`하기 위해 사용됩니다.  
시퀸스 번호는 TCP 연결 시 [3Way Handshake](https://bigsungg.github.io/posts/TCP-3-Way-Handshake%EC%99%80-4-Way-Handshake/#3-way-handshake)를 통해 서로의 ISN을 확인합니다.  
또한, `시퀸스 번호는 TCP에서 패킷을 전송할 때마다 데이터의 바이트 크기만큼 증가`합니다.  
예시) 시퀸스 번호가 1000이고 250바이트의 데이터를 보낸다면 다음 시퀸스 번호는 1250이 됩니다.

## ACK

`ACK`는 `수신자가 송신자에게 데이터를 정상적으로 받았다는 것을 알리기 위해` 사용됩니다.  
ACK는 수신한 데이터의 마지막 바이트에 1을 더한 값으로 전송합니다.  
예시) 시퀸스 번호가 1000이고 250바이트의 데이터를 받았다면 ACK는 1250입니다.

## 통신 과정

![Desktop View](/assets/img/TCP/tcp_seq_ack.png)

1. 송신자의 시퀸스 번호가 S이고 L 바이트 크기의 데이터를 전송할 때  
TCP 헤더에 시퀸스 번호 S를 포함하여 수신자에게 전송하고  
이후, 시퀸스 번호의 값을 S + L값으로 변경합니다.

2. 패킷을 받은 수신자에서 패킷에 담겨있는 S + L을 ACK로 전송합니다.

위와 같은 과정은 송신자가 데이터를 보낼 때마다 반복됩니다.

<!-- markdownlint-capture -->
<!-- markdownlint-disable -->
> 송신자가 일정 시간 동안 수신자로부터 이전에 보낸 패킷에 대한 `ACK`를 받지 못하면  
송신자는 `타임아웃`이 발생하여 해당 패킷을 다시 수신자에게 `재전송`합니다.
{: .prompt-info }
<!-- markdownlint-restore -->