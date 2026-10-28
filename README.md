# Planetspoon

생활 계산기와 Notezi의 개인정보처리방침을 제공하는 정적 웹사이트입니다. HTML과 공통 CSS만 사용하므로 패키지 설치나 빌드가 필요하지 않습니다. JavaScript를 사용하지 않으며, 각 정책은 독립된 HTML 페이지로 직접 열 수 있습니다.

## 페이지

현재 원격 저장소 `planetspoon/planetspoon`의 기본 GitHub Pages 주소를 기준으로 한 **배포 후 URL**입니다.

| 페이지 | URL | 파일 |
| --- | --- | --- |
| 홈페이지 | https://planetspoon.github.io/planetspoon/ | `docs/index.html` |
| 생활 계산기 | https://planetspoon.github.io/planetspoon/calcmate/privacy/ | `docs/calcmate/privacy/index.html` |
| Notezi | https://planetspoon.github.io/planetspoon/notezi/privacy/ | `docs/notezi/privacy/index.html` |

운영자명은 Planetspoon, 문의 이메일은 `planetspoon.support@gmail.com`입니다. 스타일과 아이콘은 `docs/assets/`에서 관리합니다. 모든 내부 경로는 상대 경로이므로 사용자 사이트나 프로젝트 사이트에서 별도의 경로 설정 없이 동작합니다.

생활 계산기의 표시 이름과 소개 문구는 `calcmate-app/app.json`, `calcmate-app/store-assets/listing/ko.json`을 기준으로 2026년 10월 29일 반영했습니다. 프로젝트 식별자와 정책 URL의 경로는 `calcmate`입니다.

Planetspoon 파비콘은 선택된 C안 ‘Quiet orbit’을 SVG로 제작한 `docs/assets/favicon.svg`를 사용합니다. 짙은 녹색 바탕에 연두색 행성과 궤도를 배치했으며, 모든 페이지의 브라우저 아이콘과 헤더 심볼에서 같은 파일을 사용합니다.

## 로컬 확인

저장소 루트에서 실행합니다.

```sh
python3 -m http.server 4173 --bind 127.0.0.1 --directory docs
```

브라우저에서 http://127.0.0.1:4173/ 에 접속합니다. 종료할 때는 터미널에서 `Ctrl+C`를 누릅니다.

## GitHub Actions로 배포

