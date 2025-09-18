# 🔍 Jetsnack 코드 분석 가이드

> **바이브코딩 입문자를 위한 핵심 코드 분석 및 설명**

## 📁 프로젝트 구조 분석

### 🏗️ 아키텍처 패턴
Jetsnack은 **MVVM (Model-View-ViewModel)** 패턴을 따릅니다:

```
Model (데이터) ← → ViewModel (비즈니스 로직) ← → View (UI)
```

- **Model**: `model/` 폴더의 데이터 클래스들
- **ViewModel**: `ui/home/cart/CartViewModel.kt` 등
- **View**: `ui/` 폴더의 Composable 함수들

## 🎨 핵심 컴포넌트 분석

### 1. 커스텀 디자인 시스템 (`ui/theme/Theme.kt`)

```kotlin
@Immutable
data class JetsnackColors(
    val brand: Color,
    val brandSecondary: Color,
    val uiBackground: Color,
    val gradient6_1: List<Color>,
    // ... 더 많은 색상 정의
)
```

**학습 포인트**:
- `@Immutable` 어노테이션으로 성능 최적화
- `CompositionLocal`을 활용한 전역 테마 관리
- 다크/라이트 테마 지원

### 2. 커스텀 레이아웃 (`ui/components/Grid.kt`)

```kotlin
@Composable
fun VerticalGrid(modifier: Modifier = Modifier, columns: Int = 2, content: @Composable () -> Unit) {
    Layout(content = content, modifier = modifier) { measurables, constraints ->
        val itemWidth = constraints.maxWidth / columns
        val itemConstraints = constraints.copy(
            minWidth = itemWidth,
            maxWidth = itemWidth,
        )
        val placeables = measurables.map { it.measure(itemConstraints) }
        // ... 레이아웃 로직
    }
}
```

**학습 포인트**:
- `Layout` API를 활용한 커스텀 레이아웃 구현
- 측정(Measure)과 배치(Place) 과정 이해
- 반응형 그리드 시스템 구축

### 3. 애니메이션 (`ui/home/Home.kt`)

```kotlin
val animatedColor by animateColorAsState(
    targetValue = if (isSelected) selectedColor else unselectedColor,
    animationSpec = tween(300)
)
```

**학습 포인트**:
- `animateColorAsState`를 활용한 색상 애니메이션
- 상태 기반 애니메이션 구현
- `tween` 애니메이션 스펙 활용

## 🧩 컴포넌트별 상세 분석

### 1. 버튼 컴포넌트 (`ui/components/Button.kt`)

```kotlin
@Composable
fun JetsnackButton(
    onClick: () -> Unit,
    modifier: Modifier = Modifier,
    enabled: Boolean = true,
    text: @Composable () -> Unit
) {
    // 커스텀 버튼 구현
}
```

**특징**:
- 재사용 가능한 컴포넌트 설계
- 다양한 상태(활성화/비활성화) 지원
- 커스텀 스타일링 적용

### 2. 카드 컴포넌트 (`ui/components/Card.kt`)

```kotlin
@Composable
fun JetsnackCard(
    modifier: Modifier = Modifier,
    onClick: (() -> Unit)? = null,
    content: @Composable () -> Unit
) {
    // 커스텀 카드 구현
}
```

**특징**:
- 클릭 가능한 카드 지원
- 일관된 디자인 시스템 적용
- 접근성 고려

### 3. 그리드 컴포넌트 (`ui/components/Grid.kt`)

```kotlin
@Composable
fun VerticalGrid(
    modifier: Modifier = Modifier,
    columns: Int = 2,
    content: @Composable () -> Unit
) {
    // 커스텀 그리드 레이아웃 구현
}
```

**특징**:
- 동적 컬럼 수 지원
- 반응형 레이아웃 구현
- 성능 최적화된 레이아웃

## 🎭 애니메이션 분석

### 1. 색상 애니메이션

```kotlin
val animatedColor by animateColorAsState(
    targetValue = if (isSelected) selectedColor else unselectedColor,
    animationSpec = tween(300)
)
```

