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

# Kotlin

# Computer Architecture

# Operating System

<details>
  <summary>프로세스와 스레드의 차이점을 설명해주세요.</summary>

TODO

</details>

# Network

<details>
  <summary>REST에 대해 설명해주세요.</summary>

https://dev-coco.tistory.com/97

먼저 REST에 대해 설명드리겠습니다. REST는 Representational State Transfer의 약자로, 자원을 이름으로 구분해 해당 자원의 상태를 주고 받는 모든 것을 의미합니다.
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
  - 3개 중 2개를 무작위 선택해서 면접하듯이 질문
  - 1개는 지난 번에 공부했던 주제 중 아무거나 선정하여 질문
  - 답변이 부족한 경우 다음 주차에 다시 공부
  - 종료 후 다음 주에 진행할 주제 선정
