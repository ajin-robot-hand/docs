# Robot Hand Team Blog

MkDocs Material의 blog 플러그인으로 만든 팀 블로그입니다. 각 팀원이 진행한 작업을 `docs/blog/posts/`에 글로 정리합니다.

## 시작하기 전에 (설정 필요)

1. `docs/blog/.authors.yml`에 팀원 프로필을 추가하세요.
2. GitHub 저장소 Settings → Pages → Build and deployment → Source를 **Deploy from a branch**, Branch를 **gh-pages**로 설정하세요 (`main`에 첫 push 후 `.github/workflows/deploy.yml`이 실행되어 `gh-pages` 브랜치를 생성합니다).

## 로컬 개발

```bash
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
mkdocs serve
```

`http://127.0.0.1:8000`에서 확인합니다.

## 새 글 작성

`docs/blog/posts/YYYY-MM-DD-제목.md` 파일을 만들고, `docs/blog/posts/2026-08-12-welcome.md`를 참고해서 front matter(`date`, `categories`, `authors`)를 채우세요. `main` 브랜치에 push하면 자동으로 배포됩니다.

## 배포

`main`에 push되면 GitHub Actions(`.github/workflows/deploy.yml`)가 `mkdocs gh-deploy`를 실행해 `gh-pages` 브랜치로 빌드 결과를 배포합니다.
