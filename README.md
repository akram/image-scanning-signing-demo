# image-scanning-signing-demo

The demo runs on Scaleway and uses scw command line

```
SERVER_ID=$(scw  create  --commercial-type=C2L --ip-address=dynamic  centos)
scw start $SERVER_ID
sleep 10
IP=$(scw inspect $SERVER_ID  2> /dev/null | jq -r .[0].public_ip.address )
while [ -z $IP ]; do
    IP=$(scw inspect $SERVER_ID 2> /dev/null | jq -r .[0].public_ip.address )
    echo "Server not started, retrying ..."
    sleep 1
done

sed s/@@IP@@/$IP/g inventory.ini > /tmp/inventory
ansible-playbook -i /tmp/inventory.ini install.yaml -e domain=example.com
```

