# tiktok_flutter

flutter create tiktok_flutter

# 1. PROJECT SETUP

## Initialization

- primary color 을 틱톡 색상으로 변경 0xFFE9435A
- 상수 관리하는 폴더 구조 constants 추가 

## Constants

- tailwindcss 의 size 를 sizes.dart 에 정리해 두고 사용한다.
- 디자인시스템이 없는경우 이런식으로 미리 정의해둔 값들로 UI 를 만들면 일관성 있게 작업할수 있다.
- size 를 사용하여 SizedBox 를 만들어서 사이 간격을 일관성 있게 작업하기 위해 gaps.dart 를 정의했다.
- constants 폴더에 있는 class 들은 utility class 이다.

<br><br>

# 2. AUTHENTICATION

## Sign Up Screen

- Scaffold 없이 Text 위젯을 사용하면 밑줄이 생기는걸 볼수 있는데, Scaffold 내부에 있고 없고가 중요하고 항상 필요하다고 보면 된다.
- Scaffold 의 body 에 SafeAria 위젯을 사용하면 모바일 기기의 홀 부분을 피할수 있다. (RN 의 safearea 와 같은 기능)
- 스크린 하단에 고정되어있어야 하는 UI 는 Scaffold 의 bottomNavigationBar 를 사용하면 된다.

## Login Screen

- push 로 화면 전환을 할경우 뒤로가기가 가능하다. 스택 형태로 계속 쌓이게 되므로 필요치 않은부분은 push 를 쓰면 안된다.
- pop 으로 화면 전환을 하면 유저가 보고있는 스택의 최상단 부분이 제거된다.
- 폴더 구조를 기능단위로 가져가고, 해당 기능에서 사용되는 스크린을 모으고, 해당 기능에서 사용되는 공통의 위젯들을 관리하는 폴더를 만들어서 사용한다.
- 클래스에 속성을 추가하고 생성자에 추가한 속성을 편하게 넣으려면 생성자에서 Code Action 을 실행하면 된다.
- FractionallySizedBox 는 부모의 크기에 영향을 받는 위젯이다. widthFactor 인자로 설정할수 있다.

## AuthButton

- flutter pub add font_awesome_flutter
- Expanded 위젯은 Row 나 Column 안에서 점유할수 있는 최대를 점유한다.
- Stack 위젯은 자식 위젯들을 위로 쌓아주는 위젯이다.
- Stack 에 있는 위젯 하나의 정렬만 바꾸려면 Align 위젯을 사용하면 된다.

## Sign Up Form

- main.dart 에서 theme 의 scaffoldBackgroundColor 를 설정하면 전체 scaffold 의 디폴트 색상을 설정핧수 있다.
- main.dart 에서 theme 의 appBarTheme 를 설정하면 전체 AppBar 의 디폴트 스타일 설정을 할수 있다.
- main.dart 에서의 전역설정 외에 다른 설정은 해당 스크린에서 추가하면 된다. (당연히 덮어씌워짐)

## Username Screen

- input form 을 관리하는 위젯에서는 StatefuleWidget 을 사용한다.
- TextEditingController 를 선언하고 TextField 위젯의 controller 속성을 사용하여 state 를 관리할수 있다.
- initState() 메서드에서 컨트롤러에 대한 event listiner 를 추가할수 있다.
- 추가한 addListener 에서 setState 를 통해 컨트롤러에서 관리하고 있는 text state 를 변수에 할당해준다.
- 변수의 값에 따라 버튼 색을 바꿔준다.
- AnimatedContainer 를 사용해서 duration 속성을 설정하면 transition 효과를 줄수 있다.

## FormButton

- AnimatedDefaultTextStyle 위젯을 사용하여 텍스트 관련 애니메이션을 추가할수 있다.
- Controller 는 dispose() 에서 항상 없애는걸 신경써야한다. 수동으로 조작해야 하는 부분이고 그렇지 않을경우 crash 가 발생한다.
- initState() 에서 super.initState() 가 가장 먼저 호출되는것처럼, dispose() 에서도 super.dispose() 가 가장 마지막에 호출되어야 한다.
- stateful widget 안에서는 context 에 자유롭게 접근할수 있으므로 Navigator.of 를 사용하여 화면 이동을 할때 context 를 인자로 넘기지 않아도 된다.

## Email Screen

- TextField 위젯의 decoration 속성의 errorText 에 정규식 관련 함수를 추가하여 error text 를 출력할수 있다.
- TextField 위젯의 keyboardType 속성을 설정하면 사용자가 입력하기 편한 키보드가 노출된다.
- TextField 위젯의 autocorrect 속성을 설정하면 사용자 키보드에 자동 완료 추천이 사라진다.
- Flutter 에서 제공하는 FocusScope 를 사용하면 TextField 외에 다른 부분을 클릭했을때 focus 를 지울수 있다.

    void _onScaffoldTap() {
        FocusScope.of(context).unfocus();
    }

