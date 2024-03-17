# bash 常用命令



1，上传文件到服务器(需要配置.ssh配置文件)

```bash
scp 3D-Registration-with-Maximal-Cliques-main.zip chengjun@i38944o710.goho.co:/home/chengjun
```

2，安装解压

```bash
sudo apt install unzip
unzip zipped_file.zip
```

3，修改编码格式

```bash
>vim demo.txt
>:set fileencoding
#显示
fileencoding=latin1


:setlocal buftype=
:set fileencoding=utf-8
:wq! 
 
>:set fileencoding
#显示
fileencoding=utf-8
```

