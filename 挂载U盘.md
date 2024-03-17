# 挂载U盘

1，确保U盘是linux系统支持的U盘格式

2，需要使用sudo权限

## 下面是命令

`sudo -i` 是以超级用户（root）身份登录到系统的命令。使用这个命令后，你将获得完全的系统管理员权限，可以执行系统中的几乎所有任务。要退出 `sudo -i`，你可以使用 `exit` 命令。

```bash
sudo -i # 进入管理员权限
fdisk -l # 查找插入服务器的U盘
sudo mkdir /mnt/usb #创建一个挂载U盘的文件
sudo mount /dev/sdc1 /mnt/usb # 挂载U盘
sudo ls /mnt/usb # 查看挂载完U盘的内容
‘’‘
之后就可以进行操作了
sudo cp -r /mnt/usb/modelnet40_ply_hdf5_2048 /home/chengjun/cj/CJ_PyCharm/Project/Point_Cloud_registration/PointNet_Concat_FC # 复制到需要的文件中
’‘’
sudo umount /mnt/usb # 卸载 U 盘
sudo eject /dev/sdc1 # 弹出U盘
exit # 退出管理员权限
```

