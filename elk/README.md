
Elasticsearch is a real-time, distributed storage, search, and analytics engine. 
It can be used for many purposes, but one context where it excels is indexing streams of semi-structured data, such as logs or decoded network packets.

Kibana is an open source analytics and visualization platform designed to work with Elasticsearch. 
You use Kibana to search, view, and interact with data stored in Elasticsearch indices. You can easily perform advanced data analysis and visualize your data in a variety of charts, tables, and maps.

The Beats are open source data shippers that you install as agents on your servers to send operational data to Elasticsearch. 
Beats can send data directly to Elasticsearch or via Logstash, where you can further process and enhance the data.

* Auditbeat - Audit data
* [Filebeat](https://www.elastic.co/guide/en/beats/filebeat/7.6/filebeat-getting-started.html) - Log files
* Functionbeat - Cloud data
* Heartbeat - Availability monitoring
* Journalbeat - Systemd journals
* Metricbeat - Metrics
* Packetbeat - Network traffic
* Winlogbeat - Windows event logs


* https://www.elastic.co/guide/en/elastic-stack-get-started/master/get-started-docker.html
* https://www.elastic.co/guide/en/elastic-stack-get-started/current/get-started-elastic-stack.html

## Get started 
1. `docker-compose up -d`
2. open `http://localhost:5601`

## References
* https://www.elastic.co/guide/en/elasticsearch/reference/7.6/docker.html
* https://www.elastic.co/guide/en/kibana/current/docker.html