**사용 사례**: 버튼 선택 상태 변경 시 색상 전환

### 2. 크기 애니메이션

```kotlin
val animatedSize by animateFloatAsState(
    targetValue = if (isExpanded) 1.2f else 1.0f,
    animationSpec = spring()
)
```

**사용 사례**: 카드 확장/축소 애니메이션

### 3. 전환 애니메이션

```kotlin
AnimatedContent(
    targetState = currentScreen,
    transitionSpec = {
        slideInHorizontally() + fadeIn() togetherWith
        slideOutHorizontally() + fadeOut()
    }
) { screen ->
    // 화면 내용
}
```

**사용 사례**: 화면 간 전환 애니메이션

## 🧭 네비게이션 분석

### 1. 네비게이션 설정 (`ui/navigation/JetsnackNavController.kt`)

```kotlin
@Composable
fun JetsnackNavController(
    navController: NavHostController = rememberNavController()
) {
    NavHost(
        navController = navController,
        startDestination = "home"
    ) {
        composable("home") { Home() }
        composable("snack_detail/{snackId}") { backStackEntry ->
            val snackId = backStackEntry.arguments?.getString("snackId")
            SnackDetail(snackId = snackId)
        }
    }
}
```

**특징**:
- 타입 안전한 네비게이션
- 딥링크 지원
- 백스택 관리

### 2. 화면 전환

```kotlin
navController.navigate("snack_detail/${snack.id}")
```

**특징**:
- 데이터 전달을 위한 URL 파라미터 활용
- 프로그래매틱 네비게이션

## 🛒 비즈니스 로직 분석

### 1. 장바구니 ViewModel (`ui/home/cart/CartViewModel.kt`)

```kotlin
class CartViewModel : ViewModel() {
    private val _cartItems = MutableStateFlow<List<CartItem>>(emptyList())
    val cartItems: StateFlow<List<CartItem>> = _cartItems.asStateFlow()
    
    fun addItem(item: CartItem) {
        // 장바구니에 아이템 추가 로직
    }
    
    fun removeItem(itemId: String) {
        // 장바구니에서 아이템 제거 로직
    }
}
```

**특징**:
- `StateFlow`를 활용한 상태 관리
- 비즈니스 로직과 UI 분리
- 테스트 가능한 구조

### 2. 데이터 모델 (`model/Snack.kt`)

```kotlin
data class Snack(
    val id: String,
    val name: String,
    val price: Long,
    val imageUrl: String,
    val tags: Set<String> = emptySet()
)
```

**특징**:
- 불변 데이터 클래스
- 직렬화 가능한 구조
- 타입 안전성 보장

## 🎯 학습 포인트 요약

### 1. Compose 기초
- **Composable 함수**: UI를 구성하는 기본 단위
- **State 관리**: `remember`, `mutableStateOf` 활용
- **Recomposition**: 상태 변경에 따른 UI 업데이트

### 2. 레이아웃 시스템
- **기본 레이아웃**: `Column`, `Row`, `Box`
- **커스텀 레이아웃**: `Layout` API 활용
- **Modifier**: 레이아웃 조정 및 스타일링

### 3. 애니메이션
- **상태 기반 애니메이션**: `animate*AsState`
- **전환 애니메이션**: `AnimatedContent`
- **제스처 애니메이션**: `AnimatedVisibility`

### 4. 아키텍처
- **MVVM 패턴**: 관심사 분리
- **ViewModel**: 비즈니스 로직 관리
- **StateFlow**: 반응형 상태 관리

## 🚀 다음 단계

### 1. 코드 수정 실습
- 색상 변경해보기
- 애니메이션 속도 조정해보기
- 새로운 컴포넌트 추가해보기

### 2. 기능 확장
- 새로운 화면 추가하기
- 검색 기능 개선하기
- 즐겨찾기 기능 추가하기

### 3. 성능 최적화
- `remember` 활용하기
- `LazyColumn` 최적화하기
- 불필요한 리컴포지션 방지하기

---

**코드를 직접 수정하고 실행해보며 학습해보세요! 🎯**
