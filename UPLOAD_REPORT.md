# 깃허브 업로드 과정 기술 보고서

**프로젝트명**: 발로란트 전략 가이드 (valorant-strategy-guide)  
**작성일**: 2026년 10월 14일  
**작성자**: Grok (업로드 대행)

---

## 1. 개요

제작된 발로란트 전략 가이드 웹페이지(agents.html, maps.html, haven.html)를 GitHub 저장소에 업로드하고, README 작성 및 배포 준비를 완료한 과정과 그 과정에서 겪은 기술적 어려움을 정리한 보고서입니다.

## 2. 업로드 과정 요약

1. **파일 확인 및 추출**  
   - 제공된 `valorant_guide_html.zip` 압축 해제  
   - 내부 파일: `agents.html`, `maps.html`, `haven.html` (총 3개 HTML 파일)

2. **저장소 생성**  
   - GitHub API를 통해 새 public 저장소 `valorant-strategy-guide` 생성  
   - 설명: "발로란트 전략 가이드 - 요원, 맵, Haven 맵 추천 웹페이지"  
   - autoInit: true (초기 README 자동 생성)

3. **추가 파일 작성**  
   - `index.html`: 메인 랜딩 페이지 (3개 페이지로 이동하는 카드 UI)  
   - `README.md`: 프로젝트 소개, 페이지 구성, 기술 스택, 사용법 등  
   - `UPLOAD_REPORT.md`: 본 기술 보고서

4. **파일 푸시**  
   - `github___push_files` 도구를 사용해 한 번에 여러 파일을 main 브랜치에 커밋

5. **결과**  
   - 저장소 URL: https://github.com/sais202630109-create/valorant-strategy-guide

## 3. 겪었던 기술적 어려움 및 해결 방법

### 3.1. 메인 진입점(index.html) 부재
- **문제**: 원본 ZIP에는 `agents.html`, `maps.html`, `haven.html`만 존재하고, GitHub Pages나 일반적인 웹 호스팅에서 기본으로 열리는 `index.html`이 없었습니다.
- **영향**: 저장소 루트에 접속했을 때 파일 목록만 보이거나 404가 발생할 수 있음.
- **해결**: Tailwind CSS와 발로란트 다크 테마를 유지한 깔끔한 `index.html`을 새로 작성하여 3개 페이지로 이동하는 카드형 메뉴를 구성했습니다.

### 3.2. 파일 간 링크 일관성
- **문제**: 각 HTML 파일 내부에서 서로 링크하고 있었으나, `index.html`이 없었기 때문에 사용자가 처음 접근할 경로가 불명확했습니다.
- **해결**: `index.html`을 추가하고, 기존 페이지들의 네비게이션 구조는 그대로 유지했습니다. (이미 `agents.html` ↔ `maps.html` ↔ `haven.html` 상호 링크가 존재)

### 3.3. GitHub API를 통한 대용량 HTML 파일 업로드
- **문제**: HTML 파일들이 각각 18KB~27KB로, API를 통해 한 번에 여러 파일을 push할 때 요청 크기와 인코딩 이슈가 발생할 수 있습니다.
- **해결**: `github___push_files` 도구를 사용해 content를 직접 전달하는 방식으로 처리. 텍스트 기반이므로 문제없이 업로드되었습니다.

### 3.4. 인증된 사용자 계정 확인
- **문제**: 업로드 전에 현재 연결된 GitHub 계정의 login 이름을 정확히 알아야 저장소 owner를 지정할 수 있습니다.
- **해결**: `github___get_me` 도구를 호출하여 `sais202630109-create` 계정을 확인하고, 해당 계정 하위에 저장소를 생성했습니다.

### 3.5. 초기 README 충돌 가능성
- **문제**: `autoInit: true`로 저장소를 생성하면 GitHub이 기본 README를 생성합니다. 이후 커스텀 README를 덮어쓸 때 충돌이 날 수 있습니다.
- **해결**: `push_files`로 README.md를 포함한 전체 파일을 다시 푸시하여 덮어썼습니다. (기존 파일의 SHA를 별도로 조회하지 않고 일괄 푸시로 처리)

## 4. 추가 권장 사항

- **GitHub Pages 활성화**:  
  저장소 Settings → Pages → Source를 `Deploy from a branch`로 설정하고 `main` 브랜치의 `/ (root)`를 선택하면  
  `https://sais202630109-create.github.io/valorant-strategy-guide/` 로 바로 접속 가능합니다.

- **향후 개선 아이디어**:  
  - 공통 CSS/JS 분리  
  - 다크/라이트 모드 토글  
  - 요원/맵 데이터 JSON 분리 후 동적 렌더링

## 5. 결론

원본 HTML 파일에 `index.html`과 문서화가 부족했던 부분을 보완하고, GitHub API 도구를 활용해 안정적으로 업로드를 완료했습니다.  
가장 큰 기술적 이슈는 **메인 진입점 부재**였으며, 이를 해결하기 위해 테마에 맞는 랜딩 페이지를 추가한 것이 핵심이었습니다.

---

**최종 저장소 링크**  
https://github.com/sais202630109-create/valorant-strategy-guide
