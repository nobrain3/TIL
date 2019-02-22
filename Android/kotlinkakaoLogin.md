
# 코틀린?

현재 자바 기반으로 앱 개발중이다. 안드로이드는 이제 코틀린으로 옮기는 추세라 아직 초반이라 코틀린으로 개발을 진행할까 고민중이다
일단 둘이 병행하면서 개발하는걸로 하자.
코틀린 관련 블로그
https://academy.realm.io/kr/posts/kotlin-1/?

## 카카오 로그인 연동
현재 로그인 화면 구현중 MainActivity의 OnCreate()에서 LoginFragment.java를 호출한다 이 프래그먼트에서 로그인 화면을 그리는데  여기서 카카오톡과 네이버 API를 이용해 로그인 연동을 개발중이다.
현재 카카오 디벨로퍼 사이트의 샘플 문서를 올려서 실행하고 있다.
샘플키에 hash 등록완료 keytool을 이용해서 debut.keystore의 hash를 샘플코드 hash에 등록했는데 계속 안됐다. 
원인은 http://blog.devez.net/352 블로그에서 찾았다.  openssl 버전에 따라 해시키값이 다르게 생성되는 문제여서 코드내에서 PackageManager을 이용하여 추출하니 잘됐다.


카카오 디벨로퍼
https://developers.kakao.com/docs/android/getting-started#%ED%82%A4%ED%95%B4%EC%8B%9C-%EB%93%B1%EB%A1%9D
