## 더조은 컴퓨터 아카데미 최종 프로젝트
### 화물 운송 중계 플랫폼
# 🚚 BoxMon (화물 운송 중계 플랫폼)
> 화주(화물)와 차주/운송사를 빠르게 매칭하고, 배차·운송·정산까지 한 번에 관리하는 플랫폼

<img width="200" height="200" alt="image" src="https://github.com/user-attachments/assets/b95c9102-ce33-40f7-9bed-660df8d3de0b" />

[![License](https://img.shields.io/badge/license-MIT-black.svg)](#license)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](#contributing)
[![Made with](https://img.shields.io/badge/made%20with-love-red.svg)](#)

---

## ✨ 핵심 기능
### 화주(Shipper)
- 화물 등록(출발/도착, 상·하차 방식, 톤수/차종, 희망 운임)
- 배차 제안 수신 및 선택(운송사/차주 프로필, 평점/리뷰 기반)
- 운송 상태 실시간 추적(상차/이동/하차/완료)
- 운송 완료 후 정산/세금계산서/영수증 관리

### 차주/운송사(Carrier)
- 배차 공고 탐색 및 지원(조건 필터, 경로/거리 기반 추천)
- 운송 진행 상태 업데이트(상차/하차 증빙 업로드)
- 운송 이력 및 수익 리포트

### 운영/관리(Admin)
- 사용자/차량/서류 승인(KYC, 차량 등록증 등)
- 분쟁/클레임 관리, 평점/리뷰 모니터링
- 운임 정책/수수료/프로모션 관리

---
## 🗺️ 데이터베이스 설계 (ERD)
<img width="3700" height="1733" alt="BoxMong ERD (1)" src="https://github.com/user-attachments/assets/c8af95be-c361-4341-8730-623053d59ab6" />


## 🧩 서비스 흐름
```mermaid
sequenceDiagram
    participant 화주
    participant 시스템
    participant 관리자
    participant 차주

    화주->>시스템: 화물 등록 요청 (물품 정보, 운송비 정보 포함)
    시스템->>시스템: 화주 포인트 잔액 조회
    
    alt  잔액 부족
        시스템-->>화주: 잔액 부족 알림
    else 잔액 충분
        시스템-->>화주: 등록 완료 및 운송비 예약(결제 완료)

    Note over 차주, 시스템: [배차 및 운송 단계]
    차주->>시스템: 화물 조회 및 배차 수락
    시스템-->>차주: 배차 완료 (운송 상태 변경: 배차 완료)
    시스템-->>화주: 차주 매칭 알림 및 위치 공유 시작
    
    차주->>시스템: 운송 상태 변경 (운송 시작 -> 완료)
    시스템-->>화주: 운송 진행 상황 업데이트 (실시간)

    Note over 차주, 시스템: [정산 단계]
    차주->>시스템: 정산 요청
    시스템->>시스템: 예약된 포인트에서 수수료 공제 후 정산 금액 계산
    시스템-->>차주: 정산 내역 조회 및 지급 완료
    end
```
