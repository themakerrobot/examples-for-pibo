# OpenPibo 얼굴 추적 스크립트 (OpenPibo Face Tracking Script)

## 프로젝트 설명 (Project Description)

이 파이썬 스크립트는 OpenPibo 로봇의 카메라를 사용하여 실시간으로 사람의 얼굴을 감지하고, 감지된 얼굴이 화면 중앙에 오도록 로봇의 목(팬/틸트) 모터를 제어하여 얼굴을 추적하는 기능을 구현합니다.

This Python script enables an OpenPibo robot to detect human faces in real-time using its camera and control its neck (pan/tilt) motors to keep the detected face centered in the view, effectively tracking the face.

## 주요 기능 (Key Features)

* 실시간 얼굴 감지 (Real-time face detection).
* 감지된 얼굴의 중심 좌표 계산 (Calculation of the center coordinates of the detected face).
* 얼굴 위치에 따른 목 팬(좌우) 및 틸트(위아래) 모터 자동 제어 (Automatic control of neck pan and tilt motors based on face position).
* 얼굴 추적 상태 시각화 (얼굴 중심 원 및 목표 중앙 영역 표시) (Visualization of tracking status with a circle on the face center and a target center box).

## 사전 준비 (Prerequisites)

1.  **하드웨어 (Hardware)**:
    * OpenPibo 로봇 (OpenPibo robot).
2.  **소프트웨어 (Software)**:
    * Python 3.x
    * `openpibo` 라이브러리.

## 실행 방법 (How to Run)

1.  **스크립트 실행 (Execute the Script)**:
    * 터미널을 열고 스크립트 파일이 있는 디렉토리로 이동합니다. (Open a terminal and navigate to the directory containing the script file).
    * 다음 명령어를 입력하여 스크립트를 실행합니다: (Execute the following command:)
        ```bash
        python3 face_tracker.py
        ```

## 기능 상세 (Functionality Notes)

* 스크립트가 실행되면 로봇은 카메라를 통해 계속 이미지를 캡처하고 얼굴을 찾습니다.
* 얼굴이 감지되면, 얼굴의 중심 좌표를 계산합니다.
* `move()` 함수는 얼굴 중심 좌표가 화면 중앙의 미리 정의된 사각형 영역 (코드 내 `(270,190)` 에서 `(370,290)` 사이) 밖에 있을 경우, 얼굴이 중앙 영역으로 들어오도록 목의 팬(좌우, 모터 4번)과 틸트(상하, 모터 5번) 각도를 조금씩 조정합니다.
* IDE의 카메라 미리보기 창에는 현재 카메라 영상과 함께 감지된 얼굴의 중심(빨간 원) 및 목표 중앙 영역(녹색 사각형)이 표시되어 추적 상태를 시각적으로 확인할 수 있습니다.
* 얼굴이 감지되지 않으면 목 모터는 현재 위치를 유지합니다.