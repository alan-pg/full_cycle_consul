mkdir /var/lib/consul
mkdir /etc/consul.d

#server
consul agent -server -bootstrap-expect=3 -node=consulserver02 -bind=172.23.0.2 -data-dir=/var/lib/consul -config-dir=/etc/consul.d

#client
consul agent -bind=172.23.0.5 -data-dir=/var/lib/consul -config-dir=/etc/cons
ul.d
