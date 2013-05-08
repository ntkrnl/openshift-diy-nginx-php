Nginx + PHP 一键包  （OpenShift）
============================
这是一个 OpenShift 上的 Nginx + php-fpm 一键包的 repo 。

更多有关 OpenShift 的信息，请访问：https://openshift.redhat.com/

这只是一个翻译，加上对于原作者的小小修正。

文件都是些啥？
-------------

**`.openshift/action_hooks` 文件夹中的脚本：**

* build
    - 自动搭建 Nginx, PHP, node.js 的脚本。
* build_*
    - 用于检测版本和安装。
* deploy
    - 这个将会自动修改 Nginx 和 PHP 的配置文件。
    - 如果不存在，复制 .bash_profile 文件。
* common
    - 用于重启时输出路径。（必需）
* start
    - 启动 Nginx 和 PHP。（必需）
* stop
    - 停止 Nginx 和 PHP。（必需）

**`.openshift/tmpl` 文件夹中的模版：**

这里是一些用于脚本搭建和部署的模版。
可自行修改。

**`web/` Nginx 网络文件夹**

目前使用的网络文件夹。你可以修改 `.openshift/tmpl/nginx.conf.tmpl` 文件来修改网络文件夹的位置。

使用
-----

要让 PHP 5.4 在 OpenShift 上运行，你需要进行以下步骤：

1. 创建一个新的 Openshift "Do-It-Yourself" 应用；
2. 创建时使用本 repo；
3. 通过 SSH 连接到你的 gear ；
4. cd 到 action_hooks ；
5. 运行 `sh build` ；
6. 等待编译完成（这将持续至少一个小时）；
7. 运行 `sh deploy` ；
8. 打开 http://appname-namespace.rhcloud.com/ 来验证安装是否成功。

** 在重启app时可能会出现端口被占用的情况，解决方法如下：

1. `lsof -i :8080` ；
2. 找到占用8080端口的pid号，使用 `kill -9 pid` 杀掉进程（pid为占用端口的pid号）；
3. 再次重启应用。

其他
-----

当在你自己的工程中通过复制粘贴使用 action hooks 时候别忘记使用 `git update-index --chmod=+x -- $(git ls-files .openshift/action_hooks/*)`。

** 上一句话仅对使用 `git push` 搭建 OpenShift 者有效 **

目前 [nodejs](http://nodejs.org/) 只会在版本与已安装的不相同时才会安装，它只创建一个到 npm 的代理，通过这样避免更多的错误。

鸣谢
------

感谢:

* [@sgoettschkes](https://github.com/Sgoettschkes)
* [@drejohnson](https://github.com/drejohnson)
* [@openshift](https://github.com/openshift/)
* [@boekkooi](https://github.com/boekkooi)

计划
------
这是一些将要去做的计划，请随意提出请求。

* 让 PHP `--with-mcrypt` 可以编译
* 测试更新功能更加彻底
* 利用 Jenkins (http://jenkins-ci.org/) 测试
* 喝杯[咖啡](https://www.gittip.com/Warnar%20Boekkooi/)

