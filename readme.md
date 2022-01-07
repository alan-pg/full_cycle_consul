mkdir /var/lib/consul
mkdir /etc/consul.d

#server
consul agent -server -bootstrap-expect=3 -node=consulserver01 -bind=172.23.0.1 -data-dir=/var/lib/consul -config-dir=/etc/consul.d

#client
consul agent -bind=172.23.0.5 -data-dir=/var/lib/consul -config-dir=/etc/consul.d

consul agent -bind=172.23.0.5 -data-dir=/var/lib/consul -config-dir=/etc/consul.d --retry-join=172.23.0.1 --retry-join=172.23.0.2

apk -U add bind-tools
dig @localhost -p 8600 SRV
dig @localhost -p 8600 nginx.service.consul

curl localhost:8500/v1/catalog/services

consul catalog nodes -service nginx
consul catalog nodes -detailed

apk add nginx

mkdir /usr/share/nginx/html -p
vim /etc/nginx/conf.d/default.conf
    root /usr/share/nginx/html;
vim /usr/share/nginx/html/index.html

consul agent -config-dir=/etc/consul.d

consul keygen

http://localhost:8500/ui