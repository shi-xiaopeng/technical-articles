# 安装
pip install virtualenv

# 配置环境变量
在 ~/.bash_profile 中添加
 
# 创建环境
进入项目的目录下，执行 virtualenv --python=python3.6 env_name
创建成功，当前目录下会生成一个 env_name 的 目录

# 启动
source env_name/bin/activate  启动成功，shell 前会出现 环境名的 title;
之后就可以使用 pip 等工具了，安装的包都会在env_name的目录下。

# 退出
deactivate  退出当前环境

# 删除环境
直接删除目录即可

