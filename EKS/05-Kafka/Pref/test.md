


bin/kafka-producer-perf-test.sh --num-records 1000000 --record-size 1000 --topic test-events --throughput 1000000 --producer-props bootstrap.servers=192.168.56.249:31905 max.in.flight.requests.per.connection=1 


bin/kafka-consumer-perf-test.sh --topic test-rep-one --broker-list localhost:2181 --messages 1000000 --threads 1



bin/kafka-console-producer.sh --broker-list acbbfff10a25811ea9b7906027199240-605738047.eu-west-2.elb.amazonaws.com:9094 --topic test-events --producer.config /home/ec2-user/client-ssl.properties



bin/kafka-console-consumer.sh --bootstrap-server acbbfff10a25811ea9b7906027199240-605738047.eu-west-2.elb.amazonaws.com:9094 --topic test-events --consumer.config /home/ec2-user/client-ssl.properties




kubectl get secret kafka-cluster-cluster-ca-cert -n project-cumulus -o jsonpath='{.data.ca\.crt}' | base64 -d > ca.crt

keytool -keystore kafka.client.truststore.jks -import -file ca.crt



bin/kafka-run-class.sh kafka.tools.EndToEndLatency 192.168.56.249:31905 test-events 10000 1 1000 



sudo yum install java-1.8.0-openjdk

tar -xf archive.tar.gz

scp -i /directory/to/abc.pem /your/local/file/to/copy user@ec2-xx-xx-xxx-xxx.compute-1.amazonaws.com:path/to/file

