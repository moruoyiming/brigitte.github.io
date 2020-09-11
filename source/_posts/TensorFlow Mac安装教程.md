---

.安装Python 3.7.5 版本
百度云盘:
链接:[https://pan.baidu.com/s/1lC7ZPFAIB8pYor1DbIOL8Q](https://links.jianshu.com/go?to=https%3A%2F%2Fpan.baidu.com%2Fs%2F1lC7ZPFAIB8pYor1DbIOL8Q) 密码:v6tj
官网:
[https://www.python.org/ftp/python/3.7.5/python-3.7.5-macosx10.9.pkg](https://links.jianshu.com/go?to=https%3A%2F%2Fwww.python.org%2Fftp%2Fpython%2F3.7.5%2Fpython-3.7.5-macosx10.9.pkg)

查看版本号。

```
python3 --version
pip3 --version
virtualenv --version
```

输入which python3 查看路径

<!-- more -->

2.如果已经安装，跳过这步：
如果没用过brew，需要先下载，关于brew查看这里: [https://brew.sh/](https://links.jianshu.com/go?to=https%3A%2F%2Fbrew.sh%2F)

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

 export PATH="/usr/local/bin:/usr/local/sbin:$PATH"
```



```
/usr/bin/ruby -e "PATH"
brew update
brew install python # Python 3
sudo pip3 install -U virtualenv # system-wide install
```

3.安装virtualenv虚拟环境
创建一个新的虚拟环境通过选择一个Python解释器,创建./venv目录来保存它:可修改为其他目录。
目录会出现在 user的子目录下。

```
virtualenv --system-site-packages -p python3 ./venv
```

4.激活虚拟环境

```
source ./venv/bin/activate # sh, bash, ksh, or zsh
```

virtualenv活跃时,shell提示符前缀(venv)。 　　 安装包在一个虚拟环境在不影响主机系统设置。先升级pip:

```
pip install --upgrade pip
pip list # show packages installed within the virtual environment
```

5.退出虚拟环境

deactivate # don't exit until you're done using TensorFlow

如果提示权限不够时，需要在命令后添加 --user。

6.安装TensorFlow

```
pip install --upgrade tensorflow
```

验证安装

```
python -c "import tensorflow as tf;print(tf.reduce_sum(tf.random.normal([1000, 1000])))"
```

问题汇总

```
pip install Keras-Applications
```

ModuleNotFoundError: No module named 'matplotlib'

```
pip install matplotlib
```

ModuleNotFoundError: No module named 'tensorflow_datasets'

```
pip install tensorflow_datasets
```

ModuleNotFoundError: No module named 'tensorflow_hub'

```
pip install tensorflow_hub
```

seaborn 绘制矩阵图 (pairplot)

```
pip install seaborn
```

引入类库

# TensorFlow and tf.keras

```
import tensorflow as tf
from tensorflow import keras
```

# Helper libraries

import numpy as np
import matplotlib.pyplot as plt
import pandas as pd
import seaborn as sns