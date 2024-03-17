# TensorBoard使用笔记

1，**更改 TensorBoard 端口：** 尝试更改 TensorBoard 的运行端口。你可以使用 `--port` 参数指定端口号，例如：

```
tensorboard --logdir=logs --port=6006
```

2，**增加启动超时时间：** 通过 `--reload_interval` 参数增加 TensorBoard 的启动超时时间。例如：

```
tensorboard --logdir=logs --reload_interval=300
```

3，**更新 TensorBoard 和 TensorFlow：** 更新你的 TensorFlow 和 TensorBoard 到最新版本，因为新版本通常会修复一些 bug。

```
pip install --upgrade tensorflow tensorboard
```

4，**手动启动 TensorBoard：** 尝试手动启动 TensorBoard，看看是否会有更详细的错误信息。

```
tensorboard --logdir=logs
```

5，**找到占用端口的程序：** 使用以下命令查找占用端口 6006 的程序：

```
lsof -i :6006
```

6，**更改 TensorBoard 的端口：** 使用 `--port` 参数选择一个不同的端口，例如：

```
tensorboard --logdir=logs --port=6007
```

7，**停止占用端口的程序：** 如果你确定哪个程序占用了端口 6006，可以尝试停止该程序。你可以使用 `kill` 命令终止进程，例如：

```
kill -9 <PID>
```

8，**查看端口占用情况：** 使用以下命令查看系统中所有正在使用的端口：

```
netstat -tulpn
```

9，**清除插件缓存：** 打开命令行终端，运行以下命令：

```
rm -rf ~/.tensorboard-plugins
```

10，**找 TensorBoard 进程的 PID：**

```
ps aux | grep tensorboard
```

11，**用 `kill` 命令停止 TensorBoard 进程：**

```
kill -9 <PID>
```