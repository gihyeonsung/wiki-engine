---
title   : 오라클 클라우드 보안 규칙 SSH 허용
date    : 2020-06-28 13:31:23 +0900
updated : 2020-06-28 15:21:51 +0900
category: 삽질록
tags    : [ssh, acl]
---

오라클 클라우드에서 SSH 관련해서 ACL을 설정하다 삽질해서 정리한다.

## 뭘 하고 싶었나?

VPC에 있는 서브넷에 모든 소스 (CIDR `0.0.0.0/0`)에서 SSH가 가능하게 설정을 하려고 했다. 그래서 오라클 클라우드에 보안 목록에서 SSH를 설정하고 싶었다.

## 뭐가 문제였나?

내가 SSH를 허용하기 위해서 만든 규칙은 다음과 같았다.

| Stateless | 소스      | IP 프로토콜 | **소스 포트 범위** | 대상 포트 범위 |
| :-:       | :-:       | :-:         | :-:                | :-:            |
| 아니요    | 0.0.0.0/0 | TCP         | **22**             | 22             |

오라클 클라우드 문서에서 보안 규칙을 보면 다음과 같이 말하고 있다.

> Source port: **The port where the traffic originates from.** For TCP or UDP, you can specify all source ports, or optionally specify a single source port number, or a range. 

내가 잘못 이해한 것은 `소스 포트 범위`가 보안 규칙이 클라이언트가 아닌 서버에 대해서 작동한다고 생각했던 것이다.

더 자세하게는 이렇다.

SSH 클라이언트는 server:22에 연결하기 위해서 자신도 가지의 22번을 바인드 하는 것이 아니라 High port number (1024 >=)에서 무작위로 사용한다. 만약 클라이언트에서 SSH를 위한 포트를 미리 고정한다면, 클라이언트는 동시에 한 SSH 세션만 만들 수 있기 때문이다.

따라서 클라이언트는 소스 포트로 높은 포트에서 무작위로 서버에 연결을 시도할 것이고, 보안 그룹은 클라이언트에서 22번만 허용했기 때문에 실패했던 것이다.

## 링크

- [Are SSH destination and source ports identical (symmetric ports)?](https://stackoverflow.com/questions/30616527/are-ssh-destination-and-source-ports-identical-symmetric-ports)
- [What ports will an ssh daemon use outbound?](https://unix.stackexchange.com/questions/206993/what-ports-will-an-ssh-daemon-use-outbound)
- [오라클 클라우드에서 보안 규칙](https://docs.cloud.oracle.com/en-us/iaas/Content/Network/Concepts/securityrules.htm#parts)
