# 🚀 Jetsnack 프로젝트 설정 가이드

## 📋 사전 요구사항

### 1. 개발 환경
- **Android Studio**: Arctic Fox (2020.3.1) 이상
- **JDK**: 17 이상
- **Android SDK**: API 21 (Android 5.0) 이상
- **Gradle**: 8.13 이상

### 2. macOS 환경 설정

#### Java 17 설치 및 설정
```bash
# Homebrew를 통한 Java 17 설치
brew install openjdk@17

# PATH 설정 (터미널에서 실행)
export PATH="/opt/homebrew/opt/openjdk@17/bin:$PATH"

# 영구적으로 설정하려면 ~/.zshrc에 추가
echo 'export PATH="/opt/homebrew/opt/openjdk@17/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

#### Android SDK 설정
```bash
# Android SDK 경로 확인
ls ~/Library/Android/sdk

# 환경 변수 설정
export ANDROID_HOME="/Users/[사용자명]/Library/Android/sdk"
export PATH="$ANDROID_HOME/platform-tools:$PATH"

# 영구적으로 설정하려면 ~/.zshrc에 추가
echo 'export ANDROID_HOME="/Users/[사용자명]/Library/Android/sdk"' >> ~/.zshrc
echo 'export PATH="$ANDROID_HOME/platform-tools:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

## 🛠️ 프로젝트 설정

### 1. 프로젝트 클론
```bash
git clone https://github.com/junsang-dong/vibe-0918-android-jetsnack.git
cd vibe-0918-android-jetsnack
```

### 2. Android Studio에서 프로젝트 열기
1. Android Studio 실행
2. "Open an existing project" 선택
3. `vibe-0918-android-jetsnack` 폴더 선택
4. "Trust Project" 클릭

### 3. Gradle 동기화
- Android Studio에서 "Sync Now" 클릭
- 또는 터미널에서 `./gradlew build` 실행

## 🏃‍♂️ 실행 방법

### 에뮬레이터에서 실행
1. **에뮬레이터 생성** (없는 경우)
   - Android Studio → Tools → AVD Manager
   - "Create Virtual Device" 클릭
   - 원하는 디바이스 선택 (예: Pixel 4)
   - API 21 이상의 시스템 이미지 선택

2. **앱 실행**
   ```bash
   # 터미널에서 실행
   ./gradlew installDebug
   
   # 또는 Android Studio에서 Run 버튼 클릭
   ```

### 실제 디바이스에서 실행
1. **개발자 옵션 활성화**
   - 설정 → 휴대전화 정보 → 빌드 번호 7번 탭

2. **USB 디버깅 활성화**
   - 설정 → 개발자 옵션 → USB 디버깅 활성화

3. **디바이스 연결 및 실행**
   ```bash
   # 연결된 디바이스 확인
   adb devices
   
   # 앱 설치 및 실행
   ./gradlew installDebug
   ```

## 🐛 문제 해결

### 자주 발생하는 오류들

#### 1. Java Runtime 오류
```
Error: Unable to locate a Java Runtime
```
**해결방법**: Java 17 설치 및 PATH 설정

#### 2. Android SDK 경로 오류
```
SDK location not found
```
**해결방법**: `local.properties` 파일에 SDK 경로 설정
```properties
sdk.dir=/Users/[사용자명]/Library/Android/sdk
```

#### 3. Gradle 빌드 오류
```
Build failed with an exception
```
**해결방법**: 클린 빌드 실행
```bash
./gradlew clean
./gradlew build
```

#### 4. 에뮬레이터 연결 오류
```
No devices found
```
**해결방법**: 
- 에뮬레이터가 실행 중인지 확인
- `adb devices` 명령어로 연결 상태 확인
- 에뮬레이터 재시작

## 📚 학습 순서

### 1단계: 프로젝트 구조 파악 (1-2일)
- `app/src/main/java/com/example/jetsnack/` 폴더 구조 이해
- `MainActivity.kt` 분석
- 기본 화면 구성 파악

### 2단계: 디자인 시스템 학습 (2-3일)
- `ui/theme/` 폴더 분석
- 색상, 타이포그래피, 모양 정의 방법
- 테마 적용 방법

### 3단계: 컴포넌트 분석 (3-4일)
- `ui/components/` 폴더의 재사용 컴포넌트 분석
- 커스텀 컴포넌트 작성 방법
- 상태 관리 이해

### 4단계: 레이아웃 학습 (2-3일)
- `Grid.kt`의 커스텀 레이아웃 분석
- Layout API 활용법
- 반응형 레이아웃 구현

### 5단계: 애니메이션 학습 (2-3일)
- `Home.kt`의 애니메이션 코드 분석
- 다양한 애니메이션 API 실습
- 사용자 인터랙션 애니메이션 구현

## 🎯 실습 과제

### 초급 과제
- [ ] 새로운 색상 추가하기
- [ ] 커스텀 버튼 스타일 만들기
- [ ] 간단한 애니메이션 추가하기

### 중급 과제
- [ ] 새로운 화면 추가하기
- [ ] 커스텀 레이아웃 컴포넌트 만들기
- [ ] 복잡한 애니메이션 구현하기

### 고급 과제
- [ ] 새로운 기능 추가하기 (예: 즐겨찾기)
- [ ] 성능 최적화 적용하기
- [ ] 테스트 코드 작성하기

## 📞 도움 요청

문제가 발생하거나 질문이 있으시면:
1. GitHub Issues에 문제 등록
2. 바이브코딩 커뮤니티에 질문
3. 프로젝트 README.md 참조

---

**행복한 코딩 되세요! 🚀**
