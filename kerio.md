### Kerio Vpn Control

### Kerio control vpnclient
#### Настройка kerio-control-vpnclient 
`dpkg-reconfigure kerio-control-vpnclient`  
`vi /etc/kerio-kvc.conf`

#### Скрипт для запуска kerio и исправления ошибки связанной с тем, что не прописывается MAC адрес для устройства 
`service kerio-kvc start`  
`sleep 2`  
`cat /var/log/kerio-kvc/debug.log | grep MAC | tail -1 | tr - : |rev|cut -d' '  -f 1|rev| xargs -I {} sudo ip link set kvnet addr {}`