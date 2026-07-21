# 상세페이지 치수 이미지 생성기

의류 상세페이지용 Product Measurements 이미지를 브라우저에서 만들어 PNG로 내려받는 정적 웹앱입니다.
서버 없이 동작하며 GitHub Pages에 그대로 배포할 수 있습니다.

## 사용법

1. 카테고리(반팔/긴팔/후디/셔츠/베스트・가디건/바지・스커트/모자)를 고르고 제품을 선택
2. 치수 항목을 **클릭한 순서대로** 1, 2, 3… 번호가 매겨지고, 그림의 파란 선·번호, 치수 표, 측정 가이드가 함께 갱신됩니다
3. 사이즈(Free, S, M, L…)를 추가하고 각 칸에 치수(cm)를 입력
4. 필요하면 Check Up 섹션을 켜고, 미리보기에서 글자를 클릭해 선택 (선택 = 검은색, 미선택 = 회색)
5. "PNG 이미지 다운로드" → 2배 해상도(880px 폭) PNG 저장

## 지원 제품 (29종)

| 카테고리 | 제품 |
|---|---|
| 반팔 | 반팔티, 반팔셔츠, 반팔래글런, PK티 |
| 긴팔 | 긴팔티, 긴팔래글런 |
| 후디 | 후디, 후디지퍼, 후디지퍼포켓, 후디원포켓, 후디래글런포켓, 후디롱코트 |
| 셔츠 | 셔츠, PK셔츠, V넥, U넥, 하프넥, 하프넥지퍼, 야구점퍼 |
| 베스트・가디건 | 조끼, 가디건V, 가디건U |
| 바지・스커트 | 바지, 반바지, 치마 |
| 모자 | 볼캡 940 KF, 볼캡 JET CAP, 버킷햇, 베레 |

## 파일 구성

| 파일 | 용도 |
|---|---|
| `index.html` | 앱 전체 (배포 필수) |
| `assets.js` | 제품 원본 이미지 base64 인라인 (배포 필수) |
| `products.js` | 제품별 치수 항목/좌표 정의 (배포 필수) |
| `html-to-image.js` | PNG 변환 라이브러리 (배포 필수) |
| `assets/` | 원본/레퍼런스 PNG (개발 참고용) |
| `raw assets/` | 신규 제품 도안 원본 (클린/가이드 버전, 개발 참고용) |
| `serve.js` | 로컬 확인용 서버 (Node.js 필요) |

로컬에서 미리 보려면 이 저장소를 내려받은 뒤 아래 중 하나를 프로젝트 폴더에서 실행하고, 뜨는 주소를 직접 열어야 합니다 (Node.js가 없다면 Python으로 대체 가능).

```bash
node serve.js          # Node.js가 있는 경우 → http://localhost:8899
python3 -m http.server 8899   # Node.js가 없는 경우 → http://localhost:8899
```

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
2. `products.js`의 `PRODUCTS`에 항목 추가:
   - `category`: 사이드바 카테고리 드롭다운에 표시될 그룹명 (`PRODUCT_CATEGORIES`에 없는 값이면 새로 추가)
   - `imgW`/`imgH`: 이미지 픽셀 크기
   - `parts`: 부위별 한/영 이름, 측정 가이드 문구, 선 좌표(`lines`, 이미지 픽셀 기준), 번호 배지 위치(`badge`)