- TextField 위젯의 onEditingComplete 속성을 설정하면 키보드의 Done 을 눌렀을때 일어날 이벤트를 설정할수 있다.

## Password Screen

- TextField 의 decoration 속성에 suffix, prefix, suffixIcon, prefixIcon 을 사용하여 필요한 위젯이나 아이콘을 추가할수 있다.
- suffix 의 mainAxisSize 를 max 로 하면 모든 영역을 점유 하고, min 으로 하면 최소 영역만 점유 한다.
- TextField 의 obscureText 속성을 true 로 설정하면 비밀번호 입력으로 바뀐다.

## Birthday Screen

- bottomNavigationBar 에 CupertinoDatePicker 위젯을 사용하여 생년월일을 입력을 관리한다.
- 생일 정보 Controller 를 initState 에서 오늘 날짜로 바꿔주고, onDateTimeChanged 속성에도 같은 함수를 전달하여 날짜가 바뀔때마다 생일 정보 Controller 를 갱신시킨다.
- CupertinoDatePicker 위젯의 maximumDate, initialDate, mode 등을 설정하여 필요에 맞게 커스텀 할수 있다.

## Login Form

- Form 위젯과 TextFormField 위젯을 사용하여 여러개의 Form 유효성 관리를 할수 있다.
- Controller 로 state 를 관리할때 처럼 Form 의 글로벌키가 필요하다

    ```
    final GlobalKey<FormState> _formKey = GlobalKey<FormState>();
    ```

- Form 위젯에 key 속성에 할당켜준다.

    ```
    Form(
        key: _formKey
    )
    ```

- _formKey.currentState 에 다양한 메서드로 유효성 검사 및 값 저장을 편리하게 할수 있다.

    ```
    void _onSubmitTap() {
        if (_formKey.currentState != null) {
            if (_formKey.currentState!.validate()) {
                _formKey.currentState!.save();
            }
        }
    }
    ```

## Conclusions

- 여러개의 입력을 관리하는게 아니라면 TextField 를 사용하는게 좋다.
- 여러개의 입력을 관리할땐 Form 을 사용하는게 좋다.
- 입력과 관련된 화면에서 unfocus 를 잘 사용하면 UX에 도움을 준다.
- TextFormField 에 autovalidateMode: AutovalidateMode.always 설정을 추가하면 submit 을 누르기 전에도 계속 유효성 체크를 한다.

<br><br>

# 3. ONBOARDING

## Introduction

- 앱이 구동됬을때 앱에 대한 소개나 필요한 사전정보 등을 담을수 있는 부분에 대해서 개발할 예정입니다.

## Interests Screen

- 구현해야할 화면의 depth 가 깊다면 main.dart 에서 home 속성에 개발하려는 스크린을 바로 추가하면 편하다.
- Wrap 위젯을 사용하면 flex wrap 과 같은 기능을 사용할수 있다.
- Wrap 위젯의 spacing, runSpacing 속성을 사용하여 간격을 조절할수 있다.

## Scroll Animations

- scroll 이벤트를 사용하려면 ScrollController 를 사용한다.

    ```
    final ScrollController _scrollController = ScrollController();
    ```

- scroll 이벤트를 사용할 Scaffold 의 body 부분을 Scrollbar 위젯으로 감싸주고, controller 속성에 전달한다.

    ```
    Scrollbar(
        controller: _scrollController
        ...
    )
    ```

- initState() 에서 해당 컨트롤러에 이벤트 리스너를 추가해준다.

    ```
    void initState() {
        super.initState();
        _scrollController.addListener(_onScroll);
    }
    ```

- 스크롤 컨트롤러에서 offset 을 확인하면 현재 스크롤의 위치를 알수 있고, 이 위치를 기반으로 이벤트를 추가한다.

    ```
    void _onScroll() {
        if (_scrollController.offset > 110) {
        if (_showTitle) return;
        _showTitle = true;
        } else {
        _showTitle = false;
        }
        setState(() {});
    }
    ```

- AnimatedContainer 를 사용하여 transition 효과를 줄수 있다.
- 컨트롤러를 사용할땐 항상 dispose() 를 사용해서 컨트롤러 연결을 종료해주도록 한다.

## Tutorial Screen

