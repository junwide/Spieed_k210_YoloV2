# Spieed_k210_YoloV2

This repository helps you to **Customized** the models is to detect objects using [YOLO-V2](https://pjreddie.com/media/files/papers/YOLO9000.pdf)

这个仓库能帮助你学会客制化基于YOLOv2的目标模型训练

# Requirement(基本要求)

Machine：8GB > Memory 

OS：Windows 10（20H2）+ WSL2

APP：Docker（for WSL2）

# Env. Tutorial(搭建环境教程)

Follow the [Tutorial](https://docs.docker.com/docker-for-windows/wsl/) and Install the Docker, Use the following command to check the version in WSL.

跟随[教程](https://docs.docker.com/docker-for-windows/wsl/)安装Docker，然后在WSL使用下列命令检测安装版本。

```bash
#wsl
$ docker --version
```

![image-20210306193017993](https://gitee.com/junwide/blog/raw/master/20210306193018.png)

create a `notebooks` folder inside e.g. `Documents`:

在`Documents`中创建一个`notebook`文件夹

```sh
#wsl
mkdir ~/Documents/notebooks/
```
Then, deploy the `tensorflow/tensorflow:latest-py3-jupyter` image using:

然后，部署`tensorflow/tensorflow:latest-py3-jupyter`的镜像

```bash
$ sudo docker run -d -p 8888:8888 -v ~/Documents/notebooks/:/tf/notebooks/ tensorflow/tensorflow:latest-py3-jupyter
```
(Optional) If you have NVIDIA GPU, you can use the following command instead.

(可选的)，如果你拥有英伟达的GPU，你可以使用下面的命令

```bash
$ sudo docker run -d -p 8888:8888 -v ~/Documents/notebooks/:/tf/notebooks/ tensorflow/tensorflow:latest-gpu-py3-jupyter
```

> The `-v` flag means mount. It is a "Bind Mount". This means the `~/Documents/notebooks/` folder is connected to the `/tf/notebooks/` folder inside the container. This makes the data inside the folder `/tf/notebooks/` (container) persistent. Otherwise, if the container is stopped you lose the files.

> “-v”表示挂载的意思。这是一个“绑定安装”。这意味着“~/Documents/notebook /”文件夹连接到容器中的“/tf/notebook /”文件夹。这使得容器中的文件夹' /tf/notebook / '中的数据是持久的。否则，如果容器停止，文件将丢失。

Then, clone this repository inside `~/Documents/notebooks/`

然后，把这个仓库clone下来到`~/Documents/notebooks/`

```sh
cd ~/Documents/notebooks/
git clone https://github.com/junwide/Spieed_k210_YoloV2
```



Open Docker， go into `Containers/Apps`，and Click the Green Cube Name `tensorflow:latest-py3-jupyter`

打开docker，进入到`Containers/Apps`，然后点击`tensorflow:latest-py3-jupyter`的绿色立方体

![image-20210306195544970](https://gitee.com/junwide/blog/raw/master/20210306195545.png)

And Find the key in the log，copy it Use `Ctrl-C`

然后再log中找到密钥，然后复制他

![image-20210306195746267](https://gitee.com/junwide/blog/raw/master/20210306195746.png)



Then， open your docker and click the`open in Browser`

然后，打开你的docker然后点击 `open in Browser`

![image-20210306195041002](https://gitee.com/junwide/blog/raw/master/20210306195041.png)

![image-20210306195919270](https://gitee.com/junwide/blog/raw/master/20210306195919.png)

Use the key to Log in.

使用刚才的密钥登陆。 

# Usage （用法）

![image-20210306200303406](https://gitee.com/junwide/blog/raw/master/20210306200303.png)

You Need to know these. 你需要了解以下的信息

`configs`:  The folder have trains configs. 训练的配置文件所在文件夹

`datasets`：The dataset. 训练数据集所在文件夹

`result`：save the model. 训练完模型所在文件夹

`trainig.ipynb`：train code 训练代码

`evaluation.ipynb`：evaluation code 评估代码

----

Note： First cell just run when you are first use it.

你第一次使用时才需要运行第一个单元 .

![image-20210306201055545](https://gitee.com/junwide/blog/raw/master/20210306201055.png)



# Convert  Model（转化模型）

First of all, get the `MAix_toolbox` from :

首先，需要获取`MAix_toolbox`工具

```bash
#wsl
$ git clone https://github.com/sipeed/Maix_Toolbox.git
```

Then, download the library `nncase` typing:

下载`nncase`的库

```bash
#wsl
cd Maix_Toolbox
./get_nncase.sh
```

To convert the model, `nncase` needs some example images for inference. These example images have to be the same resolution as the input image's resolution to your model. The input size is defined in the configuration file `configs/fire.json` as:

为了转换模型，`nncase`需要一些示例图像进行推断。这些示例图像的分辨率必须与模型输入图像的分辨率相同。输入大小在配置文件`configs / fire.json`中定义为：

```json
{
    "model" : {
        "architecture":         "MobileNet",
        "input_size":           224,
        [...]
        }
}
```

The images' sizes are 224x224 pixels. Put these images in a `images` folder inside `Maix_Toolbox` and copy also the `xxx.tflite` file to the `Maix_Toolbox` folder. Finally, convert the Tensorflow Lite model to a `.kmodel` using:

图片尺寸为224x224像素。将这些图像放入“ Maix_Toolbox”内的“ images”文件夹中，并将“ xxx.tflite”文件也复制到“ Maix_Toolbox”文件夹中。最后，使用以下命令将Tensorflow Lite模型转换为`.kmodel`：

```sh
./tflite2kmodel.sh xxx.tflite
```

If you successfully convert the model, you will get a `xxx.kmodel` file and you will see:

如果成果转化，你会得到一个kmodel文件，然后看到以下信息：

![image-20210306202701478](https://gitee.com/junwide/blog/raw/master/20210306202701.png)

# Acknowledgement（致谢）

* Base on [lemariva/MaixPy_YoloV2](https://github.com/lemariva/MaixPy_YoloV2)  Jupyter Notebooks

* 基于[lemariva/MaixPy_YoloV2](https://github.com/lemariva/MaixPy_YoloV2)  Jupyter Notebooks

