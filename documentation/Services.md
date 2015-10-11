Services
==


    
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
    root@edison:~# systemctl status python-butterfly.service -l

