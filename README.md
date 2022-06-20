<br/>

# API Gateway
<br/>

## API Gateway Service
- 인증 및 권한 부여
- 서비스 검색 통합
- 응답 캐싱
- 정책, 회로 차단기 및 QoS 다시 시도
- 속도 제한
- 부하 분산
- 로깅(어떠한 클라이언트가 요청했는지 등), 추적, 상관 관계
- 헤더, 쿼리 문자열 및 청구 변환
- IP 허용 목록에 추가 

사용자가 설정한 라우팅 설정에 따라서 각각의 엔드포인트로 <br/>
클라이언트 대신해서 요청하고 응답을 받으면 다시 클라이언트에게 전달해 주는 프록시 역할을 한다. <br/>
시스템 내부 구조는 숨기고 외부 요청에 대해서 적절한 형태로 가공해서 응답해 줄 수 있다. <br/>
<br/>

## Spring Cloud에서의 MSA간 통신 
#### (1) RestTemplate 
~~~
RestTemplate restTemplate = new RestTemplate();
restTemplate.getForObject("http://localhost:8080/", User.class, 200);
~~~
#### (2) Feign Client 
~~~
@FeignClient("stores") // 외부로 호출하고 싶은 추가적인 마이크로서비스 이름을 등록. 
public interface StoreClient {
    @RequestMapping(method = RequestMethod.GET, value="/stores")
    List<Store> getStores();
    // Store라는 이름을 가진 마이크로서비스의 API를 자신이 가지고 있는 API처럼 호출해서 사용 가능. 
...
~~~
<br/>

## Load Balancer, API Gateway
### Netflix Ribbon (Load Balancer)
초창기 로드밸런서. 비동기 호환이 잘 안되어서 사용x. <br/>
클라이언트 내부에 있는 로드밸런서(Client side Load Balancer). <br/>
클라이언트 내부에서 요청하려는 마이크로서비스의 주소를 직접 관리. <br/>
- (ip:port 정보가 아니라) 서비스 이름으로 서비스를 호출 가능. 
- Health Check

### Netflix Zuul (API Gateway)
이 프로젝트에서는 Netflix Zuul(Routing, API Gateway)을 사용해서 <br/>
First Service, Second Service로 요청을 보내는 것을 구현해 본다. <br/>

### Spring Cloud의 Load Balancer, API Gateway
- Load Balancer: Netflix Ribbon => Spring Cloud Loadbalancer
- API Gateway: Netflix Zuul => Spring Cloud Gateway 
<br/>

<br/><br/><br/><br/>
