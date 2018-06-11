# image-scanning-signing-demo

The demo runs on Scaleway and uses scw command line

```
SERVER_ID=$(scw  create  --commercial-type=C2L --ip-address=dynamic  centos)
scw start $SERVER_ID
sleep 10
IP=$(scw inspect $SERVER_ID  2> /dev/null | jq -r .[0].public_ip.address )
while [ -z $IP ]; do
    IP=$(scw inspect $SERVER_ID 2> /dev/null | jq -r .[0].public_ip.address )
    echo "Server not start, retring ..."
    sleep 1
done

ansible-playbook -i inventory.ini install.yaml -e server_ip=$IP -e domain=example.com
```

