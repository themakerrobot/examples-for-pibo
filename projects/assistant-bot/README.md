# OpenPibo 다기능 로봇 스크립트 (OpenPibo Multi-Function Bot Script)

## 프로젝트 설명 (Project Description)

이 파이썬 스크립트는 OpenPibo 로봇을 사용하여 다양한 상호작용 기능을 수행하도록 합니다. 로봇은 다음 기능들을 수행할 수 있습니다:

* 매 분마다 현재 시간을 음성으로 안내합니다.
* 카메라로 사람의 얼굴을 감지하면 인사하고 눈 LED를 켭니다.
* 특정 QR 코드 ("봇카드")를 인식하여 해당하는 기능을 수행합니다:
    * **날씨**: 서울 지역의 현재 날씨 예보를 알려줍니다.
    * **뉴스**: 주요 뉴스 랭킹의 헤드라인을 읽어줍니다.
    * **체조**: 음악과 함께 정해진 체조(춤) 동작을 수행합니다.
    * **대화**: 스크립트를 실행한 터미널을 통해 간단한 질문을 입력받아 답변합니다.
    * **카메라**: 카운트다운 후 사진을 촬영하여 저장합니다.

This Python script enables an OpenPibo robot to perform various interactive tasks. The robot can:

* Announce the current time every minute.
* Greet detected faces using its camera and turn on its eye LEDs.
* Recognize specific QR codes ("Bot Cards") to perform corresponding functions:
    * **Weather (날씨)**: Provides the weather forecast for Seoul.
    * **News (뉴스)**: Reads a top news ranking headline.
    * **Exercise (체조)**: Performs a pre-defined exercise (dance) routine with music.
    * **Conversation (대화)**: Takes simple questions via the terminal running the script and provides answers.
    * **Camera (카메라)**: Takes a photo after a countdown and saves it.

## 실행 방법 (How to Run)

1.  **사전 준비 (Prerequisites)**:
    * OpenPibo 로봇이 준비되어 있고 켜져 있어야 합니다.
    * 스크립트에서 사용하는 이미지 및 오디오 파일들이 `/home/pi/openpibo-files/` 경로 아래에 올바르게 위치해야 합니다. (예: `/home/pi/openpibo-files/image/expression/smile.jpg`, `/home/pi/openpibo-files/audio/music/exercise.mp3` 등)
    * 기능을 실행할 봇카드(QR 코드)가 준비되어 있어야 합니다. (데이터: '날씨', '뉴스', '체조', '대화', '카메라')

2.  **스크립트 실행 (Execute the Script)**:
    * Pibo의 터미널 또는 SSH 연결을 통해 스크립트가 저장된 디렉토리로 이동합니다.
    * 다음 명령어를 입력하여 스크립트를 실행합니다:
        ```bash
        sudo python3 pibo_main.py
        ```

3.  **실행 중 상호작용 (Interaction during execution)**:
    * 로봇이 실행되는 동안 카메라 앞에 얼굴을 보여주거나 봇카드를 보여주면 해당 기능이 작동합니다.