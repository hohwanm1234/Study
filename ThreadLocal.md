# ThreadLocal

해당 Thread만 접근 할 수 있는 저장소

* 사용하는 이유
- 동시성 문제 해결을 위해

# 동시성 문제란?
Spring에서 Bean은 싱글톤으로 저장되는데, 하나의 인스턴스 필드에 여러 쓰레드가 동시에 접근하면 동시성 문제가 발생된다.
-> 트래픽이 많을 시 자주 발생
-> 지역변수에는 발생하지 않으나, static등의 공용변수에 접근할 때 발생

# 예시 소스
@Slf4j
public class Test {
	private FieldService fieldService = new FieldService();
    
	@Test
	void field() {
		log.info("main start");
		Runnable userA = () -> {
			fieldService.logic("userA");
		};
		Runnable userB = () -> {
			fieldService.logic("userB");
		};
        
		Thread threadA = new Thread(userA);
		threadA.setName("thread-A");
		Thread threadB = new Thread(userB);
		threadB.setName("thread-B");
		threadA.start(); //A실행
        
		sleep(2000); //동시성 문제 발생X
		// sleep(100); //동시성 문제 발생O
        
		threadB.start(); //B실행
		sleep(3000); //쓰레드B가 끝날 때까지 메인 쓰레드 종료 대기
		log.info("main exit");
	}
	private void sleep(int millis) {
		try {
			Thread.sleep(millis);
		} catch (InterruptedException e) {
			e.printStackTrace();
		}
	}
 } 

-> 해당 결과
[Thread-A] 저장 name=userA -> nameStore=null
[Thread-B] 저장 name=userB -> nameStore=userA
[Thread-A] 조회 nameStore=userB
[Thread-B] 조회 nameStore=userB

-> Thread-A/B에 모두 userB가 저장되는 동시성 문제가 발생함을 확인할 수 있다.


# 기본적인 사용법
- 값 저장 : ThreadLocal.set
- 값 조회 : ThreadLocal.get
- 값 제거 : ThreadLocal.remove
