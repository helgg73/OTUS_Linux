# OTUS_Linux

Изменен box на доступный в репозитории из России.

Исправлена ошибка Failed to download metadata for repo 'appstream': Cannot prepare internal mirrorlist: No URLs in mirrorlist:
https://techglimpse.com/failed-metadata-repo-appstream-centos-8/
cd /etc/yum.repos.d/
sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-*
sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-*

Обновлено ядро системы с версии 4.18.0-240.1.1.el8_3.x86_64 до 6.7.9-1.el8.elrepo.x86_64. Использован https://github.com/Nickmob/vagrant_kernel_update

# Установка репозитория elrepo
sudo yum install -y https://www.elrepo.org/elrepo-release-8.el8.elrepo.noarch.rpm 
# Установка нового ядра из репозитория elrepo-kernel
yum --enablerepo elrepo-kernel install kernel-ml -y

# Обновление параметров GRUB
grub2-mkconfig -o /boot/grub2/grub.cfg
grub2-set-default 0
echo "Grub update done."
# Перезагрузка ВМ
shutdown -r now
