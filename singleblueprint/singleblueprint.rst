.. Adding labels to the beginning of your lab is helpful for linking to the lab from other pages
.. _singleblueprint:

----------------
创建单虚拟机蓝图
----------------

开始你第一个蓝图
++++++++++++++++

按照下图选在 **左侧倒数第二个图标** ，选择创建第一个蓝图

  .. figure:: images/f1.png
      :width: 70 %

选择 **Next** 

  .. figure:: images/f2.png
      :width: 70 %

选择 **Next** 

  .. figure:: images/f3.png
      :width: 70 %

选择 **Next** 

  .. figure:: images/f4.png
      :width: 70 %

用自己的名字命名应用，选择 **Launch and Create App**

  .. figure:: images/f5.png
      :width: 70 %

等待蓝图创建完成

  .. figure:: images/f6.png
      :width: 70 %

从右上角选择 **Launch Console** ，并使用默认用户名口令登录  **root / nutanix/4u**

  .. figure:: images/f7.png
      :width: 70 %


创建自定义蓝图
++++++++++++++

接下来我们看下如何创建自定义蓝图。从左侧图标选择 **Blueprint** 进入蓝图页面，从左上角选择 **Create Blueprint** --> **Single VM Blueprint**

  .. figure:: images/s0.png
      :width: 70 %

使用你自己的名字命名蓝图名称，并选择项目 **default**

  .. figure:: images/s1.png
      :width: 70 %

使用你自己的名字命名虚拟机名称，**Cloud** 选择 **Nutanix** ，操作系统选择 **Linux**

  .. figure:: images/s2.png
      :width: 70 %

指定虚拟机规格，包括CPU内存等参数，确定使用 **cloudinit** 脚本对虚拟机进行初始化，主要是创建用户，代码从下面复制

  .. code-block::

    #cloud-config
    disable_root: False
    ssh_pwauth: True
    password: nutanix/4u
    chpasswd: { expire: False }

  .. figure:: images/s31.png
      :width: 70 %

滚动页面选择虚拟机镜像 **CentOS7.qcow2**

  .. figure:: images/s32.png
      :width: 70 %

滚动页面在 **NICs** 下，添加一个网卡，并选择对应的网络（网络应该已经被创建在AHV上）

  .. figure:: images/s33.png
      :width: 70 %

选择保存后，进入第4步 **Advanced Options** ，选择 **Add/Edit Credentials**

  .. figure:: images/s41.png
      :width: 70 %

添加默认用户名 **centos** ，密码是 **nutanix/4u**

  .. figure:: images/s42.png
      :width: 70 %

在 **Connection** 下，选中 **Check login upon create** ，并在下拉框中选择上一步创建的用户名

  .. figure:: images/s43.png
      :width: 70 %

滚动页面到 **Packages** ，点击 **Package Install** 右侧的 **Edit** ，添加一个任务。任务类型是 **Execute** ；脚本类型是 **Shell** ；Credential使用 **centos** ；任务代码请从下面复制

  .. code-block::

    sudo yum update -y

  .. figure:: images/s44.png
      :width: 70 %

完成并回到前一页面，选择页面上方 **Save**

  .. figure:: images/s45.png
      :width: 70 %

选择页面右上角 **Launch** ，运行这个蓝图，并用自己名字命名这个App

  .. figure:: images/s5.png
      :width: 70 %


