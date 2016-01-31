Services
==

> Systemd is an init system and system manager that is widely becoming the new standard for Linux machines. While there are considerable opinions about whether systemd is an improvement over the traditional SysV init systems it is replacing, the majority of distributions plan to adopt it or have already done so

> systemctl command, the central management tool for controlling the init system



    root@edison:~# nano python-main.sh
    cd /home/root/python/script/location/
    python main.py
    root@edison:~# cd /lib/systemd/system
    root@edison:~# nano python-main.service
    [Unit]
    Description=Python Main
    After=sys-subsystem-net-devices-%i.device

    [Service]
    ExecStart=/bin/bash /home/root/python-main.sh
    Restart=always
    RestartSec=10 

    [Install]
    Alias=pythonmain
    WantedBy=multi-user.target
    
    root@edison:~# systemctl daemon-reload
    root@edison:~# systemctl --system enable python-main
    root@edison:~# systemctl start python-main
    root@edison:~# systemctl status python-main.service -l

