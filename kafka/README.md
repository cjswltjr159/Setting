kafka local 세팅 (for M1 Mac, docker-compose)

m1 맥은 arm64 아키텍쳐라서 arm64를 지원하는 bitnami와 provectuslabs 이미지를 사용한다.

bitnami: https://hub.docker.com/r/bitnami/kafka

provectuslabs :  https://hub.docker.com/r/provectuslabs/kafka-ui



docker-compose 파일 다운로드

curl -sSL https://raw.githubusercontent.com/bitnami/containers/main/bitnami/kafka/docker-compose.yml > docker-compose.yml



docker-compose.yml

version: "2"

services:
  kafka:
    image: docker.io/bitnami/kafka
    ports:
      - "9092:9092"
    volumes:
      - "kafka_data:/bitnami"
    environment:
      - ALLOW_PLAINTEXT_LISTENER=yes

######### 추가 #########
  kafka-ui:
    image: provectuslabs/kafka-ui
    ports:
      - "8080:8080"
    environment:
      - KAFKA_CLUSTERS_0_NAME=local_kafka_0
      - KAFKA_CLUSTERS_0_BOOTSTRAPSERVERS=kafka:9092
#######################

volumes:
  kafka_data:
    driver: local



실행

docker-compose up



kafka 구성 테스트

kafka-ui 접속 (http://localhost:8080)

Topic 생성

Consumer 실행 

kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic TEST-TOPIC-1 --from-beginning

Produce Message



KRAFT (kafka 2.8 이상부터 적용)

KRAFT(Apache Kafka Raft)는 메타데이터 관리를 위해 ZooKeeper에 대한 Apache Kafka의 종속성을 제거하기 위해 도입된 프로토콜이다. 이건 메타데이터에 대한 책임을 두 개의 서로 다른 시스템인 ZooKeeper와 Kafka로 나누는 대신 Kafka 자체로 통합함으로써 Kafka의 아키텍처를 크게 단순화한다.

KRaft는 early access로 개발 중에만 사용해야 한다.

https://developer.confluent.io/learn/kraft/
