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