- DefaultTabController 위젯을 사용하여 3페이지의 튜토리얼 스크린을 만들었다.
- DefaultTabController 위젯과 TabBarView, TabPageSelector 는 같이 사용되어야 한다.
- DefaultTabController 의 length 속성을 설정하여 페이지 수를 정할수 있고, 그 설정에 맞춰 TabBarView 의 children 속성에 위젯을 넣어줘야 한다.
- 이런식으로 할수도 있고 DefaultTabController 대신 TabBarView 에 controller 를 추가하여 개발할수도 있다.
- bottomNavigationBar 에 TabPageSelector 위젯을 추가해서 현재 몇 페이지 인지 확인할수 있는 정보를 편리하게 제공할수 있다.

## AnimatedCrossFade

- AnimatedCrossFade 위젯으로 두가지 화면에 에니메이션 효과를 줄수 있다.
- crossFadeState 속성에서 속성에 따라 보여지는 화면을 ( firstChild, secondChild ) 를 선택할수 있다.
- GestureDetector 의 onPanUpdate, onPanend 로 드래그 관련 이벤트를 만들수 있다.

    ```
    void _onPanUpdate(DragUpdateDetails details) {
        if (details.delta.dx > 0) {
            setState(() {
                _direction = Direction.right;
            });
        } else {
            setState(() {
                _direction = Direction.left;
            });
        }
    }

    void _onPanEnd(DragEndDetails details) {
        if (_direction == Direction.left) {
            setState(() {
                _showingPage = Page.second;
            });
        } else {
            setState(() {
                _showingPage = Page.first;
            });
        }
    }
    ```

<br><br>

# 4. TAB NAVIGATION

## pushAndRemoveUntil

- Navigator 로 화면을 이동할때 스택 히스토리가 남으면 안되는 이동에서는 pushAndRemoveUntill 을 사용하여 뒤로가기를 막을수 있다.
- 두번째 인자의 return 값이 설정 방법이다

    ```
    (route) => true or (route) => false
    ```

## BottomNavigationBar

- Scaffold bottomNavigationBar 에 BottomNavigationBar 위젯을 사용하여 하단 네비게이션을 구현할수 있다.
- BottomNavigationBar 의 currentIndex 속성을 사용해 선택되어있는 탭을 설정할수 있다.
- onTap 속성에 콜백함수를 전달하여 index 를 변경해준다.
- 선택 되어있는 네비게이션에 따라 백그라운드 색을 변경할수도 있고 다양한 설정들이 존재한다.

## NavigationBar

- BottomNavigationBar 는 material design 2 의 사양을 따르고, NavigationBar 는 material design 3 의 사양을 따른다.

## Cupertino TabBar

- CupertinoTabScaffold 는 IOS 디자인과 유사한 레이아웃을 제공한다.

## Custom NavigationBar

- Column 위젯은 기본적으로 세로 공간을 최대한으로 점유하므로 mainAxisSize 속성을 신경써줘야 한다.

    ```
    mainAxisSize: MainAxisSize.min
    ```

- 하단 네비게이션을 클릭할때 유저 편의성을 위해 Container 위젯을 Expanded 로 감싸주면 사용하기 좋다.

## Stateful Navigation part One

- 동일한 위젯을 여러개 사용할때 GlobalKey 를 전달해주면 각각의 인스턴스로 사용할수 있다.
- https://github.com/nomadcoders/tiktok_clone/commit/5819b1a4535d5b23bd2eb77ab41bfe1e86aafcc5

## Stateful Navigation part Two

- Offstage 위젯을 사용하면 사용자에게 보여지지 않을때도 스크린을 숨겨놓을수 있다.
- Body 에 Stack 으로 Offstage 위젯들을 쌓아놓고, 인덱스에 따라 offstage 속성을 설정하면 state 를 유지하는 네비게이션과 스크린을 만들수 있다.
- 너무 많은 Offstage 위젯은 성능저하를 유발할수도 있다.
- https://github.com/nomadcoders/tiktok_clone/commit/fe0dd51ddac68ce7848e1dfddf09b4c0a444acb4

## Post Video Button

- Positioned 위젯은 Stack 내부의 요소들을 이동시킬수 있게 해준다.
- Positioned 위젯은 움직일때 기준이 필요하다. 그래서 3번째 children 으로 Container 를 사용한다. 마지막에 쌓인 Container 를 기준으로 빨간색, 파란색 Positioned 위젯들이 움직인다.
- clipBehavior 속성은 overflow 와 같은 속성이다.

    ```
    clipBehavior: Clip.none
    ```

<br><br>

# 5. VIDEO TIMELINE

## Infinite Scrolling

- PageView 안에 들어가는 Container 들은 PageView 의 크기만큼 점유한다.
- PageView 의 pageSnapping 속성을 사용하면 Container 이동 시 이벤트가 발생한다.
- PageView 또는 ListView 의 builder 메서드를 사용해서 렌더링 성능저하 이슈를 줄일수 있다.
- builder 는 context 와 index 정보를 가지고 렌더링을 수행한다. 몇개의 아이템을 가지고 있는지 명시해줘야 한다.

    ```
    PageView.builder(
        itemCount: 4,
        itemBuilder: (context, index) => Container(
            color: colors[index],
        )
    )
    ```

