# OpenPibo 로봇 Q&A 웹 인터페이스 (OpenPibo Robot Q&A Web Interface)

## 프로젝트 설명 (Project Description)

이 프로젝트는 FastAPI를 사용하여 OpenPibo 로봇과 상호작용하는 웹 애플리케이션입니다. 사용자는 웹 브라우저를 통해 미리 정의된 로봇 관련 질문 목록을 보고, 질문을 선택하면 연결된 OpenPibo 로봇이 해당 질문에 대한 답변을 수행합니다. 답변은 미리 녹음된 음성 재생, 로봇 모션 실행, 눈 LED 점등의 형태로 이루어집니다. 또한, 웹 인터페이스를 통해 로봇의 음성 재생 볼륨을 조절할 수 있습니다.

This project is a web application built with FastAPI that interacts with an OpenPibo robot. Users can view a list of predefined questions about robots via a web browser. Selecting a question triggers the connected OpenPibo robot to perform the corresponding answer, which involves playing a pre-recorded audio file, executing robot motions, and lighting up its eye LEDs. The application also allows adjusting the robot's audio playback volume through the web interface.

## 주요 기능 (Key Features)

* 웹 기반 인터페이스 제공 (Provides a web-based interface).
* 미리 정의된 질문 목록 표시 (Displays a list of predefined questions).
* 질문 선택 시 로봇 반응 (Robot responds upon question selection):
    * 미리 녹음된 답변 음성 재생 (Plays pre-recorded audio answer).
    * 관련 로봇 모션 수행 (Performs related robot motions).
    * 눈 LED 점등 (Lights up eye LEDs).
* 웹 인터페이스를 통한 로봇 볼륨 조절 기능 (Robot volume control via web interface).

## 사전 준비 (Prerequisites)

1.  **하드웨어 (Hardware)**:
    * OpenPibo 로봇 (OpenPibo robot).
2.  **소프트웨어 (Software)**:
    * Python 3.x
    * 필요한 Python 라이브러리 (Required Python libraries): `fastapi`, `uvicorn`, `pydantic`, `openpibo`.
3.  **파일 및 디렉토리 (Files and Directories)**:
    * 이 FastAPI 스크립트 파일 (예: `main.py`) (This FastAPI script file, e.g., `main.py`).
    * `templates` 라는 이름의 디렉토리. (A directory named `templates`).
    * `templates` 디렉토리 안에 웹 페이지를 정의하는 `index.html` 파일. (An `index.html` file inside the `templates` directory defining the web page).
    * `mp3` 라는 이름의 디렉토리. (A directory named `mp3`).
    * `mp3` 디렉토리 안에 스크립트의 `alist`에 해당하는 답변들이 미리 녹음된 오디오 파일 (예: `answer_0.mp3`, `answer_1.mp3`, ..., `answer_14.mp3`). **주의:** 이 스크립트는 TTS를 실시간으로 생성하지 않으므로, 오디오 파일이 반드시 미리 준비되어 있어야 합니다. (`tts.py` 스크립트 등을 사용하여 생성할 수 있습니다.) (Pre-recorded audio files corresponding to the answers in `alist` must exist inside the `mp3` directory, e.g., `answer_0.mp3`, `answer_1.mp3`, ..., `answer_14.mp3`. **Note:** This script does not perform real-time TTS; the audio files must be prepared beforehand, possibly using the `tts.py` script).

## 실행 방법 (How to Run)

1.  **준비 (Setup)**:
    * 모든 사전 준비 사항(라이브러리 설치, 디렉토리 생성, `index.html` 및 `.mp3` 파일 준비)이 완료되었는지 확인합니다. (Ensure all prerequisites are met: libraries installed, directories created, `index.html` and `.mp3` files prepared).
2.  **서버 시작 (Start the Server)**:
    * 터미널을 열고 이 스크립트 파일(`main.py` 등)이 있는 디렉토리로 이동합니다. (Open a terminal and navigate to the directory containing this script file (e.g., `main.py`)).
    * 다음 명령어를 실행하여 FastAPI 애플리케이션 서버를 시작합니다: (Run the following command to start the FastAPI application server:)
        ```bash
        uvicorn main:app --host 0.0.0.0 --port 10001
        ```
        * `main`은 스크립트 파일명(확장자 제외), `app`은 스크립트 내 FastAPI 인스턴스 이름입니다. (Replace `main` with your script's filename without the extension, and `app` with the FastAPI instance name in your script).
        * `--host 0.0.0.0` 은 Pibo와 같은 네트워크 상의 다른 기기에서 접속 가능하게 합니다. ( `--host 0.0.0.0` allows connections from other devices on the same network as Pibo).
        * `--port 10001` 은 접속 포트 번호입니다. ( `--port 10001` is the connection port number).

## 사용 방법 (Usage)

1.  **웹 페이지 접속 (Access the Web Page)**:
    * Pibo 로봇과 같은 네트워크에 연결된 기기(PC, 스마트폰 등)의 웹 브라우저를 엽니다. (Open a web browser on a device (PC, smartphone, etc.) connected to the same network as the Pibo robot).
    * 주소창에 Pibo 로봇의 IP 주소와 설정된 포트 번호(10001)를 입력합니다. (예: `http://<Pibo의 IP 주소>:10001`). (Enter the Pibo robot's IP address and the configured port number (10001) in the address bar, e.g., `http://<Pibo's IP Address>:10001`).
2.  **질문 선택 (Select a Question)**:
    * 웹 페이지에 표시된 질문 목록에서 원하는 질문을 클릭합니다. (Click on the desired question from the list displayed on the webpage).
3.  **로봇 반응 확인 (Observe Robot Response)**:
    * OpenPibo 로봇이 해당 질문에 대한 답변 음성을 재생하고, 설정된 동작을 수행하며 눈 LED를 켤 것입니다. (The OpenPibo robot will play the audio answer, perform the configured motions, and light up its eyes for the selected question).
4.  **볼륨 조절 (Adjust Volume)**:
    * 웹 페이지 상단의 볼륨 슬라이더를 조절하여 로봇의 음성 재생 볼륨을 변경할 수 있습니다. (You can adjust the robot's audio playback volume using the volume slider at the top of the webpage).
