# docker-elk
ELK를 활용한 Winautomation 모니터링 시스템

선행 조건
Docker, Docker Compose 설치
 * 64bit Linux(권장) https://docs.docker.com/compose/install/
 * Windows10 or Windows Server 2016 https://docs.docker.com/docker-for-windows/install/


이 Github를 다운로드 => 압축 해제 =>  디렉토리로 이동 => 아래 커맨드 실행

docker-compose up -d

아래와 같이 보이면 정상적으로 실행 성공

mltest@mltest:~$ docker container ls
CONTAINER ID  IMAGE                     COMMAND                  CREATED     STATUS        PORTS                                                                NAMES
e092980bd703  dockerelk_logstash        "/usr/local/bin/dock…"   2 days ago  Up 20 hours   5044/tcp, 0.0.0.0:5002->5002/tcp, 9600/tcp, 0.0.0.0:6000->5000/tcp   dockerelk_logstash_1
e3ca24a96b60  dockerelk_nginx           "nginx -g 'daemon of…"   9 days ago  Up 2 days     80/tcp, 0.0.0.0:5600->5600/tcp                                       dockerelk_nginx_1
44ce669c0582  dockerelk_kibana          "/usr/local/bin/kiba…"   13 days ago Up 2 days     0.0.0.0:5601->5601/tcp                                               dockerelk_kibana_1
00d4ead61446  dockerelk_elasticsearch   "/usr/local/bin/dock…"   13 days ago Up 2 days     0.0.0.0:9200->9200/tcp, 0.0.0.0:9300->9300/tcp                       dockerelk_elasticsearch_1


문제시 로그 보기 
docker logs dockerelk_logstash_1
docker logs dockerelk_kibana_1
docker logs dockerelk_elasticsearch_1
docker logs dockerelk_nginx_1

nginx는 로그인용도로 기본 ID/PW는 admin/kbrpa20181!

https://ip:5600 로그인이 필요
http://ip:5601 로그인 불필요 

config 변경 후 개별 서버 재기동 방법(전부 수행할 필요 없음)
docker container restart dockerelk_logstash_1
docker container restart dockerelk_kibana_1
docker container restart dockerelk_elasticsearch_1
docker container restart dockerelk_nginx_1


서버로 로그 전송
http post에 데이터를 json포맷으로 발송(ip:5002)하면 자동 파싱됨

JSON 포맷
{ "Key1": "value1", "Key2": "value2"}
