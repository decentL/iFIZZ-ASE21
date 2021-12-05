# iFIZZ-ASE21

# IFIZZ: Deep-State and Efficient Fault-Scenario Generation to Test IoT Firmware

"[IFIZZ: Deep-State and Efficient Fault-Scenario Generation to Test IoT Firmware](https://nesa.zju.edu.cn/download/liu_pdf_ifizz.pdf)" published in [ASE 2021](https://conf.researchr.org/home/ase-2021).

## Docker Image

The Docker image is available [here (Google Drive)](https://drive.google.com/file/d/1QWua3q9QNSPpGzJn3JgGym1G31KUgokI/view?usp=sharing).

### Use the Docker Image

1. Import the image

```bash
$ docker import ifizz.tar ifizz:v1
```

2. Create a container

```bash
$ docker run --privileged -it --name iFIZZ -w /root/firmadyne ifizz:v1 /bin/sh -c 'su - postgres -c "/etc/init.d/postgresql start" &&   /bin/bash'
```

3. Run firmware in the container

```bash
$ export USER=root
$ ./scratch/1/run.sh
```

4. Login to the firmware

    user: root
    password: password

> NOTE:
> 
> how to exit the firmware: `CRTL+A`, `X`

5. Start the test

```bash
cd /etc
./begin.sh
```

> NOTE:
> 
> 1. how to check the test status: 
>
>    1.1 enter the contianer: `docker exec -it iFIZZ bash`
>
>    1.2 login to the firmware by ssh: `ssh root@192.168.0.100` (password is "password")
>
>    1.3 check the crash log: `cat /etc/crash_log`
>
> 2. how to test more software of the firmware: 
>
>   This Docker image only tests `ntpclient-wrapp` by default. If you want to test more software, please add the software name in the `/etc/blacklist` file in the firmware before executing`./begin.sh`. For example. if you want to test `sed`, please add "2 sed" to the `/etc/blacklist` file.
>
> 3. how to get the test results:
>
>   The test will take 24 hours. Please login to the firmware by ssh, and find the test results (crash logs) in the `root` dir.