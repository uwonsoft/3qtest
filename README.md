# 인적성평가원 3QTEST 홈페이지 및 검사툴

## 프로젝트 개요

이 프로젝트는 **인적성평가원 3QTEST**의 홈페이지와 검사 툴을 개발하는 프로젝트입니다. 이 프로젝트는 사용자가 인적성 평가를 쉽게 접근하고, 온라인 상에서 검사 결과를 실시간으로 확인할 수 있는 시스템을 목표로 합니다.

### 주요 기능

* **홈페이지**: 3QTEST의 정보와 검사 예약을 지원하는 웹사이트
* **검사 툴**: 온라인으로 인적성 검사를 진행하고 결과를 제공하는 툴
* **실시간 결과 분석**: 사용자에게 실시간으로 검사 결과와 피드백 제공

## 사용 기술

🔹 웹 개발 (Rust + WebAssembly)
* Rust는 WebAssembly(Wasm)으로 컴파일할 수 있어, 웹 브라우저에서 네이티브 수준의 성능을 낼 수 있습니다.

🔹 주요 기술 스택  
* Server : Ubuntu 22.04.4 LTS  
* WebServer : Docker
   ```bash
   // Docker 설치
   
   // 0. 기존 Docker 제거 (에러가 난다면, 그냥 무시하십쇼)
   sudo apt-get remove docker docker-engine docker.io containerd runc

   // 1. 패키지 업데이트
   sudo apt-get update

   // 2. 필수 패키지 설치
   sudo apt-get install apt-transport-https ca-certificates curl software-properties-common

   // 3. Docker 공식 GPG 키 추가
   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

   // 4. Docker 저장소 추가
   echo "deb \[arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg\] https://download.docker.com/linux/ubuntu $(lsb\_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

   // 5. 다시 패키지 업데이트
   sudo apt-get update

   // 6. Docker 및 관련 패키지 설치
   // (막 어떤 서비스를 restart할 거냐고 묻는 화면이 뜨면, 걍 다 스페이스바 눌러서 선택(*로 만들기)하세요)
   sudo apt-get install docker-ce docker-ce-cli containerd.io

   // 7. Docker 설치 확인
   // (에러가 발생하지 않고, Docker version ~라고 뜨면 성공!)
   // (만약 에러가 발생한다면, 죄송합니다 ... 다른 블로그를 참고해보셔요 ...!)
   sudo docker --version

   // 추가1. Docker 서비스 상태 확인
   sudo systemctl start docker

   // 추가2. Docker 서비스 실행
   (서버를 껐다 켜면, Docker를 다시 실행해줘야 하더라구요~)
   sudo systemctl status docker
   ```
   
  

Rust: 성능과 메모리 안전성을 제공
WebAssembly (Wasm): Rust 코드를 브라우저에서 실행 가능
Wasm-bindgen: Rust와 JavaScript 상호작용 도구
Yew / Leptos / Dioxus: Rust 기반의 프론트엔드 프레임워크
Trunk: Rust 웹앱 번들링 도구
🔹 개발 방법
Rust를 WebAssembly로 컴파일
JavaScript 또는 TypeScript로 Wasm과 연동
Yew, Leptos 같은 Rust 프레임워크 활용
💡 Rust 기반의 웹 UI 프레임워크 (Yew, Leptos, Dioxus)를 사용하면 React와 비슷한 방식으로 웹 개발 가능!

2. 하이브리드 앱 개발 (Rust + WebView)
Rust를 활용해 하이브리드 앱을 만들 수도 있습니다. Electron이나 Tauri 같은 프레임워크를 활용하면 됩니다.

🔹 주요 기술 스택
Tauri: Rust 기반의 경량 데스크톱/모바일 앱 프레임워크
Wry: WebView를 활용한 Rust 기반 네이티브 앱 개발
Dioxus (with Tauri): Rust 기반 UI 개발
🔹 개발 방법
Tauri 사용 → Web 기술(HTML, CSS, JS)과 Rust를 조합
Wry 사용 → WebView로 Rust 기반 네이티브 UI 개발
Rust + WebAssembly 조합하여 성능 최적화
💡 Tauri는 Electron보다 가볍고 빠르며, Rust의 성능을 활용할 수 있음!

3. Rust + WebAssembly + Tauri 조합
프론트엔드: Rust(Yew, Leptos) + WebAssembly
백엔드 / 네이티브 기능: Rust (Tauri, Axum, Actix 등)
데스크톱 및 모바일 하이브리드 앱: Tauri

## 프로젝트 구조

1. **backend**: Rust로 작성된 서버 사이드 로직. 검사 데이터 처리 및 사용자 요청에 대한 응답.
2. **frontend**: Dioxus를 사용하여 작성된 사용자 인터페이스. 검사 화면, 결과 화면 등.
3. **database**: 검사 결과 저장 및 사용자 관리용 데이터베이스 (예: PostgreSQL)
4. **API**: RESTful API를 사용하여 백엔드와 프론트엔드 간의 데이터 송수신 처리

## 설치 및 실행 방법

### 요구사항

* Rust (최소 버전 1.55.0)
* Cargo (Rust의 패키지 관리자)
* Node.js (프론트엔드 빌드를 위한 도구)

### 백엔드 실행

1. 프로젝트 디렉토리로 이동

   ```bash
   cd backend
   ```
2. 의존성 설치

   ```bash
   cargo build
   ```
3. 서버 실행

   ```bash
   cargo run
   ```

### 프론트엔드 실행

1. 프로젝트 디렉토리로 이동

   ```bash
   cd frontend
   ```
2. 의존성 설치

   ```bash
   npm install
   ```
3. 로컬 서버 실행

   ```bash
   npm run start
   ```

## 기여 방법

이 프로젝트에 기여하고자 하시면, 먼저 이 저장소를 Fork한 후, 수정한 내용을 Pull Request로 제출해 주세요.

기여 전에 [이슈 트래킹 시스템](https://github.com/your-repo/issues)을 확인하여 먼저 논의할 사항이 있는지 확인하시기 바랍니다.

## 라이선스

이 프로젝트는 [MIT License](LICENSE) 하에 라이선스가 제공됩니다.

---

이 정도로 기본적인 README 초안이 될 것 같습니다. 필요에 따라 프로젝트 세부 사항이나 추가 기능을 설명하는 부분을 더 넣을 수 있습니다. 예를 들어, UI 디자인, 구체적인 검사 툴의 알고리즘, 데이터 처리 방식 등을 추가하면 좋겠죠.
