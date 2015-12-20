Python Package Index
==

> The Python Package Index or PyPI is the official third-party software repository for the Python programming language. Python developers intend it to be a comprehensive catalog of all open source Python packages. Wikipedia

> The Python Package Index is a repository of software for the Python programming language. Official Homepage

- [Python Package Index Homepage](https://pypi.python.org/pypi)
- [Python Package Index Wikipedia](https://en.wikipedia.org/wiki/Python_Package_Index)


    root@edison:~# pip search psutil
    psutil                    - psutil is a cross-platform library for retrieving
                                information onrunning processes and system
                                utilization (CPU, memory, disks, network)in
                                Python.
    root@edison:~# pip install psutil
    Downloading/unpacking psutil
      Running setup.py egg_info for package psutil
    
        warning: no previously-included files matching '*' found under directory 'docs/_build'
        warning: manifest_maker: MANIFEST.in, line 18: 'recursive-include' expects <dir> <pattern1> <pattern2> ...
        
    Installing collected packages: psutil
      Running setup.py install for psutil
        
        warning: no previously-included files matching '*' found under directory 'docs/_build'
        warning: manifest_maker: MANIFEST.in, line 18: 'recursive-include' expects <dir> <pattern1> <pattern2> ...
    
    Successfully installed psutil
    Cleaning up...
    root@edison:~# 


## Python Pip Optional 

    
    root@edison:~# pip install <package name> --target /other/path package
    root@edison:~# export PYTHONPATH=$PYTHONPATH:/other/path
    root@edison:~# echo "export PYTHONPATH=$PYTHONPATH:/other/path" >> /etc/profile

