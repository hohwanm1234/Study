# Proxy pattern
"대리자" 어떤 객체를 사용하고자 할때,
객체를 직접적으로 참조하는 것이 아닌 해당 객체를 대항하는 객체를 통해 대상 객체에 접근하는 방식을 사용하면
해당 객체가 메모리에 존재하지 않아도 기본적인 정보를 참조하거나 설정할 수 있다.

# 기본적인 이미지
![image](https://github.com/hohwanm1234/Study/assets/46438755/d4156d28-c406-459e-879e-dc81cdadeecd)

![image](https://github.com/hohwanm1234/Study/assets/46438755/f078c582-e63e-44c7-9ea0-bf8c368fba63)

![image](https://github.com/hohwanm1234/Study/assets/46438755/30b83f1f-9e82-4539-94a4-a5f8faafb3d1)

![image](https://github.com/hohwanm1234/Study/assets/46438755/7036de42-2cbc-4b68-a446-6ebb21060e9f)

# 프록시 주요 기능
1. 접근제어
- 권한에 따른 접근 차단
- 캐싱 (프로세스 지속 시간을 줄일 수 있음)
- 지연로딩
2. 부가기능 추가
- 서버가 제공하는 기능에 부가기능 추가

# 프록시 패턴의 장단점
1. 프록시패턴 장점
- 사이즈가 큰 객체가 로딩되기 전에도 프록시를 통해 참조할 수 있다.
- 실제 객체의 public 메소드를 숨기고 인터페이스를 통해 노출시킬 수 있다.
- 로컬에 있지 않고 떨어져있는 객체를 사용할 수 있다.
- 원래 객체에 접근에 대해 사전 처리를 할 수 있다.
2. 프록시패턴 단점
- 객체를 생성할 때 한 단계를 거치게 되므로 (첫번째 객체 생성 시 느려짐) 빈번한 객체 생성이 필요한 경우 성능이 저하될 수 있다.
- 프록시 내부에서 객체 생성을 위해 스레드가 생성, 동기화가 구현되어야 하는 경우 성능이 저하될 수 있다.
- 로직이 난해해져 가독성이 떨어질 수 있다.

# Sample
public class ProxyPatternTest {
  void noProxyTest() {
    RealSubject realSubject = new RealSubject();
    ProxyPatternClient client = new ProxyPatternClient(realSubject);
    client.execute(); // 총 3번 실행 (1초 소요)
    client.execute(); // (1초 소요 - 총 3초 소요)
    client.execute();
  }
  
  void cacheProxyTest() {
    RealSubject realSubject = new RealSubject();
    CacheProxy cacheProxy = new CacheProxy(realSubject);
    ProxypatternClient client = new ProxyPatternClient(cacheProxy);
    client.execute(); // 총 3번 실행 (1초)
    client.execute(); // (0.1초 소요 - 총 1.2초 소요)
    client.execute();
  }
}
