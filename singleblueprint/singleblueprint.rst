.. Adding labels to the beginning of your lab is helpful for linking to the lab from other pages
.. _singleblueprint:

----------------
创建单虚拟机蓝图
----------------

创建自定义蓝图
++++++++++++++

接下来我们看下如何创建自定义蓝图。从左侧图标选择 **Blueprint** 进入蓝图页面，从左上角选择 **Create Blueprint** --> **Single VM Blueprint**

  .. figure:: images/s0.png
      :width: 70 %

使用你自己的名字命名蓝图名称，并选择项目 **default**

  .. figure:: images/s1.png
      :width: 70 %

使用你自己的名字命名虚拟机名称， **Cloud** 选择 **Nutanix** ，操作系统选择 **Linux**

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


修改资源
++++++++

- 进入 **App** 页面
- 选择刚才运行的应用

  .. figure:: images/up1.png
      :width: 70 %

- 选择右上角 **Update** --> **Update VM Configuration**
- 修改CPU数量 **2** --> **4**
- 修改内存数量 **4** --> **8**

  .. figure:: images/up2.png
      :width: 70 %

  .. figure:: images/up3.png
      :width: 70 %

  .. note:: 缩小配置会导致虚拟机关机并重启

修改Action
++++++++++

- 进入 **App** 页面
- 选择刚才运行的应用
- 选择右上角 **Update** --> **Update Actions & Credentials**

  .. figure:: images/act1.png
      :width: 70 %

- 选择 **+Add action**
- 在左上角给Action命名，比如 **My Action1**

  .. figure:: images/act2.png
      :width: 70 %

- 选择Task，并输入具体需要执行的Task内容，如下图

  .. figure:: images/act3.png
      :width: 70 %

- 完成后选择 **Done** ， 并再次确认修改，选择 **Confirm**

  .. figure:: images/act4.png
      :width: 70 %

- 新Action已经创建，选择 **Update** ， 保存修改

  .. figure:: images/act5.png
      :width: 70 %

- 从应用页面中查看Action已经被创建，并执行

  .. figure:: images/act6.png
      :width: 70 %

  .. figure:: images/act7.png
      :width: 70 %


