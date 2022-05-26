vagrant plugin uninstall vagrant-winnfsd - удалил плагин. Сам её не ставил. Исчезла ошибка
sh: netsh: command not found
sh: cscript: command not found
It seems that you don't have the privileges to change
the firewall rules. NFS will not work without that
firewall changes.

Удалил последнюю версию плагина и поставил более старую
vagrant plugin install vagrant-vbguest --plugin-version 0.21

После этого начал работать провижн при первом запуске машины.

По скрипту создается рейд и диски разбиваются на партиции.
После перезагрузки рейд монтируется
