### 스프링 배치
- 배치 어플리케이션을 개발하기 위한 Function을 제공하는 프레임워크
- 대용량 처리에 적합
- 통계로 확인 및 저장 가능

### 프로세스 모델
- Tasklet(단일성)
(1) 트랜잭션/속도 문제 떄문에 대용량 처리에 부적함
(2) 단일성 프로세스에만 개발

- Chunk(개발 표준)
(1) Chunk 단위로 개발이 되기 때문에, 트랜잭션 단위가 명확함 (Rollback 범위 확실)
(2) ItemReader / ItemProcessor - 개별 단위
    ItemWriter - 리스트(Array) 단위
    
![image](https://github.com/hohwanm1234/Study/assets/46438755/b4173c33-e545-4ec8-902e-55ff63b30507)

### 개발
![image](https://github.com/hohwanm1234/Study/assets/46438755/49128210-76ec-4af6-9ee7-b07d4b2a592f)

1. 개발 순서
- Job - Step - ItemReader - ItemWriter - ItemProcessor

(1) Job
- 여러 단계의 Step으로 구성
- JobParameters : Job을 식별하거나 Job에서 참조하는 데이터
- Scope Annotaion / 유효성 검사 체크

* 예시 코드
	public Job batchJob() {
	 return jobBuilderFactory.get("batchJob") // JobBuilder를 생성하는 팩토리, Job의 이름을 매개변수로 받음 
	.start(step01()) // 처음 실행 Step
 .next(step02()) // 두번째 실행 Step
 
 (2) Step
 - Step은 Job내부에 구성되어 있으며, 실제 작업을 수행하는 역할
 - 전략 패턴에 맞게 다양한 구현체로 구성

* 예시 코드
	@Bean(JOB_NAME + "Step01")
	public Step step01() {
	    return stepBuilderFactory.get(JOB_NAME + "Step01")
	        .<ZcmwSampleDvo, ZcmwSampleDvo>chunk(chunkSize)
	        .reader(reader())              // ItemReader      (xx에서 데이터를 불러오거나 읽는 역할)
	        .processor(processor())  // ItemProcessor  (주로 데이터 가공 / 필터링)
	        .writer(writer())               // ItemWriter (Array / List) (배치 비즈니스 처리 후 Item을 출력하는 객체)
	        .build();
}

(3) Tasklet
- 배치 Job중 온라인으로 넘기던지 단순한 처리를 할 때 사용
- SQL 업데이트 / Shell / EAI호출 / DB 프로시저 호출 등에 주로 사용



