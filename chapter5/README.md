Bu repo chapter teki Lab-task3'un otomatik cozumunu saglayan playbook'lari barindiriyor (daha ziyade makina performansını test için yaptın).

Çalıştırmak için:

server1# git clone https://github.com/alpaslank-73/gl294.git

server1# cd gl294/chapter5

Egitimde 8 kisi varsa fork'u 8 yapabilirsin (aynı anda bu kadar kişi lab yapıyorken hypervisor üzerinde nasıl bir durum oluşuyor):

server1# ansible-playbook -f8 chapter5_lab-task-3_otomatik_solution.yaml

--------------------------

scaleup.yaml Bonus lab'ı için (Dikkat! server1 degil stationX uzerinde calisacak):

server1# scp scaleup.yaml station10:/home/guru/playbooks

Guru olarak stationX uzerinde:

guru@stationX playbooks $ ansible-playbook -i lb_web_inventory -e scale_num=2 scaleup.yaml

Ancak bu scale konusu tam olarak duzgun calismiyor zira container'larin repo'larinda sorun var. Vakit darligindan bu konuya bakamadin fakat sorun asagidaki gibi (eski container'in reposu duzeltilmis ancak yeni container'inkinde sorun var:)

[guru@station10 playbooks]$ docker exec -it web1 /bin/bash

[root@036aa675a480 /]# cat /etc/yum.repos.d/AppStream.repo
[AppStream]
baseurl=http://vault.centos.org/8.3.2011/AppStream/$basearch/os/
gpgcheck = 0
name = CentOS 8 AppStream Repo

[root@036aa675a480 /]# exit

[guru@station10 playbooks]$ docker exec -it web5 /bin/bash

[root@eb4abd6ae984 /]# cat /etc/yum.repos.d/AppStream.repo
[AppStream]
baseurl = http://10.100.0.254/centos8/AppStream/
gpgcheck = 0
name = CentOS 8 AppStream Repo
