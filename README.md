# android-interview

안드로이드 개발자 면접 대비.

# Android

[android-interview-questions](https://github.com/amitshekhariitbhu/android-interview-questions) repo를 참고함.

<details>
  <summary>Context에 대해 설명해주세요.</summary>
  
Context는 단어 그대로 맥락을 의미하며, 어플리케이션 혹은 컴포넌트의 현재 상태를 나타냅니다. 
Context를 통하여 어플리케이션 리소스들과 클래스들을 접근할 수 있으며, 엑티비티를 실행하는 작업을 할 수 있습니다.

Activity, Service, Application은 모두 context를 상속하였습니다. 따라서 context를 잘못 사용하는 경우 메모리 누수로 이어질 수 있습니다.

Context중에 Application context와 Activity context가 대표적인데요, Application context는 앱과 관련되어있고 앱이 살아있는 동안 변경되지 않습니다. 따라서 싱글톤 객체에서 context가 필요한 경우 이것을 이용하면 됩니다.

Activity context는 뷰와 관련이 많은 context입니다. 따라서 activity의 생명주기와 연관이 됩니다. GUI 작업을 위한 context는 이것으로만 사용 가능합니다. 만약 싱글톤 객체에서 activity context를 이용한다면 GC에게 수거되지 않아 메모리 누수가 발생합니다.

대부분의 경우 해당 컴포넌트의 context를 이용하면 되고, 앱 전체 수명주기와 연관있거나 싱글톤 객체에서는 application context를 이용하면 됩니다.

</details>

<details>
  <summary>Intent에 대해 설명해주세요.</summary>
  
인텐트는 메시징 객체로, 다른 앱 컴포넌트로부터 작업을 요청하는 데 사용할 수 있습니다. 크게 액티비티 시작, 서비스 시작, 브로드캐스트 전달과 같은 사용 사례가 있습니다.

인텐트는 크게 **명시적 인텐트**와 **암시적 인텐트**로 구분됩니다. 명시적 인텐트는 시작할 컴포넌트의 이름을 명시하는 방법입니다. 예를 들어 명시적 인텐트를 통해 앱에 존재하는 특정 액티비티를 실행할 수 있습니다. 암시적 인텐트는 작업을 지정하여 기기에서 해당 작업을 수행할 수 있는 모든 앱을 호출할 수 있도록 하는 방법입니다. 예를 들어 사용자가 다른 사람에게 콘텐츠를 공유하고자 하는 경우 `ACTION_SEND` 작업이 있는 인텐트를 생성한 다음 공유할 콘텐츠를 지정하는 엑스트라를 추가하는 방법이 있습니다.

암시적 인텐트를 수신하기 위해서는 매니페스트에 앱 컴포넌트에 대해 `<intent-filter>`를 선언하면 됩니다.

인텐트에는 `PendingIntent`가 존재합니다. 이는 앱이 구동되지 않을 때 다른 앱에게 권한을 허가하여 인텐트를 마치 본인 앱에서 실행되는 것처럼 사용하게 하는 것입니다. `PendingIntent`는 대표적으로 Notification, 위젯, AlarmManager를 사용할때 사용됩니다.

</details>

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

<details>
  <summary>클린 아키텍처를 사용해보셨는데 사용하신 이유가 있나요?</summary>

https://jja08111.github.io/android/android-clean-architecture/
https://meetup.nhncloud.com/posts/345

변화에 유연한 프로그램을 개발하기 위해서 사용했습니다. 클린 아키텍처는 구현체가 추상화에 의존하는 구조로 되어있습니다.
따라서 추상화 모듈은 엔터티, 비즈니스 로직을 포함하고 구현체 모듈은 프레임워크, DB들을 포함합니다.
변화가 잦은 구현체에 의존하지 않기 때문에 변화에 유연한 구조입니다.
예를 들어 기존 뷰 시스템에서 컴포즈로 전환을 할 때 비즈니스 로직이 담긴 부분은 그대로 유지한 채 presentation 레이어만 변경을 할 수 있습니다.

또한 테스트 하기 좋은 구조이기 때문입니다. 각 계층을 연결하는 인터페이스들이 존재하기 때문에 Fake 객체를 구현하여 쉽게 테스트를 진행할 수 있습니다.

</details>

<details>
  <summary>의존성 주입에 대해 설명해주세요.</summary>

의존성 주입은 하나의 객체가 다른 객체의 의존성을 제공하는 기법입니다. 의존성 주입의 목적은 객체의 생성과 사용의 관심을 분리하는 것입니다.
이는 가독성과 코드 재사용성을 높여줍니다. 인터페이스를 통해 주입을 받기 때문에 다양한 구현체를 주입 받을 수 있습니다.
또한 테스트에 용이해집니다. 손쉽게 테스트 더블을 생성하여 유닛 테스트가 용이해집니다.

> 의존성이 무엇인가요?

의존성은 한 객체가 매개변수나 리턴 값 혹은 멤버 변수로 다른 객체를 참조하는 것을 의미합니다.

> 왜 의존성 관리가 중요한가요?

객체가 의존하고 있는 다른 객체가 수정되는 경우 해당 객체에 대한 변경이 필요해집니다. 이는 의존성 관리가 제대로 되지 않는 경우 작은 수정이 수많은 변경을 초래할 수 있습니다.
또한 의존성 관리가 제대로 되지 않는 경우 유닛 테스트가 어려워집니다. 때문에 의존성 관리가 중요합니다.

> 그렇다면 안드로이드에서 어떤식으로 의존성을 주입하셨나요?

저는 안드로이드에서 Dagger, Hilt를 이용하여 의존성 주입을 했습니다.

> 왜 라이브러리를 사용하셨나요? 그리고 다른 라이브러리 대신 해당 라이브러리를 이용한 이유가 있나요?

수동으로 컨테이너를 구현하여 의존성을 주입하게 되면 많은 보일러플레이트 코드가 필요하기 때문입니다. 또한 안드로이드 수명 주기를 모두 고려해야 하는데 이를 잘못하는 경우 미묘한 버그와 메모리 누수가 발생하게 됩니다.
따라서 라이브러리를 사용했습니다.

Dagger, Hilt를 사용한 이유는 컴파일 타임에 의존성이 주입되어 안정성이 높기 때문입니다. Koin의 경우 Service Locator Pattern을 이용하여 런타임에 주입되기 때문에 런타임 오류가 발생할 가능 성이 존재합니다. 또한 구글에서 의존성 주입에 Hilt를 사용하는 것을 권장하기 때문입니다.
따라서 Dagger, Hilt를 사용했습니다.

</details>

<details>
  <summary>Activity의 생명주기를 설명해주세요.</summary>

엑티비티는 created, started, resumed, paused, stopped, destroyed 상태를 가집니다.

엑티비티의 생명주기를 잘못 관리하면 문제가 생길 수 있습니다.
예를 들어 사용자가 앱을 사용하는 도중에 전화가 걸려오거나 다른 앱으로 전환할 때 비정상 종료되는 문제,
사용자가 앱을 활발하게 사용하지 않을 때에도 시스템 리소스를 낭비하는 문제,
사용자가 앱을 나갔다가 나중에 다시 돌아올 때 이전 상태가 사라지는 문제,
화면을 회전했을 때 비정상 종료되거나 상태가 사라지는 문제가 있습니다.

먼저 시스템은 엑티비티를 생성할 때 `onCreate()` 콜백함수를 실행합니다. 이는 반드시 구현되어야 합니다.
이때 엑티비티의 전체 수명 주기 동안 한 번만 실행해야 하는 기본 앱 시작 로직을 실행합니다. 예를 들어 바인딩을 하거나 ViewModel과 연결하는 등 클래스 멤버 변수를 인스턴스화 할 수 있습니다.

그 후 엑티비티가 started 상태가 되면 시스템은 곧바로 `onStart()`를 호출합니다. 이때 엑티비티는 사용자에게 보여지고, 앱은 엑티비티를 포그라운드에 보내 사용자와 상호작용 할 수 있도록 준비합니다. 이 메소드에서 앱이 UI를 관리하는 코드를 초기화합니다.

그리고 엑티비티가 resumed 상태가 되면 `onResume()` 메소드가 실행됩니다. 이때 엑티비티는 포그라운드에 표시됩니다. 이 상태에 진입했을 때 앱이 사용자와 상호작용합니다. 어떤 이벤트가 발생하여 포커스가 떠날 때까지 엑티비티는 이 상태에 머무릅니다.

그러다 방해되는 이벤트가 발생하면 엑티비티는 paused 상태에 들어가고, 시스템이 `onPause()` 콜백을 호출합니다. 이는 엑티비티가 포그라운드에 있지 않다는 것을 나타냅니다. 예를 들어 일부 이벤트가 앱 실행을 방해하거나, 새로운 다이어로그가 열릴 때 등을 의미합니다. 이 콜백은 아주 잠시 실행되므로 이곳에서 데이터를 저장하거나 네트워크를 호출하는 등의 부하가 큰 종료 작업은 `onStop()`에서 해야합니다.

그 후 엑티비티가 사용자에게 표시되지 않으면 엑티비티는 stopped 상태가 됩니다. 예를 들어 새로 시작된 엑티비티가 화면 전체를 차지하는 경우입니다. 이 메소드에서는 앱이 사용자에게 보이지 않는 동안 필요 없는 리소스를 해제하거나 조정해야 합니다. 앱이 다시 실행되면 `onRestart()`가 호출되며, 만약 메모리가 부족한 경우 시스템에 의해 종료되어 다시 `onCreate()`부터 진행됩니다.

마지막으로 `onDestroy()`입니다. 이 메소드는 엑티비티가 소멸되기 전에 호출됩니다. 예를 들어 사용자가 엑티비티를 닫거나, `finish()` 함수를 호출하여 엑티비티가 종료되거나, 구성 변경으로 인해 시스템이 일시적으로 엑티비티를 소멸시키는 경우입니다.

</details>

<details>
  <summary>Fragment의 생명주기를 설명해주세요.</summary>

https://jja08111.github.io/android/fragment-lifecycle/

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

<details>
  <summary>Java의 static과 Kotlin의 object 차이를 설명해주세요.</summary>

Java의 static 키워드로 정적 메소드 혹은 정적 변수를 만들 수 있습니다. 이들은 `final` 상수를 제외하고 클래스가 로딩되는 시점에 메모리에 적재됩니다. 때문에 프로그램 종료시까지 메모리에 할당된 채로 존재하게 됩니다.

이와 다르게 Kotlin의 object는 클래스를 싱글톤 형태로 만듭니다. 이는 실제 사용될 때 초기화가 되어 메모리에 적재되며 Java의 static과 다릅니다. 단, `const val`로 선언한 상수, `@JVMStatic` 혹은 `@JVMField`의 어노테이션이 붙은 변수 및 함수들은 Java의 static과 같은 모습을 갖습니다.

> 그렇다면 object와 companion object의 차이점은 무엇인가요?

companion object는 클래스 내부에 존재하는 싱글톤 객체입니다. Java로 변환된 코드를 보면 해당 객체 내부에 Companion이라는 정적 클래스로 되어있는 것을 확인할 수 있습니다.

https://steady-coding.tistory.com/593  
https://velog.io/@skyepodium/클래스는-언제-로딩되고-초기화되는가  
https://nuritech.tistory.com/18

</details>

<details>
  <summary>Coroutine에 대해 설명해주세요.</summary>

https://jja08111.github.io/kotlin/kotlin-coroutine/

</details>

<details>
  <summary>GC에 대해 설명해주세요.</summary>

GC는 garbage collection의 약자로 메모리 기법 중의 하나입니다. GC는 동적 할당된 메모리 영역 중 더이상 어떤 변수도 가르키지 않게 된 영역을 탐지하여 자동으로 해제하는 기법입니다.

GC의 장점은 다음과 같습니다. 먼저 이미 해제된 변수에 접근하는 "유효하지 않은 포인터 접근 문제"가 없습니다. 그리고 이미 해제된 메모리를 다시 해제하려는 이중해제 문제가 없습니다. 더이상 필요하지 않은 메모리가 해제되지 않고 남아있는 메모리 누수 문제가 없습니다.
단점으로는 어떤 메모리를 해제할지 결정하는 데 비용이 듭니다. 또한 GC가 동작하는 타이밍이나 점유 시간을 예측하기 어렵습니다. 따라서 실시간 시스템에는 적합하지 않습니다. 그리고 할당된 메모리가 언제 해제되는지 정확히 알 수 없습니다.

> GC 알고리즘은 어떻게 될까요?

대표적인 첫 번째 GC 알고리즘은 Reference counting입니다. 객체마다 참조되고 있는 횟수를 카운트하여 만약 더이상 참조되지 않는 경우 해당 부분을 해제할 수 있도록 하는 방식입니다. 하지만 이는 한계점이 존재합니다. 만약 순환 참조가 존재한다면 여기에 속한 모든 객체들은 해제될 수 없기 때문입니다.

이 순환 참조 문제를 해결한 알고리즘은 Mark and Sweep입니다. 이 알고리즘은 루트 영역과 힙 영역이 존재합니다. 루트에서 해당 객체를 접근할 수 있는지 판단하여 접근할 수 없다면 해제 가능하다고 판단합니다. 루트부터 그래프 순회를 진행하여 연결된 부분을 reachable, 연결되지 않은 부분을 unreachable으로 나눕니다. Java와 Javascript가 이 방식을 사용합니다.
이 방식에는 단점이 존재하는데요, 의도적으로 GC를 실행시켜 그래프를 순회해야합니다. 따라서 특정 시점에 GC에게 컴퓨터 리소스를 내줘야합니다.

> JVM에서 GC가 어떻게 운영될까요?

Stack, native method stack, method area 영역이 루트 스페이스가 되어 Mark and Sweep으로 동작합니다.

GC를 실행하는 시점은 힙 영역을 보면 알 수 있습니다. 힙 메모리 영역은 eden, survival1, survival2, old generation으로 구분됩니다. eden영역부터 차오르며 이곳이 가득차면 minor GC가 동작합니다. 여기서 살아남은 객체는 age-bit를 1 증가시키고 survival1으로 이동합니다. survival1이 나중에 가득차면 또 minor GC가 동작하고 survival2로 이동합니다. 계속 왔다갔다 이동하다가 age-bit가 15를 넘어서면 old 영역으로 이동합니다. 추후에 old 영역이 가득차면 major GC가 동작합니다. 이 major GC는 수행하는데 오래걸립니다. 이렇게 구현한 이유는 대부분 객체의 수명이 짧았기 때문입니다.

GC를 실행하기 위해 JVM이 멈추는 시점을 Stop the World 시간이라고 합니다. 이 시간을 단축하는것이 중요합니다. GC 방법 중에 Serial GC는 싱글스레드를 이용하여 수행하는데 속도가 느립니다. 이와 다르게 Parallel GC는 여러 쓰레드로 GC를 수행하여 수행 시간이 짧습니다. 마지막으로 G1 GC는 garbage first의 약자로 힙 영역을 잘게 나누어 어느 영역은 young generation, 어느 영역은 old generation으로 활용합니다. 런타임에 G1 GC가 필요에따라 영역 갯수를 튜닝하여 GC 실행시간을 최소화 할 수 있습니다.

</details>

# Computer Architecture

<details>
  <summary>CPU의 작동원리를 설명해주세요.</summary>

https://jja08111.github.io/computer_architecture/what-does-cpu-do/

</details>

# Operating System

<details>
  <summary>프로세스와 스레드의 차이점을 설명해주세요.</summary>

https://jja08111.github.io/os/proccess-vs-thread/

프로세스는 프로그램이 메모리에 적재되어 실행되는 것을 의미하고, 스레드는 프로세스 내에 존재하는 실행 단위입니다. 스레드는 프로세스에 속한 자원을 공유하며, 프로세스는 다른 프로세스와 메모리를 공유하지 않습니다.
프로세스는 스레드들의 컨테이너이며 스레드들에게 공유 공간을 제공합니다.

</details>

<details>
  <summary>CPU 스케줄링에 대해 설명해주세요.</summary>

</details>

<details>
  <summary>데드락에 대해 설명해주세요.</summary>

데드락은 자원을 소유한 스레드들 사이에서 각 스레드가 다른 스레드가 소유한 자원을 요청하여 모든 스레드가 무한정 대기하는 현상을 말합니다.
데드락은 4가지 필요충분조건을 가집니다.

첫 번째 상호배제입니다. 자원은 둘 이상의 스레드들에게 동시에 사용할 수 없어야 합니다.
두 번째 소유하면서 대기입니다. 스레드가 자원을 소유하면서 다른 자원을 대기해야 합니다.
세 번째 선점 불가 입니다. 스레드에게 할당된 자원을 강제로 빼앗지 못합니다.
네 번째 환형 대기입니다. 한 그룹의 스레드들에서 각 스레드가 다른 스레드가 소유한 자원을 요청하는 사이클이 형성 되어야 합니다.

이 조건 중 하나라도 성립하지 않으면 데드락은 발생하지 않습니다.

> 꼬리 질문: 그렇다면 데드락을 어떻게 해결할까요?

데드락을 해결하는 방법에는 예방, 회피, 감지 및 복구, 무시 방법이 있습니다.

결론을 먼저 말하자면 무시 방법을 사용합니다. 발생할 가능성이 낮은 데드락을 위해 수많은 비용을 들이기보다 무시하는 전략이 효율적이기 때문입니다. 단, 핵관련 시스템과 같이 실시간 시스템에는 무시하는 전략은 적절하지 않습니다.

예방 방법은 앞서 말씀드린 필요충분조건 중 하나를 발생하지 않도록 예방하는 것 입니다.
상호배제를 없앤다는 것은 하나의 자원을 둘 이상의 스레드가 동시에 사용한다는 것이기 때문에 이는 말이 안되는 방식입니다.
그리고 소유하면서 대기하지 않도록 하는 방법은 한 번에 모든 자원을 요청하여 대기하지 않도록 하여야 하는데 이는 너무 비효율 적입니다.
또한 자원 선점을 허용하는 것은 자원을 빼앗긴 스레드의 상태를 복구할 수 있도록 관리해야 하며, 어느 스레드의 자원을 빼앗을지 결정하는 알고리즘이 필요하여 단순하지 않은 방법입니다.
마지막으로 환형대기를 없애는 방법의 경우 모든 자원에 번호를 매겨 자원 번호가 낮은 순으로 할당을 하면 가능합니다만, 이는 모든 자원에 번호를 매기는 것이 현실적으로 어렵기 때문이 이 방법 또한 쉽지 않습니다.

다른 방법인 교착상태 회피를 말씀드리겠습니다. 자원 할당을 요청 받았을 때, 앞으로 환형 대기가 발생하지 않는다는 확신이 있을 때만 자원을 할당함으로써 교착상태의 발생을 피하는 방법입니다. 대표적인 알고리즘으로 banker`s 알고리즘이 있습니다.

또 다른 방법인 교착상태 감지 및 복구에 대해 말씀드리겠습니다. 이 방법은 교착상태를 감지하는 백그라운드 프로그램을 상시적으로 실행시켜 교착상태를 감지하고 해제하는 방법입니다. 해제하는 방법에는 자원 강제 선점, 롤백, 스레드 강제종료와 같은 방법들이 있습니다.
이 방법은 계속해서 백그라운드 프로그램을 실행시켜야 하기 때문에 시스템에 적지 않은 부담을 주고 교창상태를 해제하는 방법들도 시스템에 많이 부담스럽습니다.

</details>

<details>
  <summary>페이징 메모리 기법에 대해 설명해주세요.</summary>

페이징 메모리 기법은 물리 메모리와 논리 메모리를 페이지 단위로 나누어 관리하는 기법입니다. 페이지 테이블을 두어 프레임을 참조하는 방식을 사용합니다.
페이징은 하나의 프로세스 공간을 분산하여 할당합니다. 페이징은 고정 크기 메모리 기법을 이용하기 때문에 외부 단편화는 존재하지 않고 내부 단편화가 작게 존재합니다.

> 외부 단편화와 내부 단편화가 무엇인가요?

먼저 단편화는 해당 메모리 영역이 너무 작아 프로세스에게 할당할 수 없는 현상을 뜻합니다. 외부 단편화는 가변 크기 파티션에서 발생하는 단편화입니다.
하나의 프로세스가 분할하지 않고 연속적으로 메모리를 할당한 후 프로세스가 종료되어 홀이 발생하는 데, 이때 외부 단편화가 발생할 수 있습니다.
내부 단편화는 고정 크기 파티션에 발생합니다. 고정된 영역을 전부 사용하지 못할 때 내부 단편화가 발생합니다.

> 세그먼트 기법과 페이징을 비교해주세요.

세그먼트 메모리 기법은 프로세스를 논리 세그먼트들로 나누고 각 논리 세그먼트에 한 덩어리의 물리 메모리를 할당하는 기법입니다.
주로 코드, 데이터, 스택, 힙 세그먼트로 나누어 할당합니다. 세그먼트의 크기는 고정되어 있지 않기 때문에 외부 단편화가 발생할 수 있습니다.
따라서 홀 선택 알고리즘이 필요하며 이로인해 오버헤드가 발생할 수 있습니다.

페이징 메모리 기법은 페이지로 불리는 고정된 영역을 할당하기 때문에 내부 단편화만 존재합니다. 하지만 페이지 크기는 보통 4KB로 작기 때문에 무시할만한 수준입니다.
세그먼트 기법과 다르게 홀 선택 알고리즘을 사용하지 않아도 되기 때문에 메모리 활용과 시간 오버헤드 면에서 우수합니다.

> 페이징 기법은 물리 메모리를 두 번 참조하기 때문에 성능적으로 불리한데요. 이를 어떻게 해결할 수 있을까요?

TLB를 이용하여 해결할 수 있습니다. TLB는 translation look-aside buffer의 약자로 최근에 참조한 프레임의 주소를 O(1)만에 접근할 수 있는 캐시 메모리입니다.
TLB miss가 발생하면 가장 오래된 항목을 제거하거나 LRU 방식을 이용하여 miss된 항목을 넣습니다.

TLB가 성능 향상을 주는 이유는 참조의 지역성 때문입니다. 대부분의 프로그램은 순차 메모리 액세스 패턴을 가지기 때문에 짧은 시간동안 일정 구간의 메모리 영역을 반복 액세스합니다.
따라서 TLB 히트가 계속 발생하여 성능 향상을 얻게 됩니다.

> 단순히 페이징 테이블을 프로세스마다 두어 관리하면 프로세스는 페이지 테이블의 모든 항목을 이용하지 않기 때문에 메모리 낭비가 발생할 수 있습니다. 이를 어떻게 해결할까요?

해결하는 방법으로 역 페이지 테이블, 멀티 레벨 페이지 테이블이 존재합니다.

역 페이지 테이블은 모든 프로세스가 공유하는 하나의 페이지 테이블을 두어 관리하는 기법입니다. 따라서 페이지 테이블에는 프로세스 번호가 추가적으로 필요합니다.

다른 방법으로는 멀티 레벨 페이지 테이블입니다. 멀티 레벨 페이지 테이블은 페이지 디렉터리와 같은 중간 단계의 페이지 테이블을 두어 여러 테이블을 거쳐 물리메모리에 접근하는 방식입니다.
이 기법은 프로세스가 필요한 페이지 테이블만 생성하기 때문에 메모리 낭비가 매우 적습니다.

</details>

<details>
  <summary>가상 메모리 기법에 대해 설명해주세요.</summary>

가상 메모리 기법은 물리 메모리 용량 한계를 극복하기 위한 방법입니다. 물리 메모리의 용량보다 큰 프로세스 혹은 작지만 여러 프로세스를 합쳤을때 물리 메모리 용량을 초과해도 동시에 실행할 수 있는 메모리 관리 기법입니다.

가상 메모리 핵심은 물리 메모리 영역을 디스크 공간으로 확장하는 것과 스와핑입니다. 가상 메모리는 프로세스의 전체를 물리 메모리에 적재하지 않고 일부만 메모리에 적재합니다.
따라서 필요한 경우만 적재를 해야 하는데 이것을 요구 페이징이라 부릅니다. 요구 페이징을 구현하기 위해서는 페이지 테이블에 valid비트, modified비트, 물리 주소 필드가 필요합니다. 
프로세스가 가상 주소를 발생시켰을때 해당 페이지가 물리 메모리에 없는 경우를 페이지 폴트라고 합니다. 페이지 폴트가 발생한 경우 희생 프레임을 선택하여 메모리를 할당해야합니다.

페이지 폴트가 빈번하게 발생하여 디스크 입출력이 심각하게 증가하고 CPU 활용율이 대폭 감소하는 현상이 발생하는데 이를 스레싱이라 합니다. 이는 현재 프로세스들을 감당할 수 없을 만큼 메모리가 부족한 경우 발생합니다.

요구 페이징이 효과적인 이유는 프로그램의 참조의 지역성과 작업 집합 때문입니다. 프로그램은 짧은 시간 범위 내에 일정 구간의 메모리 영역을 반복 참조하는 경향이 있습니다. 
시간 지역성과 공간 지역성이 존재합니다. 시간 지역성은 코드나 데이터 자원 등이 아주 짧은 시간 내에 다시 사용되는 특성을 말합니다. 예를 들어 반복문이 있습니다. 
공간 지역성은 지금 참조하는 주소의 주변 번지를 가까운 미래에 다시 참조할 경향이 높은 특성을 말합니다. 예를 들어 배열 순차 탐색이 있습니다.

작업집합이라는 용어가 존재하는데 이는 일정 시간 범위 내에 프로세스가 참조한 페이지들의 집합을 의미합니다. 즉, 작업 집합은 현재 프로세스의 실행에 필요한 페이지들의 집합을 의미합니다.
프로세스는 페이지 폴트가 발생하며 작업 집합을 형성해나갑니다.

페이지 교체를 위해 희생 프레임을 선택해야합니다. 이때 작업 집합이 아닌 페이지를 희생 프레임으로 선택하는 것이 중요합니다. 페이지 교체 알고리즘은 크게 아래와 같습니다.

- OPT
- FIFO
- LRU
- Clock

</details>

# Network

<details>
  <summary>RESTful API에 대해 설명해주세요.</summary>

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

<details>
  <summary>TCP와 UDP를 비교해주세요.</summary>

https://jja08111.github.io/network/tcp-vs-udp/

</details>

<details>
  <summary>브라우저에 google.com을 입력 했을 때 일어나는 일들을 설명해주세요.</summary>

https://jja08111.github.io/network/what-happened-when-type-google-com.md/

</details>

<details>
  <summary>HTTP에 대해 설명해주세요.</summary>

TODO

</details>

# 진행 방식

- 일주일 동안 같은 주제로 진행하는 사람과 각자 공부
  - 3개 주제 공부
- 토요일 3시 비대면 모임
  - 준비한 3개의 질문을 면접하듯이 질문
  - 1개는 지난 번에 공부했던 주제 중 아무거나 선정하여 질문
  - 답변이 부족한 경우 다음 주차에 다시 공부
  - 종료 후 다음 주에 진행할 주제 선정
