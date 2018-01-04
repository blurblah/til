*1주일 정도 cortana skill 만들면서 PoC 한 결과*
### Card UI
Cortana skill에서 response로 내려줄 수 있는 항목 중 card가 있음.
Card의 종류는 hero, audio, signin 등 여러가지가 있으나 이 중 audio, signin이 특정 플랫폼에서 제대로 동작하지 않음.

### Signin card
Signin의 경우 로그인이 필요할 때 사용자가 로그인을 할 수 있도록 버튼 형태로 제공됨.
웹에서는 정상 동작하지만 Windows IoT core 에서는 정상동작 하지 않음.
Hero card에 button을 달아서 openurl 하도록 링크를 달아두어도 Windows IoT core에서는 반응이 없음.

### Audio card
Audio card는 streaming을 재생할 수 있도록 제공되는 card ui.
제목, 재생할 stream url, 설명 등을 추가했는데 simulator 에서는 정상 동작.
재생이나 다운로드 버튼 등이 표시되고 음원 설명이나 실행이 정상적으로 동작하지만 아이폰이나 Windows IoT core에서는 제대로 동작하지 않음.
아이폰에서는 card ui가 표시되지 않고 음원이 자동 재생되고 skill 종료시 재생중단됨.
Windows IoT core에서도 기본 동작은 아이폰에서와 동일하지만 cortana 종료시에도 음원이 계속 재생되는 문제가 있음.