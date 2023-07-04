# tiktok_flutter

flutter create tiktok_flutter

## Initialization

- primary color 을 틱톡 색상으로 변경 0xFFE9435A
- 상수 관리하는 폴더 구조 constants 추가 

## Constants

- tailwindcss 의 size 를 sizes.dart 에 정리해 두고 사용한다.
- 디자인시스템이 없는경우 이런식으로 미리 정의해둔 값들로 UI 를 만들면 일관성 있게 작업할수 있다.
- size 를 사용하여 SizedBox 를 만들어서 사이 간격을 일관성 있게 작업하기 위해 gaps.dart 를 정의했다.
- constants 폴더에 있는 class 들은 utility class 이다.

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