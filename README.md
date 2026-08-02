# 말랑오락실

모여서 하는 미니게임 파티 웹앱. 방을 만들고 4자리 코드로 참여해서
여러 판의 미니게임을 겨루고 총점으로 순위를 가린다.

## 기술 구성

- 단일 HTML 파일 (빌드 과정 없음)
- Firebase Realtime Database로 방/점수 동기화
- Vercel 정적 호스팅

## 로컬 실행

모듈 임포트 때문에 `file://` 로는 열리지 않는다. 정적 서버가 필요하다.

```bash
python3 -m http.server 8000
# http://localhost:8000
```

## 게임 목록

반응속도 · 7초 · 10초 감각 · 덧셈 · 곱셈 · 답 고르기 · 가까운 쪽 ·
스트룹 · 역 가위바위보 · 순서 암기 · 짝 맞추기 · 다른 색 · 순서대로 ·
개수 세기 · 원 그리기 · 슬라이더 · 두더지 · 도망가는 원 · 눈치게임 · 소수파

## 데이터 구조

```
rooms/{4자리코드}/
  host, state, round, total, mode, gameId, briefAt, used
  players/{닉네임}/ { c, score, seat, online }
  rounds/{n}/{닉네임}/ { v, label, hi, tb }
  rounds/{n}/_res      정렬된 결과와 획득 점수
  live/{n}/            눈치게임 taps, 소수파 picks
```

방장 클라이언트가 점수 집계와 상태 전환을 담당한다.
