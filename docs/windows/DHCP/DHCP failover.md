### DHCP failover

---

Отказоустойчивость DHCP подразумевает настройку двух компьютеров Server 2012 и выше со служебной ролью DHCP и установку их в паре. Эта пара способна обеспечить высокую доступность DHCP, благодаря следующим техническим возможностям:

* **Load balance mode** (Режим балансировки нагрузки)

  Режим балансировки нагрузки (в документации он иногда называется режимом распределения нагрузки, load sharing mode) – это способ настройки отказоустойчивости DHCP по умолчанию. Когда вы настраиваете два сервера DHCP в режиме балансировки нагрузки, **каждый сервер будет предоставлять IP-адреса из одной и той же области, и при этом адреса не дублируются**. Балансировка нагрузки позволяет каждому серверу выдавать адреса в аренду из указанного диапазона. **При отказе одного из серверов DHCP другой продолжает предоставлять адреса, пока первый сервер DHCP снова не начнет работать.**

* **Hot standby mode** (Режим горячей замены )

  Когда вы настраиваете два сервера с ролью DHCP, реализованной в режиме горячей замены, или горячего резервирования, серверы работают в отношениях отказоустойчивости. Активный сервер предоставляет IP-адреса и информацию о настройке клиентам. **Второй же сервер выполняет эту функцию в том случае, если первый недоступен.**



Чтобы настроить отказоустойчивый вариант DHCP, выполните следующие шаги:

1. Установите роль DHCP на двух отдельных серверах под управлением Server 2012, которые являются членами одного и того же домена Active Directory (AD).
2. Убедитесь, что роль DHCP на каждом сервере авторизована в AD.
3. Создайте соответствующие области на первом сервере DHCP.
4. Выберите область адресов, для которой вы включаете функцию отказоустойчивости. В меню Action нажмите **Configure Failover**.
5. На странице Introduction to DHCP Failover мастера Configure Failover убедитесь в наличии выбранной вами области и нажмите Next.
6. На странице **Specify the partner server to use for failover** нажмите Add Server. На экране 3 в окне Add Server вы видите список всех компьютеров Server 2012, выполняющих служебную роль DHCP и авторизованных в домене. Выберите сервер DHCP, который хотите использовать в качестве сервера-партнера, и нажмите OK.
7. На странице Specify the partner server to use for failover нажмите Next.
8. На странице **Create a new failover relationship** выберите либо режим Load balance, либо Hot standby в раскрывающемся списке Mode.
9. Если вы настраиваете сервер в режиме балансировки нагрузки, определите приоритет weight, который нужно назначить каждому серверу. По умолчанию каждый сервер работает в варианте равномерного распределения нагрузки equal load, как показано на экране 4. Если вы настраиваете сервер в режиме горячей замены, задайте роль сервера-партнера (Active, либо работающий в режиме ожидания Standby) и процент адресов, выделенный для резервного сервера из диапазона, как показано на экране 5.
10. При желании задайте параметр **State Switchover Interval**. Данная настройка определяет временной интервал до начала выдачи резервным сервером адресов клиентам сети.
11. Выберите общий секретный ключ **shared secret**. Это позволит вам объединить в пару серверы DHCP. Щелкните **Next**.
12. На последней странице нажмите **Finish**.