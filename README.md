# Ansible playbook (csf)
<br>
#Если есть другой файрвол  - отключаем

systemctl stop firewalld && systemctl disable firewalld

#Устанавливаем:

yum install perl-libwww-perl -y или apt install libwww-perl -y

cd /usr/src
wget -qO- https://download.configserver.com/csf.tgz | tar xvz
cd csf
sh install.sh

#Tестируем:

perl /usr/local/csf/bin/csftest.pl

#Перезепустим и протестируем:

systemctl restart {csf,lfd}
systemctl enable {csf,lfd}
systemctl is-active {csf,lfd}
csf -v
csf -ra #reboot all = перезагрузит csf и lfd

#Сразу добавим процессы в игнорирование которые потребляют много ресурсов иначе они будут дропнуты lfd

csf.pignore
exe:/opt/pgpro/1c-13/bin/postgres
exe:/opt/1cv8/x86_64/8.3.19.1150/ragent
exe:/opt/1cv8/x86_64/8.3.19.1150/rmngr
exe:/opt/1cv8/x86_64/8.3.19.1150/rphost
</br>
