# android-interview

안드로이드 개발자 면접 대비.

# Android

[android-interview-questions](https://github.com/amitshekhariitbhu/android-interview-questions) repo를 참고함.

<details>
  <summary>4대 컴포넌트에 대해 설명해주세요.</summary>

https://developer.android.com/guide/components/fundamentals#Components

액티비티는 사용자와 상호작용하기 위한 진입점입니다. 액티비티는 사용자 인터페이스를 포함한 화면 하나를 나타냅니다.
예를 들어 이메일 앱이라면 새 이메일 목록을 표시하는 액티비티가 하나 있고, 이메일을 작성하는 액티비티가 또 하나, 그리고 이메일을 읽는 데 쓰는 액티비티가 또 하나 있을 수 있습니다. 여러 액티비티가 함께 작동하여 해당 이메일 앱에서 짜임새 있는 사용자 환경을 구성하는 것은 사실이지만, 각자 서로 독립되어 있습니다. 따라서 이메일 앱에서 허용할 경우 다른 앱이 이런 액티비티 중 하나를 시작할 수 있습니다. 예를 들어 카메라 앱이라면 이메일 앱 안의 액티비티를 시작하여 사용자가 새 이메일을 작성하고 사진을 공유하게 할 수 있습니다.

서비스는 여러 가지 이유로 백그라운드에서 앱을 계속 실행하기 위한 다목적 진입점입니다. 이는 백그라운드에서 실행되는 구성 요소로, 오랫동안 실행되는 작업을 수행하거나 원격 프로세스를 위한 작업을 수행합니다.
서비스는 사용자 인터페이스를 제공하지 않습니다. 예를 들어 서비스는 사용자가 다른 앱에 있는 동안에 백그라운드에서 음악을 재생하거나, 사용자와 액티비티 간의 상호작용을 차단하지 않고 네트워크를 통해 데이터를 가져올 수도 있습니다.

Broadcast Receiver는 시스템이 정기적인 사용자 플로우 밖에서 이벤트를 앱에 전달하도록 지원하는 구성 요소로, 앱이 시스템 전체의 브로드캐스트 알림에 응답할 수 있게 합니다. Broadcast Receiver도 앱으로 들어갈 수 있는 또 다른 명확한 진입점이기 때문에 현재 실행되지 않은 앱에도 시스템이 브로드캐스트를 전달할 수 있습니다. 예를 들어 앱이 사용자에게 예정된 이벤트에 대해 알리는 알림을 게시하기 위한 알람을 예약할 경우, 그 알람을 앱의 Broadcast Receiver에 전달하면 알람이 울릴 때까지 앱을 실행하고 있을 필요가 없습니다. 대다수의 브로드캐스트는 시스템에서 발생합니다. 예컨대 화면이 꺼졌거나 배터리가 부족하거나 사진을 캡처했다고 알리는 브로드캐스트가 대표적입니다. 앱도 브로드캐스트를 시작할 수 있습니다. 예를 들어 다른 앱에 일부 데이터가 기기에 다운로드되었고 이를 사용할 수 있다는 것을 알리는 데 사용합니다. Broadcast Receiver는 사용자 인터페이스를 표시하지 않지만, 상태 표시줄 알림을 생성하여 사용자에게 브로드캐스트 이벤트가 발생했다고 알릴 수 있습니다. 다만 Broadcast Receiver는 그저 다른 구성 요소로의 게이트웨이인 경우가 더 보편적이고, 극소량의 작업만 수행하도록 만들어진 경우가 많습니다. 예컨대 JobService를 예약하여 시작하여 JobScheduler가 포함된 이벤트를 기초로 어떤 작업을 수행하게 할 수 있습니다.

콘텐츠 제공자는 파일 시스템, SQLite 데이터베이스, 웹상이나 앱이 액세스할 수 있는 다른 모든 영구 저장 위치에 저장 가능한 앱 데이터의 공유형 집합을 관리합니다. 다른 앱은 콘텐츠 제공자를 통해 해당 데이터를 쿼리하거나, 콘텐츠 제공자가 허용할 경우에는 수정도 가능합니다. 예를 들어 Android 시스템은 사용자의 연락처 정보를 관리하는 콘텐츠 제공자를 제공합니다. 적절한 권한을 가진 앱이라면 콘텐츠 제공자(예: ContactsContract.Data)를 쿼리하여 특정한 인물에 대한 정보를 읽고 쓸 수 있습니다.

</details>

<details>
  <summary>MVC, MVP, MVVM, MVI에 대해 비교해주세요.</summary>
  
MVC는 Model, View, Controller로 구성됩니다. Controller가 사용자의 입력을 받아 Model에서 정보를 얻어와 View를 갱신합니다. View는 Model에서 정보를 얻어와 자신을 갱신합니다. 
MVC 패턴은 초기 개발속도가 빠르다는 장점이 있습니다. 하지만 앱의 크기가 커지면 Controller가 비대해져 유지보수에 좋지 않습니다. 
또한 View와 Contoller가 강하게 결합되어 Controller를 테스트하기 어렵습니다.

MVP는 앞선 MVC의 문제를 해결한 패턴입니다. MVP는 Model, View, Presenter로 구성됩니다. Presenter는 ViewInterface를 가지고 있으며 View는 ViewInterface를 구현합니다.
때문에 Presenter가 View에 대한 의존성을 띄지 않는 구조입니다. 그렇기 때문에 Presenter를 테스트 하기 좋으며 코드가 적절히 분리되어 관리하기 좋습니다.
하지만 View와 Presenter가 1대1 관계이기 때문에 비슷한 로직을 가진 화면이 이미 존재해도 계속해서 Presenter를 만들어야 하는 단점이 있습니다.

MVVM은 앞선 MVP의 View와 Presenter의 1대1 구조 단점을 개선한 패턴입니다. MVVM은 Model, View, ViewModel로 구성됩니다.
ViewModel은 Presenter와 다르게 observable 깂를 가지고 있습니다. 이 값을 View에서 구독하여 변화를 관찰합니다.
때문에 MVVM 패턴은 ViewModel과 View의 관계는 1:N이 되어 로직을 재활용 할 수 있는 장점이 있습니다.
하지만 좋지 않은 구조로 설계하면 상태 값이 많아졌을 때 상태관리가 어려워 질 수 있습니다. 또한 부수효과 관리가 어렵습니다.

MVI 패턴은 앞선 MVVM의 상태관리와 부수효과 문제를 개선합니다. MVI는 Model, View, Intent로 구성됩니다.
사용자가 Intent를 발생시켜 불변 Model을 다른 값으로 복사하고, 이 복사된 Model은 View에 상태를 제공합니다.
또한 MVI는 SideEffect를 따로 관리합니다. Background 작업, API 통신, I/O 작업들이 주로 포함됩니다.
MVI는 상태가 한 곳에서 관리되기 때문에 상태가 많아져도 충돌이 일어나지 않습니다. 단방향 구조이기 때문에 흐름 관리가 쉽습니다.
Model이 불변 객체이기 때문에 스레드에 안정적입니다. 하지만 다른 패턴에 비해 러닝 커브가 높은 것이 단점입니다.

</details>

# Kotlin

<details>
  <summary>sealed class와 enum class에 대해 비교해주세요.</summary>
  
sealed class에 상속된 sub class들이 무엇이 있는 지 컴파일 타임에 알 수 있는 것이 가장 큰 특징입니다. 
enum class와 다르게 sub class를 인스턴스화 할 수 있으며 동일한 패키지 내에서 상속이 가능합니다. 
enum class는 각 값들이 상수이며 이는 인스턴스화 할 수 없고 상속을 할 수 없다는 것을 의미합니다.

</details>

<details>
  <summary>스코프 함수에 대해 설명해주세요.</summary>
  
kotlin에는 스코프 함수가 존재하며 `let`, `with`, `run`, `apply`, `also`가 있습니다.

`let`은 extension 함수이며 주로 nullable 값을 non-null일 때만 특정 작업을 수행하기 위해 사용됩니다. 그리고 콜 체인의 결과를 가지고 함수를 호출할 때 이용됩니다.

`with`는 extension 함수가 아니며 주로 람다 결과를 반환하지 않고 특정 오브젝트로 함수들을 여러번 실행 할 때 사용됩니다.

`run`은 extension 함수와 일반 함수가 존재합니다. 주로 객체 초기화와 결과 값 연산이 람다 내에서 동시에 이루어 질 때 사용됩니다.
non-extension 함수의 경우 스코프 안에 변수를 두어 특정 연산 값을 반환할 때 유용합니다.

`apply`는 extension 함수이며 주로 객체 생성 후 곧바로 초기값을 설정하는 작업을 수행할 때 사용됩니다.

`also`는 extension 함수이며 주로 객체의 속성이나 메서드에 접근할 때 보다는 객체를 사용하는 작업이 필요할 때 쓰입니다. 또한 외부의 `this` 레퍼런스를 가리지 않고 싶을 때 사용됩니다.

`apply`와 `also`는 객체 자신을 반환하며, `run`, `with`, `let`은 람다의 결과를 반환합니다.

</details>

# Computer Architecture

# Operating System

<details>
  <summary>프로세스와 스레드의 차이점을 설명해주세요.</summary>

https://jja08111.github.io/os/proccess-vs-thread/

프로세스는 프로그램이 메모리에 적재되어 실행되는 것을 의미하고, 스레드는 프로세스 내에 존재하는 실행 단위입니다. 스레드는 프로세스에 속한 자원을 공유하며, 프로세스는 다른 프로세스와 메모리를 공유하지 않습니다.
프로세스는 스레드들의 컨테이너이며 스레드들에게 공유 공간을 제공합니다.

</details>

# Network

<details>
  <summary>REST에 대해 설명해주세요.</summary>

https://dev-coco.tistory.com/97

REST는 Representational State Transfer의 약자로, 자원을 이름으로 구분해 해당 자원의 상태를 주고 받는 모든 것을 의미합니다.
URI는 정보의 자원만 표현해야 하며, 자원의 행위는 HTTP Method에 명시해야 합니다.

**URI vs URL**

https://inpa.tistory.com/entry/WEB-🌐-URL-URI-차이

> URI는 식별하고, URL위치를 가르킵니다.

- URI: 특정 리소스를 식별하는 통합 자원 식별자를 의미합니다.
- URL: 컴퓨터 네트워크 상에서 리소스가 어디 있는지 알려주기 위한 규약입니다. URI에 포함됩니다.

**HTTP**

https://developer.mozilla.org/ko/docs/Web/HTTP/Overview

Hypertext Transfer Protocol의 약자로 인터넷 상에서 데이터를 주고 받기 위한 서버/클라이언트 모델을 따르는 프로토콜입니다.
Application 계층의 프로토콜로 [TCP/IP](https://www.ibm.com/docs/ko/aix/7.1?topic=management-transmission-control-protocolinternet-protocol) 위에서 작동합니다. 클라이언트가 requst를 보내면 서버는 요청을 처리하여 response를 보낸다. Connectionless, Stateless 방식으로 동작합니다.

</details>

# 진행 방식

- 일주일 동안 같은 주제로 진행하는 사람과 각자 공부
  - 3개 주제 공부
- 토요일 3시 비대면 모임
  - 준비한 3개의 질문을 면접하듯이 질문
  - 1개는 지난 번에 공부했던 주제 중 아무거나 선정하여 질문
  - 답변이 부족한 경우 다음 주차에 다시 공부
  - 종료 후 다음 주에 진행할 주제 선정
