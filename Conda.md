# Conda
为 Python 程序创建的环境管理工具，适用于 Linux，OS X 和 Windows，也可以打包和分发其他软件（R, Ruby, Lua, Scala, Java, JavaScript, C/C++, FORTRAN）。
> 例如系统里会存在多个版本的 Python，环境管理的价值在于将同一个 Python 版本的不同需求分开

## Conda,Miniconda,Anaconda 三者区别
+ Anaconda：一个非常流行的 Python 发行版，用于科学计算。它包含了 Vonda、Python 和超过 150 个科学软件包及其依赖项；
+ Miniconda：Anaconda 的轻量级版本，只包含了 Python 和 Conda，以及它们的依赖项;
+ Conda：一个开源的包管理系统和环境管理系统，用于安装多种语言的软件包。<br>
>根据不同的需求，从 Anaconda 和 Miniconda 二者选其一进行，进行安装即可：
>+ 方便，省事，想一步到位就可以选 Anaconda；
>+ 想要小巧，灵活，快速就选 Miniconda。

## 安装 Anaconda

## conda 环境设置

~~~
export PATH=/home/xuem1/software/anaconda3/bin/conda:$PATH




# >>> conda initialize >>>
# !! Contents within this block are managed by 'conda init' !!
 __conda_setup="$('/data/software/anaconda3/bin/conda' 'shell.bash' 'hook' 2> /dev/null)"
 if [ $? -eq 0 ]; then
     eval "$__conda_setup"
 else
     if [ -f "/data/software/anaconda3/etc/profile.d/conda.sh" ]; then
         . "/data/software/anaconda3/etc/profile.d/conda.sh"
    else
         export PATH="/data/software/anaconda3/bin:$PATH"
     fi
 fi
unset __conda_setup

export CONDA_PKGS_DIRS=/data/home/xuem1/.conda/pkgs

# <<< conda initialize <<<
~~~

~~~
conda --version
~~~
确定是否设置成功

## Conda 管理环境
当开始使用 conda 时，已经默认创建了一个 base 的环境，但是，如果不想将程序放入这个基础环境（base）中，可以选择创建单独的环境以使程序彼此隔离。

### 查看已安装的环境
借助 conda info 命令可以查看与 conda 相关的一些信息，配合 -e, --envs 选项，可以查看所有环境的列表
~~~
conda info -envs
~~~

\* 指示当前所处环境

### 创建新环境
通过 conda create 命令可以创建一个新环境，利用 --name 选项，可以为新环境命名。
~~~
conda create -name python_3.10 python=3.10

# 创建一个名为 python_3.10 的包含 Python 3.10 的新环境
~~~

### 激活环境

~~~
conda activate python_3.10
~~~
+ 如果直接使用 conda activate （不带环境名），会默认切回 base 环境
+ conda activate 仅适用于 conda 4.6 及更高版本
+ 
### 安装包

~~~
conda install pandas
~~~

### 查看已安装的包

~~~
conda list
~~~

### 移除已安装的包

~~~
conda remove pandas --force
~~~

### 移除已创建的环境

~~~
conda remove -name python_3.10 --all
~~~
