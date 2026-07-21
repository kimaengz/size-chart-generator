# 상세페이지 치수 이미지 생성기

의류 상세페이지용 Product Measurements 이미지를 브라우저에서 만들어 PNG로 내려받는 정적 웹앱입니다.
서버 없이 동작하며 GitHub Pages에 그대로 배포할 수 있습니다.

## 사용법

1. 제품 선택 (티셔츠 / 바지)
2. 치수 항목을 **클릭한 순서대로** 1, 2, 3… 번호가 매겨지고, 그림의 파란 선·번호, 치수 표, 측정 가이드가 함께 갱신됩니다
3. 사이즈(Free, S, M, L…)를 추가하고 각 칸에 치수(cm)를 입력
4. 필요하면 Check Up 섹션을 켜고, 미리보기에서 글자를 클릭해 선택 (선택 = 검은색, 미선택 = 회색)
5. "PNG 이미지 다운로드" → 2배 해상도(880px 폭) PNG 저장

## 파일 구성

| 파일 | 용도 |
|---|---|
| `index.html` | 앱 전체 (배포 필수) |
| `assets.js` | 제품 원본 이미지 base64 인라인 (배포 필수) |
| `html-to-image.js` | PNG 변환 라이브러리 (배포 필수) |
| `assets/` | 원본/레퍼런스 PNG (개발 참고용) |
| `serve.js` | 로컬 확인용 서버 — `node serve.js` → http://localhost:8899 |

## GitHub Pages 배포

```bash
# GitHub에서 새 저장소 생성 후:
git remote add origin https://github.com/<계정>/<저장소>.git
git push -u origin main
```

저장소 → Settings → Pages → Source를 `main` 브랜치 `/ (root)`로 설정하면
`https://<계정>.github.io/<저장소>/` 에서 접속할 수 있습니다.

## 새 제품(이미지) 추가 방법

1. 제품 라인 드로잉 PNG를 base64로 변환해 `assets.js`의 `ASSETS`에 추가
2. `index.html`의 `PRODUCTS`에 항목 추가:
   - `imgW`/`imgH`: 이미지 픽셀 크기
   - `parts`: 부위별 한/영 이름, 측정 가이드 문구, 선 좌표(`lines`, 이미지 픽셀 기준), 번호 배지 위치(`badge`)