- onPageChanged 속성에 page 를 인자로 받는 콜백 함수를 추가해서 itemCount 를 갱신 시키는 식으로 무한스크롤을 구현할수 있다.

## PageController

- flutter 에서 무언가를 제어하고 싶을땐 controller 를 사용하면 된다.
- controller 객체 내부에 있는 메서드를 사용하여 에니메이션 효과를 줄수 있다.

    ```
    _pageController.animateToPage(
      page,
      duration: const Duration(milliseconds: 100),
      curve: Curves.linear,
    );
    ```

## Video Player

- flutter pub add video_player
- Positioned.fill 은 화면 전체를 채우는 위젯을을 만들어준다.
- statefull 위젯에서 state 는 widget.~ 으로 widget 에 접근할수 있다.
- VideoPlayer 위젯에 controller 를 전달해서 비디오를 재생할수 있다.
- VideoPlayerController 를 사용할때 항상 initialize 하는 단계를 거처야 한다.

    ```
    @override
    void initState() {
        super.initState();
        _initVideoPlayer();
    }

    void _initVideoPlayer() async {
        await _videoPlayerController.initialize();
        _videoPlayerController.play();
        _videoPlayerController.addListener(_onVideoChange);
        setState(() {});
    }

    void _onVideoChange() {
        if (_videoPlayerController.value.isInitialized) {
            if (_videoPlayerController.value.duration ==
                _videoPlayerController.value.position) {
                widget.onVideoFinished();
            }
        }
    }
    ```

- initialize 를 끝낸 비디오의 길이와 현재 재생되고 있는 비디오의 재생시간이 같으면 비디오가 끝났다는걸 체크하고 전달받은 onVideoFinished 함수를 실행시켜서 다음 페이지로 넘어간다.

## VisibilityDetector

- pubspec.yaml 파일에 dependencies 아래 visibility_detecor: 0.3.3 추가한다.
- 각각의 의존성들은 공식문서를 보면 메서드 내에 전달되는 인자값들이 자세히 나와있으니 사용할때는 항상 공식문서를 참고하는게 좋다.
- Positioned 위젯은 항상 Stack 위젯의 자식으로 존재해야 한다. Positioned 위젯을 다른 위젯으로 감싸주면 안된다.
- IgnorePointer 위젯으로 감싸주는 부분은 포인터가 무시하게 된다.
- VisibilityDetector 위젯을 사용해서 스크린에 전체 화면이 보일때 영상이 재생되도록 할수 있다.

## AnimationController

- animation controller 를 사용할때 class 에 mixin 을 추가해줘야 한다.

    ```
    class _VideoPostState extends State<VideoPost> with SingleTickerProviderStateMixin
    ```

- animation controller 를 만들고 lowerBound (최소값), upperBound(최대값), value(기본값), duration 을 설정해준다.
- _animationController 에 addListener 를 추가해주고 그 곳에서 setState() 를 실행시켜준다.
- animation controller 의 값이 변하는걸 알수 있는 이유는 animation controller 의 reverse(), forward() 메서드를 사용하기 때문이다.

## AnimatedBuilder

- animation 을 빌드하는 다른 방법은 AnimatedBuilder 위젯을 사용하는 것이다.
- controller 만 사용할땐 이벤트를 추가해서 setState() 메서드를 사용해 다시 랜더링을 진행했다.
- AnimatedBuilder 위젯에 animation 에 animation controller 를 추가해주면, builder 속성에서 animation controller 의 변화를 감지하고 return 해준다.
- child 는 animation 을 적용하려는 대상을 의미한다.

    ```
    AnimatedBuilder(
        animation: _animationController,
        builder: (context, child) {
            return Transform.scale(
                scale: _animationController.value,
                child: child,
            );
        },
    )
    ```

## SingleTickerProviderStateMixin

- with 키워드에 Mixin 을 사용하면 그 클래스를 복사해오겠다는 뜻이다. 그 클래스의 모든 메서드와 속성 전부를 가지고 온다.
- vsync 는 위젯이 안보일때 에니메이션을 막아 불필요한 리소스 사용을 줄여주는 것이다. vsync 를 사용하기 위해 SingleTickerProviderStateMixin 를 추가해줘야 한다.
- SingleTickerProviderStateMixin 안에 있는 Ticker 가 부드러운 에니메이션을 가능하게 해준다.
- 즉 에니메이션은 Ticker 가 필수로 필요하고, 화면이 활성되어있는 위젯에만 적용되어야 하니 SingleTickerProviderStateMixin 가 필요하다. 