# 킬로그 외부 보정 서버

FastAPI + OpenCV GrabCut 기반 배경 분리. Python은 Render에서 실행되므로 PC를 초기화해도 운영 가능.

## Render 배포

1. 이 4개 파일(`app.py`, `editor.html`, `requirements.txt`, `render.yaml`)을 개인 GitHub 저장소에 업로드한다.
2. Render에서 **New → Blueprint**를 선택하고 그 저장소를 연결한다. 또는 **New → Web Service** 선택 후 `pip install -r requirements.txt` / `uvicorn app:app --host 0.0.0.0 --port $PORT` 설정, Free 플랜 선택.
3. `https://서비스이름.onrender.com/health`에서 `ok:true`를 확인한다.
4. 제공된 통합 대필 편집기의 킬로그 결과에서 `외부 GrabCut 보정` 버튼을 눌러 서버 주소를 입력한다.

배포 주소는 GitHub와 Render 계정에 연결되어 있으며 노트북과 무관하다.
무료 Render는 사용량 제한과 유휴 절전이 있고, 대량 공개 운영에는 적합하지 않을 수 있다. Render 이용 약관상 16세 미만은 서비스 이용이 허용되지 않는다.

관리자가 전체 사용자에게 자동 연결하려면 `대필편집기_킬로그_Render_클라우드연동_전체_index.html`의 `const SNA_KILL_SERVER_URL='';` 값을 Render 배포 주소로 변경한다. 이 값이 비어 있으면 사용자 브라우저에서 처음 사용할 때 서버 주소를 입력한다.

## 로컬 확인

```
python -m pip install -r requirements.txt
python -m uvicorn app:app --host 127.0.0.1 --port 8000
```

브라우저에서 http://127.0.0.1:8000 접속. 로컬 접속은 동일 컴퓨터에서만 가능.

## 주의

- API는 공개된 URL로 접근 가능하므로 자동화된 남용을 막는 인증과 사용량 제한은 운영 전 추가해야 한다.
- 이미지 업로드를 파일로 저장하지 않지만 공개 서비스는 민감한 사진을 처리할 목적으로 사용하면 안 된다.
- AI가 아닌 GrabCut 특성상 배경과 색이 같은 영역이나 반투명 꼬리는 직접 살리기/지우기 표시가 필요할 수 있다.