1. [저장소의 Pages 설정](https://github.com/planetspoon/planetspoon/settings/pages)을 엽니다.
2. **Build and deployment → Source → GitHub Actions**를 선택합니다. GitHub Free를 사용하는 경우 저장소가 공개 상태여야 합니다.
3. 변경 사항을 직접 커밋하고 `release` 브랜치에 push합니다. **Settings → Environments → github-pages**에 배포 브랜치 제한이 있으면 `release`를 허용합니다.
4. [Actions](https://github.com/planetspoon/planetspoon/actions)에서 **Deploy GitHub Pages**가 성공했는지 확인합니다. 수동 실행 시 **Run workflow**에서 `release` 브랜치를 선택합니다.
5. 배포 작업에 표시된 HTTPS 주소에서 홈페이지와 두 정책 페이지를 확인합니다.

`.github/workflows/pages.yml`은 GitHub의 공식 정적 사이트 템플릿을 따릅니다. `release`에 push하면 `docs/`만 Pages 아티팩트로 업로드하고 배포합니다. 수동 실행을 포함해 `release` 브랜치에서만 배포 작업을 실행합니다. 저장소 문서와 개발 설정은 배포 대상에 포함하지 않습니다.

Actions를 사용하지 않으려면 워크플로 파일을 삭제하고 Pages의 Source를 **Deploy from a branch**, 브랜치를 **release**, 폴더를 **/docs**로 설정합니다. 두 배포 방식을 동시에 운영할 필요는 없습니다.

계정 루트 주소인 `https://planetspoon.github.io/`를 사용하려면 저장소 이름이 `planetspoon.github.io`여야 합니다. 현재 저장소 이름은 `planetspoon`이므로 기본 주소에 `/planetspoon/`이 포함됩니다. 사용자 지정 도메인을 연결한 경우에는 실제 배포 주소를 사용하세요.

## 앱스토어 연결

배포 성공을 확인한 후 각 앱의 App Store Connect **App Privacy → Privacy Policy URL**에 해당 앱의 정책 URL을 입력합니다. Google Play Console의 개인정보처리방침에도 같은 URL을 사용할 수 있습니다.

앱 안에서도 해당 URL을 열 수 있어야 합니다. 이 저장소는 웹사이트만 관리하며 앱 저장소는 수정하지 않았습니다. 조사 시점에 생활 계산기의 앱 정보 화면에는 정책 설명만 있고 링크 열기 동작이 없었으며, Notezi 설정에도 정책 링크가 없었습니다. 두 앱의 설정 화면에 위 URL을 연결하는 작업이 별도로 필요합니다.

## 정책의 근거와 유지보수

정책은 2026년 10월 28일 로컬의 `calcmate-app`과 `notezi-app` 구현, 설치 의존성, iOS 개인정보 선언을 확인해 작성했습니다. 두 앱의 스토어 등록용 아이콘을 재사용했습니다.

| 정책 항목 | 확인한 구현 |
| --- | --- |
| 생활 계산기 저장 항목 | `src/data/migrations/001_initial_schema.ts`, `src/features/settings/store/settingsStore.ts` |
| 생활 계산기 백업·공유 | `src/features/backup/screens/BackupScreen.tsx`, `src/shared/files/textFiles.ts`, `src/features/results/components/ResultActions.tsx` |
| 생활 계산기 기록 보관 기간 | `src/features/settings/components/RecordRetentionCleanup.tsx`, `src/data/repositories/sqlite/RecordsRepository.ts` |
| Notezi 저장 항목 | `src/db/schema.ts`, `src/features/notes/screens/NoteEditorScreen.tsx` |
| Notezi 백업·복원 사본 | `src/features/backup/backup.ts` |
| Notezi 내보내기·알림·삭제 | `src/features/notes/export.ts`, `src/features/reminders/notifications.ts`, `src/db/queries/notes.ts` |
| 수집·추적 선언 | 각 앱의 `ios/<앱 이름>/PrivacyInfo.xcprivacy`, `package.json` |

공개 전에는 실제 출시 빌드의 SDK·권한·데이터 처리 방식이 본문과 일치하는지 확인합니다. 특히 Notezi의 휴지통, 복원 전 안전 백업, 캐시와 외부 사본은 서로 다른 삭제 대상을 뜻합니다. 문의 이메일을 처리 목적 달성 후 삭제한다는 운영 방침도 실제 문의 관리에 적용해야 합니다.

정보 수집·동기화·광고·분석 기능을 추가하거나 문의 처리 방식이 바뀌면 해당 앱의 HTML 본문과 시행일·최종 수정일을 함께 갱신합니다. 필요한 경우 홈페이지의 요약도 수정합니다.

## 참고 자료

- [GitHub 공식 정적 사이트 워크플로](https://github.com/actions/starter-workflows/blob/main/pages/static.yml)
- [GitHub Pages 배포 소스 설정](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)
- [GitHub Pages 주소 및 접속 정보 처리](https://docs.github.com/en/pages/getting-started-with-github-pages/what-is-github-pages)
- [Apple App Review Guidelines 5.1.1](https://developer.apple.com/app-store/review/guidelines/#data-collection-and-storage)
- [App Store Connect 개인정보처리방침 URL 등록](https://developer.apple.com/help/app-store-connect/manage-app-information/manage-app-privacy/)
- [Obsidian의 요약 중심 개인정보 안내 구성](https://obsidian.md/privacy)
