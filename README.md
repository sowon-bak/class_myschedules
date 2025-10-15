# myschedules

`myschedules`는 일정 관리 및 스케줄링 기능을 제공하는 파이썬 프로젝트입니다.  
수업 일정, 할 일 등을 관리하고 자동화할 수 있는 도구로 설계되어 있습니다.

## 목차

1. 📦 프로젝트 구조  
2. 🚀 주요 기능  
3. 🛠 설치 및 실행 방법  
4. 🧩 사용 예시  
5. 📄 구성 파일  
6. 🧪 테스트  
7. 📜 라이선스  
8. 🙋 기여 안내  

---

## 1. 프로젝트 구조

```
.
├── Makefile
├── docker-compose.yaml
├── init.sql
├── requirements.txt
├── schedule_manager.py
├── setup.py
└── __pycache__/
```

- `schedule_manager.py` — 핵심 스케줄 관리 로직  
- `init.sql` — 초기 데이터베이스 스키마 정의  
- `docker-compose.yaml` — (옵션) 컨테이너 기반 실행 설정  
- `Makefile` — 빌드 및 실행 도우미 명령  
- `requirements.txt` — 의존 패키지 목록  
- `setup.py` — 패키지 설치 스크립트  

---

## 2. 주요 기능

- 일정 생성 / 수정 / 삭제  
- 반복 스케줄 (예: 매일, 매주 등)  
- 데이터베이스를 통한 영속 저장  
- (옵션) 도커 환경에서 실행 가능  
- 패키지 형태로 배포 및 설치 가능  

---

## 3. 설치 및 실행 방법

### 3.1. 개발 환경 (로컬)

```bash
git clone https://github.com/sowon-bak/class_myschedules.git
cd class_myschedules

# 가상 환경 생성 (예: venv)
python -m venv venv
source venv/bin/activate       # macOS/Linux  
venv\Scripts\activate.bat      # Windows

# 의존성 설치
pip install -r requirements.txt

# (선택) 패키지 형태로 설치
pip install -e .
```

### 3.2. 도커 / 도커 컴포즈 사용

```bash
docker-compose up --build
```

이렇게 하면 필요한 서비스들이 컨테이너로 실행됩니다.

### 3.3. 초기 DB 설정

`init.sql` 파일을 사용해 데이터베이스 테이블을 초기화해야 합니다.  
예를 들어, PostgreSQL 또는 MySQL 등의 RDBMS에 이 SQL을 실행하거나, 컨테이너 내부에서 실행하도록 구성할 수 있습니다.

---

## 4. 사용 예시

```python
from schedule_manager import ScheduleManager

sm = ScheduleManager(db_url="sqlite:///schedules.db")

# 일정 추가
sm.add_schedule(
    name="수학 수업",
    start_time="2025-10-20 14:00",
    end_time="2025-10-20 15:30",
    repeat="weekly",
    metadata={"classroom": "101호"}
)

# 일정 조회
schedules = sm.list_schedules()
for s in schedules:
    print(s)

# 일정 수정
sm.update_schedule(schedule_id=1, name="수학 (변경됨)")

# 일정 삭제
sm.remove_schedule(schedule_id=1)
```

---

## 5. 구성 파일 설명

| 파일 | 설명 |
|------|------|
| `requirements.txt` | 필요한 파이썬 패키지 목록 |
| `docker-compose.yaml` | 컨테이너 기반 실행을 위한 설정 |
| `init.sql` | 초기 데이터베이스 스키마 생성 SQL |
| `setup.py` | 패키지 설치 스크립트 |
| `Makefile` | 자주 쓰는 명령을 단축시키는 설정 |
| `schedule_manager.py` | 핵심 로직 (스케줄 CRUD 등) |


---


## 8. 기여 안내

1. 저장소를 fork 합니다.  
2. 브랜치를 만듭니다 (`feature/요청기능` 등)  
3. 코드를 커밋하고 Push 합니다  
4. Pull Request 를 생성합니다  

버그 리포트나 기능 개선 요청은 Issues 탭을 이용해 주세요.
