---
title: TCP Delayed ACK
date: 2024-11-29 12:00:00
categories: [Network, TCP]
tags: [Network, Transport, TCP, CS]
order : 7
published: true
---

## Delayed ACK

Delayed ACK는 TCP 누적 ACK를 활용한 방법으로  
TCP에서 세그먼트를 받을  때마다 ACK를 보내는 것이 아닌  
조금의 딜레이(RFC 1122에 따르면 최대 500ms)를 가지고 ACK를 보내는 방법입니다.  

ACK를 늦게 보내는 이유는 트래픽을 줄이기 위해서 입니다.  
세그먼트를 받을 때마다 ACK만 담긴 패킷을 보내게 된다면 비효율적인 패킷 전송이 됩니다.  
그렇기에 데이터가 담긴 세그먼트를 전송하거나 조금의 딜레이 이후 ACK를 전송합니다.

## Delayed ACK 단점

전송한 ACK가 손실되거나 지연되어 ACK를 기다리는 송신 측에서  
타임아웃이 발생해 세그먼트를 재전송할 가능성이 높아집니다.
