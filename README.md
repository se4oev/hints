# unix-hints

В этом проекте будут собраны найденные способы взаимодействия с UNIX-системами.

<h3>Kerio control vpnclient</h3>
<h4>Настройка kerio-control-vpnclient</h4>
dpkg-reconfigure kerio-control-vpnclient:
vi /etc/kerio-kvc.conf

<h4>Скрипт для запуска kerio и исправления ошибки связанной с тем, что не прописывается MAC адрес для устройства</h4>
service kerio-kvc start
sleep 2
cat /var/log/kerio-kvc/debug.log | grep MAC | tail -1 | tr - : |rev|cut -d' '  -f 1|rev| xargs -I {} sudo ip link set kvnet addr {}
