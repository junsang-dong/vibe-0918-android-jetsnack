# 🍿 Jetsnack - 구름 JUN 바이브코딩 안드로이드 앱 프로젝트

> **Jetpack Compose를 활용한 스낵 주문 앱으로 바이브코딩 입문자를 위한 실습 프로젝트**
> https://nextplatform.net/vibecoding-android-studio-cursor-app-build/

![Jetsnack Demo](android-2025-compose-samples/readme/screenshots/Jetsnack.png)

## 📋 프로젝트 개요

Jetsnack은 Google의 공식 Jetpack Compose 샘플 프로젝트로, 현대적인 안드로이드 앱 개발의 핵심 기술들을 학습할 수 있는 완벽한 예제입니다. 바이브코딩 입문자들이 안드로이드 앱 개발의 전 과정을 체험할 수 있도록 구성되었습니다.

### 🎯 학습 목표
- **Jetpack Compose** 기반의 현대적 UI 개발
- **커스텀 디자인 시스템** 구현
- **커스텀 레이아웃** 작성
- **애니메이션** 적용
- **Material Design 3** 활용
- **안드로이드 앱 빌드 및 배포** 과정

## 🚀 프로젝트 특징

### ✨ 주요 기능
- 🛒 **스낵 주문 시스템**: 다양한 스낵을 탐색하고 주문할 수 있는 인터페이스
- 🎨 **커스텀 디자인 시스템**: 브랜드에 맞는 색상, 타이포그래피, 모양 정의
- 📱 **반응형 레이아웃**: 다양한 화면 크기에 대응하는 적응형 UI
- 🎭 **부드러운 애니메이션**: 사용자 경험을 향상시키는 다양한 애니메이션 효과
- 🌙 **다크/라이트 테마**: 시스템 설정에 따른 자동 테마 전환
- 🔍 **검색 및 필터링**: 스낵 검색 및 카테고리별 필터링 기능

### 🛠️ 기술 스택
- **언어**: Kotlin
- **UI 프레임워크**: Jetpack Compose
- **아키텍처**: MVVM (Model-View-ViewModel)
- **의존성 주입**: Hilt
- **네비게이션**: Navigation Compose
- **이미지 로딩**: Coil
- **애니메이션**: Compose Animation
- **위젯**: Android App Widget

## 📁 프로젝트 구조

```
Jetsnack/
├── app/
│   ├── src/main/java/com/example/jetsnack/
│   │   ├── model/                    # 데이터 모델
│   │   │   ├── Filter.kt            # 필터 모델
│   │   │   ├── Snack.kt             # 스낵 데이터 모델
│   │   │   └── SnackCollection.kt   # 스낵 컬렉션 모델
│   │   ├── ui/
│   │   │   ├── components/          # 재사용 가능한 UI 컴포넌트
│   │   │   │   ├── Button.kt        # 커스텀 버튼
│   │   │   │   ├── Card.kt          # 커스텀 카드
│   │   │   │   ├── Grid.kt          # 커스텀 그리드 레이아웃
│   │   │   │   └── Snacks.kt        # 스낵 리스트 컴포넌트
│   │   │   ├── home/                # 홈 화면 관련
│   │   │   │   ├── Home.kt          # 메인 홈 화면
│   │   │   │   ├── Feed.kt          # 피드 화면
│   │   │   │   └── cart/            # 장바구니 관련
│   │   │   ├── theme/               # 디자인 시스템
│   │   │   │   ├── Color.kt         # 색상 정의
│   │   │   │   ├── Shape.kt         # 모양 정의
│   │   │   │   ├── Theme.kt         # 테마 정의
│   │   │   │   └── Type.kt          # 타이포그래피 정의
│   │   │   └── snackdetail/         # 상세 화면
│   │   └── widget/                  # 앱 위젯
│   └── src/main/res/                # 리소스 파일
├── build.gradle.kts                 # 프로젝트 빌드 설정
└── gradle.properties               # Gradle 속성
```

## 🎨 핵심 학습 포인트

### 1. 커스텀 디자인 시스템
```kotlin
// Theme.kt에서 커스텀 색상 팔레트 정의
@Immutable
data class JetsnackColors(
    val brand: Color,
    val brandSecondary: Color,
    val uiBackground: Color,
    val gradient6_1: List<Color>,
    // ... 더 많은 색상 정의
)
```

**학습 내용**:
- 브랜드 아이덴티티에 맞는 색상 시스템 구축
- 다크/라이트 테마 지원
- 그라데이션 색상 정의
- CompositionLocal을 활용한 테마 전역 관리

### 2. 커스텀 레이아웃
```kotlin
// Grid.kt에서 커스텀 그리드 레이아웃 구현
@Composable
fun VerticalGrid(modifier: Modifier = Modifier, columns: Int = 2, content: @Composable () -> Unit) {
    Layout(content = content, modifier = modifier) { measurables, constraints ->
        // 커스텀 레이아웃 로직
    }
}
```

**학습 내용**:
- Compose의 Layout API 활용
- 커스텀 레이아웃 알고리즘 구현
- 측정(Measure)과 배치(Place) 과정 이해
- 반응형 그리드 시스템 구축

