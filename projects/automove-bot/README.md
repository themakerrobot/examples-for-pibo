# OpenPibo 마커 기반 자율 주행 및 객체 인식 스크립트
# (OpenPibo Marker-Based Navigation and Object Recognition Script)

## 프로젝트 설명 (Project Description)

이 파이썬 스크립트는 OpenPibo 로봇을 사용하여 ArUco 마커를 따라 지정된 경로를 자율적으로 주행하고, 동시에 카메라 시야 내의 객체를 Teachable Machine 모델을 이용해 분류하는 기능을 수행합니다. 로봇은 정의된 마커 목록 (`MARKER_LIST`)을 순서대로 찾아 이동하며, 마커와의 거리 및 방향에 따라 전진하거나 회전합니다. 마커를 찾지 못할 경우 목을 좌우로 돌려 탐색하는 기능도 포함되어 있습니다.

This Python script enables an OpenPibo robot to autonomously navigate a path defined by ArUco markers while simultaneously classifying objects within its camera view using a Teachable Machine model. The robot follows a predefined sequence of markers (`MARKER_LIST`), moving forward or turning based on the distance and direction to the current target marker. It includes functionality to scan by turning its head if the marker is not immediately visible.

## 주요 기능 (Key Features)

* ArUco 마커를 이용한 경로 추종 (Path following using ArUco markers).
* 마커 ID 순서에 따른 순차적 이동 (Sequential navigation based on marker ID order).
* 마커와의 거리 및 방향에 따른 로봇 제어 (로봇 전진/회전) (Robot control (forward/turn) based on distance and direction to the marker).
* 정면에서 마커 인식 실패 시 목을 좌우로 돌려 재탐색 (Head scanning (left/right) for marker re-detection if not found straight ahead).
* Teachable Machine 모델을 이용한 실시간 객체 분류 (Real-time object classification using a Teachable Machine model).
* 상태 기반 제어 ('직진', '회전') (State-based control: 'Moving Straight', 'Turning').

## 사전 준비 (Prerequisites)

1.  **하드웨어 (Hardware)**:
    * OpenPibo 로봇 (OpenPibo robot).
    * ArUco 마커 세트 (지정된 `MARKER_LIST` ID 포함) (ArUco marker set including IDs specified in `MARKER_LIST`).
    * (선택 사항) Teachable Machine 모델로 학습시킨 객체/카드 (Optional: Objects/cards trained with the Teachable Machine model).
2.  **소프트웨어 (Software)**:
    * Python 3.x
    * `openpibo` 라이브러리
3.  **파일 (Files)**:
    * 이 파이썬 스크립트 파일. (This Python script file).
    * 학습된 Teachable Machine 모델 파일 (`.tflite`) 및 라벨 파일 (`.txt`). 스크립트 내 `tm.load()` 경로에 맞게 위치해야 합니다. (예: `/home/pi/mymodel/model_unquant.tflite`, `/home/pi/mymodel/labels.txt`). (A trained Teachable Machine model file (`.tflite`) and labels file (`.txt`). Must be located according to the path in `tm.load()` within the script, e.g., `/home/pi/mymodel/model_unquant.tflite`, `/home/pi/mymodel/labels.txt`).

## 설정 (Configuration)

스크립트 상단에서 다음 값들을 환경에 맞게 수정할 수 있습니다:

* `MARKER_LENGTH`: 사용하는 ArUco 마커의 실제 한 변 길이 (cm 단위). 거리 측정 정확도에 영향을 줍니다. (The actual side length of the ArUco markers used, in cm. Affects distance measurement accuracy).
* `MARKER_LIST`: 로봇이 따라갈 마커 ID의 순서 목록. (The ordered list of marker IDs for the robot to follow).
* `tm.load()` 경로: Teachable Machine 모델 및 라벨 파일의 실제 경로. (The actual paths to the Teachable Machine model and labels files).
* `get_dirX()` 함수 내 좌표 기준값 (420, 220): 로봇 카메라 해상도 및 원하는 중앙 영역 범위에 따라 조절될 수 있습니다. (Coordinate thresholds (420, 220) within the `get_dirX()` function might need adjustment based on camera resolution and desired center range).

## 실행 방법 (How to Run)

1.  **환경 설정 (Setup Environment)**:
    * 지정된 경로(`MARKER_LIST`)에 따라 ArUco 마커를 로봇이 인식할 수 있도록 배치합니다. (Place the ArUco markers according to the specified path (`MARKER_LIST`) so the robot can recognize them).
    * Teachable Machine 모델 및 라벨 파일이 지정된 경로에 있는지 확인합니다. (Ensure the Teachable Machine model and labels files are in the specified path).
2.  **스크립트 실행 (Execute the Script)**:
    * 터미널을 열고 이 스크립트 파일이 있는 디렉토리로 이동합니다. (Open a terminal and navigate to the directory containing this script file).
    * 다음 명령어를 입력하여 스크립트를 실행합니다: (Run the following command to execute the script:)
        ```bash
        sudo python3 main.py
        ```

## 기능 상세 (Functionality Notes)

* 로봇은 `MARKER_LIST`의 첫 번째 마커부터 찾기 시작합니다.
* 마커를 정면에서 찾으면 거리를 계산하여 30cm 이상이면 직진하고, 30cm 미만이면 다음 마커를 찾기 위해 '회전' 상태로 전환합니다.
* 마커가 좌/우측에 치우쳐 있으면 해당 방향으로 조금씩 회전하며 접근합니다 (`*_half` 모션).
* 정면에서 마커를 찾지 못하면 목을 좌우로 돌려 탐색합니다. 탐색 중 마커를 발견하면 해당 방향으로 몸 전체를 회전합니다.
* 좌우 탐색에도 실패하면 `마커 인식 불가` 메시지를 출력합니다 (추가 동작 정의 필요 시 수정).
* 주행 중 Teachable Machine 모델로 객체를 계속 분류하며, 인식률이 90% 이상일 경우 콘솔에 결과를 출력합니다.
* 마지막 마커에 30cm 이내로 접근하면 "완료" 메시지를 출력하고 프로그램을 종료합니다.
