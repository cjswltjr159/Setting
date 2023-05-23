## elasticsearch 설치
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-8.7.1-linux-x86_64.tar.gz

wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-8.7.1-linux-x86_64.tar.gz.sha512

shasum -a 512 -c elasticsearch-8.7.1-linux-x86_64.tar.gz.sha512 

tar -xzf elasticsearch-8.7.1-linux-x86_64.tar.gz

cd elasticsearch-8.7.1/ 


## vm setting
sudo vi /etc/sysctl.conf

vm.max_map_count=262144



## elasticsearch.yml
cluster.name: ELK

node.name: node-1

bootstrap.memory_lock: true

cluster.initial_master_nodes: node-1

http.port: 9200
ll

xpack.security.enabled: false


