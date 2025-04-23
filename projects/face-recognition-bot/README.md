# OpenPibo 얼굴 학습 및 인식 시스템 (OpenPibo Face Training and Recognition System)

## 프로젝트 설명 (Project Description)

이 프로젝트는 OpenPibo 로봇을 사용하여 얼굴 인식 기능을 구현하는 두 개의 파이썬 스크립트로 구성됩니다:

1.  **얼굴 학습 스크립트 (`face_training.py`)**: 로봇 카메라로 얼굴을 감지하고, 특정 이름(예: '홍길동')으로 해당 얼굴 데이터를 학습시킨 후, 학습된 데이터를 파일(`facedb`)로 저장합니다.
2.  **얼굴 인식 스크립트 (`main.py`)**: 저장된 얼굴 데이터베이스(`facedb`)를 로드(선택 사항)하고, 카메라로 실시간 얼굴을 감지합니다. 감지된 얼굴이 이미지 경계 내에 있을 경우, 데이터베이스와 비교하여 등록된 사용자인지('이름') 또는 미등록 사용자인지('Guest') 식별하고 결과를 화면에 표시합니다.

This project consists of two Python scripts that implement face recognition functionality using an OpenPibo robot:

1.  **Face Training Script (`face_training.py`)**: Detects a face using the robot's camera, trains the face data under a specific name (e.g., '홍길동'), and saves the trained data to a file (`facedb`).
2.  **Face Recognition Script (`main.py`)**: Optionally loads the saved face database (`facedb`) and detects faces in real-time via the camera. If a detected face is within the image boundaries, it compares it against the database to identify whether it's a registered user ('Name') or an unregistered user ('Guest') and displays the result.

## 포함된 파일 (Included Files)

* `face_training.py`: 얼굴 감지 및 학습, 데이터베이스 저장 스크립트 (Face detection, training, and database saving script).
* `main.py`: 얼굴 감지, (선택적) 데이터베이스 로딩, 얼굴 인식 및 결과 표시 스크립트 (Face detection, optional database loading, face recognition, and result display script).

## 사전 준비 (Prerequisites)

1.  **하드웨어 (Hardware)**:
    * OpenPibo 로봇 (OpenPibo robot).
2.  **소프트웨어 (Software)**:
    * Python 3.x
    * `openpibo` 라이브러리. 다음 명령어로 설치: (`openpibo` library. Install using:)
        ```bash
        pip install openpibo opencv-python
        ```
3.  **디렉토리 (Directory)**:
    * 얼굴 데이터베이스 파일(`facedb`)을 저장할 디렉토리 (예: `/home/pi/code/`). 스크립트 내 경로와 일치해야 합니다. (A directory to store the face database file (`facedb`), e.g., `/home/pi/code/`. Must match the path in the scripts).

## 사용 방법 (How to Use)

1.  **얼굴 학습 (Train Face - Run `face_training.py`)**:
    * `face_training.py` 스크립트를 엽니다.
    * 학습시킬 사람의 이름 (현재 '홍길동'으로 하드코딩됨)을 필요에 따라 수정합니다.
    * 데이터베이스 저장 경로 (`_face.save_db`)가 올바른지 확인합니다.
    * 스크립트를 실행합니다: `python face_training.py`
    * 카메라에 학습시킬 사람의 얼굴을 보여줍니다. 스크립트는 감지된 첫 번째 얼굴을 사용하여 학습하고 지정된 경로에 `facedb` 파일을 저장(또는 갱신)합니다.
    * 여러 사람을 학습시키거나 한 사람의 데이터를 추가하려면, 이름을 변경하고 스크립트를 반복 실행합니다. (기존 데이터에 추가 학습하려면 `_face.load_db` 주석 해제 필요).

2.  **얼굴 인식 (Recognize Face - Run `main.py`)**:
    * `main.py` 스크립트를 엽니다.
    * 학습된 데이터베이스를 사용하려면 `_face.load_db` 라인의 주석을 해제하고, `face_training.py`에서 저장한 `facedb` 파일의 정확한 경로를 지정합니다.
    * 스크립트를 실행합니다: `python3 main.py`
    * 로봇 카메라 앞에 얼굴을 보여줍니다.
    * 스크립트는 얼굴을 감지하고, 얼굴이 화면 경계 내에 있는지 확인한 후, 로드된 데이터베이스와 비교하여 인식 결과를 화면에 텍스트로 표시합니다 ('[이름] 님, 인증되었습니다.' 또는 '인증이 거절되었습니다.').

## 주요 참고 사항 (Key Notes)

* **학습 시 이름**: `face_training.py` 에서는 학습 대상의 이름이 '홍길동'으로 고정되어 있습니다. 다른 이름으로 학습시키려면 코드 내에서 직접 수정해야 합니다.
* **데이터베이스 로딩**:
    * `face_training.py`에서 이어서 학습하려면 `_face.load_db` 주석을 해제해야 기존 데이터가 유지됩니다.
    * `main.py`에서 학습된 데이터를 사용하려면 반드시 `_face.load_db` 주석을 해제하고 올바른 경로를 지정해야 합니다.
* **경계 확인**: `main.py`는 인식 전에 감지된 얼굴이 카메라 화면 가장자리에 걸치지 않는지 확인하는 `errorCheck` 함수를 포함합니다. 경계를 벗어난 얼굴은 인식 시도를 하지 않습니다.
* **파일 경로**: 스크립트 내의 `/home/pi/code/` 경로는 실제 `facedb` 파일을 저장하고 불러올 경로로 적절히 수정해야 합니다.