### 3. 애니메이션
```kotlin
// Home.kt에서 애니메이션 구현
val animatedColor by animateColorAsState(
    targetValue = if (isSelected) selectedColor else unselectedColor,
    animationSpec = tween(300)
)
```

**학습 내용**:
- Compose Animation API 활용
- 상태 기반 애니메이션 구현
- 전환 애니메이션 (Enter/Exit Transition)
- 사용자 인터랙션에 따른 애니메이션

### 4. 네비게이션
```kotlin
// Navigation Compose를 활용한 화면 전환
navController.navigate("snack_detail/${snack.id}")
```

**학습 내용**:
- Navigation Compose 설정
- 화면 간 데이터 전달
- 딥링크 처리
- 백스택 관리

## 🛠️ 개발 환경 설정

### 필수 요구사항
- **Android Studio**: Arctic Fox (2020.3.1) 이상
- **JDK**: 17 이상
- **Android SDK**: API 21 (Android 5.0) 이상
- **Gradle**: 8.13 이상

### 설치 및 실행 방법

1. **프로젝트 클론**
```bash
git clone https://github.com/junsang-dong/android-2025-compose-samples.git
cd android-2025-compose-samples/Jetsnack
```

2. **Android Studio에서 프로젝트 열기**
   - Android Studio 실행
   - "Open an existing project" 선택
   - Jetsnack 폴더 선택

3. **빌드 및 실행**
```bash
# Gradle 빌드
./gradlew build

# 에뮬레이터에서 실행
./gradlew installDebug
```

### 환경 변수 설정 (macOS)
```bash
# Java 17 경로 설정
export PATH="/opt/homebrew/opt/openjdk@17/bin:$PATH"

# Android SDK 경로 설정
export ANDROID_HOME="/Users/[사용자명]/Library/Android/sdk"
export PATH="$ANDROID_HOME/platform-tools:$PATH"
```

## 📚 학습 가이드

### 입문자 학습 순서

1. **기본 구조 파악** (1-2일)
   - 프로젝트 구조 이해
   - MainActivity.kt 분석
   - 기본 화면 구성 파악

2. **디자인 시스템 학습** (2-3일)
   - `ui/theme/` 폴더 분석
   - 색상, 타이포그래피, 모양 정의 방법
   - 테마 적용 방법

3. **컴포넌트 분석** (3-4일)
   - `ui/components/` 폴더의 재사용 컴포넌트 분석
   - 커스텀 컴포넌트 작성 방법
   - 상태 관리 이해

4. **레이아웃 학습** (2-3일)
   - `Grid.kt`의 커스텀 레이아웃 분석
   - Layout API 활용법
   - 반응형 레이아웃 구현

5. **애니메이션 학습** (2-3일)
   - `Home.kt`의 애니메이션 코드 분석
   - 다양한 애니메이션 API 실습
   - 사용자 인터랙션 애니메이션 구현

6. **네비게이션 학습** (2-3일)
   - 화면 간 이동 로직 분석
   - 데이터 전달 방법
   - 딥링크 처리

### 실습 과제

1. **기본 과제**
   - 새로운 색상 추가하기
   - 커스텀 버튼 스타일 만들기
   - 간단한 애니메이션 추가하기

2. **중급 과제**
   - 새로운 화면 추가하기
   - 커스텀 레이아웃 컴포넌트 만들기
   - 복잡한 애니메이션 구현하기

3. **고급 과제**
   - 새로운 기능 추가하기 (예: 즐겨찾기)
   - 성능 최적화 적용하기
   - 테스트 코드 작성하기

## 🐛 문제 해결

### 자주 발생하는 문제들

1. **Java Runtime 오류**
   ```bash
   # 해결방법: Java 17 설치 및 PATH 설정
   brew install openjdk@17
   export PATH="/opt/homebrew/opt/openjdk@17/bin:$PATH"
   ```

2. **Android SDK 경로 오류**
   ```bash
   # 해결방법: local.properties 파일 생성
   echo "sdk.dir=/Users/[사용자명]/Library/Android/sdk" > local.properties
   ```

3. **빌드 오류**
   ```bash
   # 해결방법: 클린 빌드
   ./gradlew clean
   ./gradlew build
   ```

## 📖 추가 학습 자료

### 공식 문서
- [Jetpack Compose 공식 문서](https://developer.android.com/jetpack/compose)
- [Material Design 3](https://m3.material.io/)
- [Android 개발자 가이드](https://developer.android.com/guide)

### 추천 학습 순서
1. Kotlin 기초 문법
2. Android 개발 기초
3. Jetpack Compose 기초
4. 이 프로젝트 분석 및 실습
5. 고급 Compose 기능 학습

## 🤝 기여하기

이 프로젝트는 학습 목적으로 제작되었습니다. 개선사항이나 버그 리포트는 언제든 환영합니다!

### 기여 방법
1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 라이선스

이 프로젝트는 Apache License 2.0 하에 배포됩니다. 자세한 내용은 [LICENSE](LICENSE) 파일을 참조하세요.

## 🙏 감사의 말

이 프로젝트는 Google의 [Android Compose Samples](https://github.com/android/compose-samples)를 기반으로 하며, 바이브코딩 입문자들의 학습을 위해 한국어로 재구성되었습니다.

---

**바이브코딩과 함께하는 안드로이드 앱 개발 여정을 시작해보세요! 🚀**
