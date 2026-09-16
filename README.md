# 대전 쓰레기통 지도 - GitHub + Vercel 배포 안내

## 폴더 구성
- `index.html` — 지도 앱 본체 (저장: JSONBin.io / AI: Google Gemini API)
- `api/analyze.js` — Gemini API를 안전하게 호출하는 서버 함수 (키는 환경변수로만 사용, 코드에 없음)
- `.gitignore` — 불필요한 파일 제외

Vercel은 `api/` 폴더 안의 `.js` 파일을 자동으로 서버 함수로 인식해요. 별도 설정 파일이 필요 없어요.

## 1) GitHub에 올리기

### git이 설치되어 있다면
```
git remote add origin https://github.com/<내계정>/<저장소이름>.git
git branch -M main
git push -u origin main
```
(이 폴더는 이미 `git init` + 첫 커밋까지 되어있어요.)

### git이 없다면 (웹으로 업로드)
1. github.com 에서 새 저장소(Repository)를 만듭니다.
2. 저장소 페이지에서 **Add file → Upload files**를 누릅니다.
3. 이 폴더 전체(`index.html`, `api` 폴더 등)를 그대로 드래그해서 올리고 **Commit changes**를 누릅니다.
   (`api/analyze.js`의 폴더 구조가 그대로 유지돼야 해요.)

## 2) Vercel과 GitHub 저장소 연결하기
1. vercel.com 에서 로그인 후 **Add New → Project**
2. 방금 만든 GitHub 저장소를 선택하고 **Import**
3. Framework Preset은 "Other"로 두고 그대로 **Deploy** 클릭 (설정 건드릴 것 없어요)

## 3) 환경변수 등록 (Gemini API 키)
1. Vercel 프로젝트 대시보드 → **Settings → Environment Variables**
2. 새 변수 추가: 이름 `GEMINI_API_KEY`, 값은 Google AI Studio에서 발급받은 키(`AIza`로 시작)
3. **Deployments → 맨 위 배포 옆 ⋯ → Redeploy**로 재배포해야 적용돼요

## 아직 채워야 할 값
`index.html` 안에 `___JSONBIN_ID___`, `___JSONBIN_KEY___` 자리표시자가 있어요.
JSONBin.io의 Bin ID와 X-Master-Key를 알려주시면 Claude가 채워서 다시 드립니다.
(이 값들은 공개돼도 안전한 값이라 코드/GitHub에 그대로 들어가도 괜찮아요.)
