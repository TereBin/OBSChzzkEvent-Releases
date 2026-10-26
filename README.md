# OBS Chzzk Alerts

치지직에서 새로운 팔로워가 생기면 OBS 화면에 팔로워 닉네임을 표시해 주는 Windows용 도구입니다.

현재는 **팔로우 알림만 지원**합니다. 구독과 후원은 치지직에서 제공하는 기존 알림 기능을 이용해 주세요.

## 바로 가기

- [최신 버전 다운로드](#다운로드)
- [설치 및 업데이트](#설치-및-업데이트)
- [확장 프로그램 등록](#1-브라우저-확장-프로그램-등록)
- [OBS 브라우저 소스 추가](#2-obs-브라우저-소스-추가)
- [사용 방법](#3-사용-방법)
- [문제 해결](#문제-해결)
- [개인정보와 소스 코드](#개인정보와-소스-코드)
- [문제 보고 및 문의](#문제-보고)

## 베타 안내

**OBS Chzzk Alerts는 현재 베타 버전입니다.**

팔로우 알림은 치지직 공식 Open API가 아니라 스트리머 스튜디오 리모컨의 Socket.IO 이벤트를 감지해 표시합니다. 별도의 치지직 API 키는 필요하지 않지만, 치지직이 리모컨의 통신 형식과 호환성을 보장하지는 않습니다.

치지직 리모컨의 주소나 이벤트 형식이 변경되면 알림이 일시적으로 작동하지 않을 수 있습니다. 문제가 발생하면 [문제 해결](#문제-해결)을 확인하고 최신 버전으로 업데이트해 주세요.

## 주요 기능

- 치지직 신규 팔로우 이벤트 자동 감지
- 팔로워 닉네임을 OBS 화면에 약 5초 동안 표시
- 투명 배경의 OBS 브라우저 소스 제공
- Chrome과 Microsoft Edge 지원
- 이벤트를 외부 서버로 보내지 않는 로컬 중계 방식
- 설치 프로그램을 통한 OBS 위치 자동 탐색 및 업데이트

## 다운로드

현재 버전은 `0.1.0`입니다.

- [Windows x64 설치 파일 바로 다운로드](https://github.com/TereBin/obs-chzzk-alerts-releases/releases/download/v0.1.0/obs-chzzk-alerts-0.1.0-windows-x64-setup.exe)
- [수동 설치용 Windows x64 ZIP](https://github.com/TereBin/obs-chzzk-alerts-releases/releases/download/v0.1.0/obs-chzzk-alerts-0.1.0-windows-x64.zip)
- [최신 릴리스 페이지와 변경 사항 보기](https://github.com/TereBin/obs-chzzk-alerts-releases/releases/latest)

일반 사용자는 설치 파일을 권장합니다. ZIP은 수동 설치와 파일 검증 용도입니다. 다운로드한 파일은 릴리스에 첨부된 `SHA256SUMS.txt`와 비교할 수 있습니다.

```powershell
Get-FileHash .\obs-chzzk-alerts-*-windows-x64-setup.exe -Algorithm SHA256
```

## 필요한 프로그램

- Windows 10 또는 Windows 11 64비트
- OBS Studio 64비트
- Chrome 또는 Microsoft Edge
- 치지직 스트리머 스튜디오 리모컨을 사용할 수 있는 계정

OBS Live Editor도 사용한다면 반드시 `0.3.2` 이상으로 업데이트하세요. 이전 `0.3.1`과 함께 사용하면 연결 포트가 충돌합니다.

## 설치 및 업데이트

### 설치

1. OBS Studio를 완전히 종료합니다.
2. 내려받은 `setup.exe`를 실행합니다.
3. Windows 관리자 권한 요청을 승인합니다.
4. 설치가 끝나면 OBS를 실행합니다.

설치 파일은 아직 코드 서명되지 않아 Windows SmartScreen이 표시될 수 있습니다. GitHub 릴리스에서 받은 파일인지 확인하고, 필요한 경우 `추가 정보` → `실행`을 선택하세요.

### 업데이트

1. OBS Studio와 열려 있는 치지직 리모컨 탭을 종료합니다.
2. 최신 설치 파일을 내려받아 실행합니다.
3. 설치가 끝나면 확장 프로그램 관리 화면에서 `OBSChzzk 리모컨 이벤트 브리지`의 새로고침 버튼을 누릅니다.
4. OBS와 치지직 리모컨을 다시 실행합니다.

플러그인은 자동으로 다운로드하거나 설치하지 않습니다. 새 버전은 [최신 릴리스 페이지](https://github.com/TereBin/obs-chzzk-alerts-releases/releases/latest)에서 직접 확인합니다.

## 설정 방법

### 1. 브라우저 확장 프로그램 등록

Chrome은 주소창에 `chrome://extensions`, Edge는 `edge://extensions`를 입력합니다.

1. 오른쪽 위의 `개발자 모드`를 켭니다.
2. `압축해제된 확장 프로그램을 로드`를 누릅니다.
3. 다음 폴더를 선택합니다.

   ```text
   C:\Program Files\obs-studio\data\obs-plugins\obs-chzzk-alerts\browser-relay
   ```

4. `OBSChzzk 리모컨 이벤트 브리지` 버전 `0.2.0`이 활성화됐는지 확인합니다.

업데이트 후에는 확장 프로그램 관리 화면에서 새로고침 버튼을 누르고, 열려 있던 치지직 리모컨 탭도 새로고침해야 합니다.

### 2. OBS 브라우저 소스 추가

1. OBS의 `소스 목록`에서 `+`를 누릅니다.
2. `브라우저`를 선택합니다.
3. `로컬 파일`을 체크합니다.
4. 다음 파일을 선택합니다.

   ```text
   C:\Program Files\obs-studio\data\obs-plugins\obs-chzzk-alerts\browser-source\chzzk-alert.html
   ```

5. 원하는 크기와 화면 위치를 조정합니다. 예시 크기로 `800 × 200`을 사용할 수 있습니다.

### 3. 사용 방법

1. OBS를 먼저 실행합니다.
2. 확장 프로그램을 등록한 Chrome 또는 Edge에서 치지직 스트리머 스튜디오의 `리모컨`을 엽니다.
3. 리모컨 탭을 열어 둔 상태로 방송합니다.
4. 새로운 사용자가 채널을 팔로우하면 OBS 브라우저 소스에 닉네임이 약 5초 동안 표시됩니다.

동일한 계정으로 언팔로우한 뒤 다시 팔로우하면 치지직 서버의 중복 처리 때문에 새 알림이 오지 않을 수 있습니다. 처음 팔로우하는 다른 계정으로 테스트하는 것이 가장 정확합니다.

## 제거

1. OBS Studio를 완전히 종료합니다.
2. Windows의 `설정 > 앱 > 설치된 앱`에서 `OBS Chzzk Alerts`를 제거합니다.
3. Chrome/Edge 확장 프로그램 관리 화면에서 `OBSChzzk 리모컨 이벤트 브리지`를 제거합니다.
4. OBS 소스 목록에 기존 브라우저 소스가 남아 있다면 직접 삭제합니다.

## 문제 해결

### 리모컨에는 팔로우가 보이지만 OBS에는 표시되지 않음

- **확인:** OBS가 실행 중인지, 브라우저 소스가 현재 장면에서 보이는지, 확장 프로그램 `0.2.0`이 활성화됐는지 확인합니다.
- **해결:** 확장 프로그램 관리 화면에서 새로고침 버튼을 누른 뒤 치지직 리모컨 탭도 새로고침합니다. OBS 브라우저 소스의 로컬 파일 경로가 올바른지도 확인합니다.

### 치지직 리모컨에도 새 팔로우가 보이지 않음

- **확인:** 테스트 계정이 채널을 처음 팔로우하는 계정인지 확인합니다.
- **해결:** 동일 계정의 언팔로우 후 재팔로우는 치지직에서 중복 처리될 수 있습니다. 처음 팔로우하는 다른 계정으로 다시 테스트합니다.

### 개발자 도구에 `ERR_CONNECTION_REFUSED`가 표시됨

- **확인:** OBS가 실행 중인지 확인하고, `도움말 > 로그 파일 > 현재 로그 보기`에서 `[obs-chzzk-alerts] plugin loaded`를 검색합니다.
- **해결:** OBS를 완전히 종료한 뒤 최신 설치 파일을 다시 실행합니다. 설치 후 OBS를 먼저 실행하고 리모컨 탭을 새로고침합니다.

### OBS 로그에 포트 또는 플러그인 로드 오류가 표시됨

- **확인:** OBS Live Editor 버전이 `0.3.2` 이상인지 확인합니다. `0.3.1`은 동일한 `21345` 포트를 사용합니다.
- **해결:** OBS Live Editor를 `0.3.2` 이상으로 업데이트합니다. 문제가 계속되면 다른 프로그램이 포트를 사용 중인지 확인한 뒤 OBS를 다시 실행합니다.

### 확장 프로그램 폴더를 찾을 수 없음

- **확인:** 기본 OBS 설치 폴더인 `C:\Program Files\obs-studio`에 플러그인이 설치됐는지 확인합니다.
- **해결:** OBS를 완전히 종료하고 최신 설치 파일을 다시 실행합니다. 포터블 OBS는 현재 설치 프로그램이 자동으로 찾지 못할 수 있습니다.

### 설치 프로그램이 OBS를 찾지 못함

- **확인:** `C:\Program Files\obs-studio\bin\64bit\obs64.exe`가 존재하는지 확인합니다.
- **해결:** 64비트 OBS Studio를 정식 설치 프로그램으로 설치한 뒤 OBS Chzzk Alerts 설치를 다시 시도합니다.

### OBS가 실행 중이라는 안내가 표시됨

- **확인:** 작업 표시줄, 시스템 트레이와 작업 관리자에서 `obs64.exe`가 남아 있는지 확인합니다.
- **해결:** OBS를 완전히 종료한 뒤 설치 파일을 다시 실행합니다.

문제가 계속되면 아래 [문제 보고](#문제-보고)를 참고해 이슈를 등록해 주세요.

## 개인정보와 소스 코드

팔로우 알림은 사용자 컴퓨터 안에서만 전달됩니다. 치지직 리모컨에서 확인한 닉네임을 `127.0.0.1`의 OBS 플러그인으로 전달하며 별도의 외부 서버에 저장하거나 전송하지 않습니다.

확장 프로그램은 치지직 스트리머 스튜디오 리모컨에서만 실행합니다. 치지직 로그인 쿠키, WebSocket 인증값과 전체 이벤트 내용은 OBS 브라우저 소스로 전달하지 않습니다.

소스 코드, 기술 구조와 빌드 방법은 [obs-chzzk-alerts 소스 저장소](https://github.com/TereBin/obs-chzzk-alerts)에서 확인할 수 있습니다. OBS Chzzk Alerts는 GNU General Public License v2.0으로 배포됩니다.

## 문제 보고

오류 보고와 기능 제안은 [OBS Chzzk Alerts Issues](https://github.com/TereBin/obs-chzzk-alerts/issues)를 이용해 주세요. 공개 이슈 작성이 어렵거나 개별 문의가 필요하면 [Discord에서 TereBin에게 문의](https://discordapp.com/users/537256771501424640)할 수 있습니다.

OBS에서 `도움말 > 로그 파일 > 현재 로그 보기`를 선택하고, 문제 발생 직후 로그에서 `[obs-chzzk-alerts]`가 포함된 줄과 Chrome/Edge 확장 프로그램 오류를 함께 제공하면 원인 확인이 빠릅니다.

WebSocket URL의 `auth` 값, 치지직 로그인 쿠키 또는 전체 HAR 파일은 공개 이슈나 Discord에 첨부하지 마세요.

## 후원

OBS Chzzk Alerts가 도움이 되었다면 [Ko-fi에서 TereBin 후원하기](https://ko-fi.com/terebin)를 통해 개발을 응원할 수 있습니다.
