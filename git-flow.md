# git-flow

## 1단계: develop 브랜치 생성

```bash
# main 브랜치에서 develop 브랜치 생성
git checkout main
git checkout -b develop

# develop 브랜치를 원격으로 푸시
git push -u origin develop
```

## 2단계: 팀원들에게 안내

**팀원들이 해야 할 일:**
```bash
# 원격 저장소에서 최신 정보 받기
git fetch origin

# develop 브랜치로 이동
git checkout develop

# 또는 원격 develop 브랜치 추적하면서 생성
git checkout -b develop origin/develop
```

## 3단계: 브랜치 전략 설명 및 규칙 정하기

### 브랜치 구조
```
main (배포용 - 건드리지 말 것!)
└── develop (개발 메인)
    ├── feature/김철수-login
    ├── feature/이영희-dashboard
    ├── feature/박민수-user-management
    └── bugfix/urgent-fix
```

### 팀 규칙 예시
```bash
# 기능 개발 시작할 때
git checkout develop
git pull origin develop
git checkout -b feature/본인이름-기능명

# 작업 완료 후
git checkout develop
git pull origin develop
git merge feature/본인이름-기능명
git push origin develop
```

## 4단계: GitHub에서 기본 브랜치 변경 (선택사항)

1. GitHub 저장소 → Settings
2. Branches → Default branch를 **develop**으로 변경
3. 이렇게 하면 clone할 때 develop이 기본으로 나옴

## 5단계: 실제 작업 워크플로우

### 새 기능 개발 시
```bash
# 1. develop에서 최신 코드 받기
git checkout develop
git pull origin develop

# 2. 기능 브랜치 생성
git checkout -b feature/login-system

# 3. 작업 후 커밋
git add .
git commit -m "로그인 기능 구현"
git push -u origin feature/login-system

# 4. 완료 후 develop에 병합
git checkout develop
git pull origin develop
git merge feature/login-system
git push origin develop

# 5. 기능 브랜치 삭제 (선택)
git branch -d feature/login-system
git push origin --delete feature/login-system
```

### 배포 준비 시 (팀장이나 담당자)
```bash
# develop에서 release 브랜치 생성
git checkout develop
git checkout -b release/v1.0

# 마지막 점검, 버그 수정 등
git add .
git commit -m "v1.0 릴리즈 준비"

# main으로 병합하여 배포
git checkout main
git merge release/v1.0
git tag v1.0
git push origin main --tags

# develop에도 병합
git checkout develop
git merge release/v1.0
git push origin develop
```

## 브랜치 명명 규칙 정하기

```
feature/이름-기능명     # feature/김철수-login
feature/기능명         # feature/user-auth
bugfix/버그명          # bugfix/login-error
hotfix/긴급수정명      # hotfix/security-patch
release/버전          # release/v1.0.0
```

## 중요한 팀 약속

1. **main 브랜치는 절대 직접 수정 금지**
2. **모든 작업은 develop에서 브랜치 생성**
3. **작업 시작 전 항상 `git pull origin develop`**
4. **커밋 메시지는 명확하게**
5. **큰 기능은 여러 번 나누어 커밋**

이렇게 설정하면 체계적인 협업이 가능해요! 팀원들과 이 규칙을 공유하고 시작하세요.
