Nginx + PHP 一键包  （OpenShift）   |   boekkooi/openshift-nginx-php54
============================
这是一个 OpenShift 上的 Nginx + php-fpm 一键包的 repo 。

This is a sample repository to get nginx + php fpm running on openshift.

更多有关 OpenShift 的信息，请访问：https://openshift.redhat.com/

More information about openshift: https://openshift.redhat.com/

这只是一个翻译，加上对于原作者的小小修正。

This repo is just a translation, and few bug fixed to the original repo.

文件都是些啥？   |   What's inside
-------------

**`.openshift/action_hooks` 文件夹中的脚本：**

**The `.openshift/action_hooks` scripts:**

* build
    - 自动搭建 Nginx, PHP, node.js 的脚本。
    - Build the versions of nginx, php and nodejs that are needed
* build_*
    - 用于检测版本和安装。
    - The functions used for checking the versions and installing
* deploy
    - 这个将会自动修改 Nginx 和 PHP 的配置文件。
    - This will render copy the nginx and php conf files
    - 如果不存在，复制 .bash_profile 文件。
    - Copy the .bash_profile if there is none
* common
    - 用于重启时输出路径。（必需）
    - A common include script for the action hooks (just setting some path's)
* start
    - 启动 Nginx 和 PHP。（必需）
    - Starts Nginx and php-fpm
* stop
    - 停止 Nginx 和 PHP。（必需）
    - Stops Nginx and php-fpm

**`.openshift/tmpl` 文件夹中的模版：**

**The `.openshift/tmpl` templates:**

这里是一些用于脚本搭建和部署的模版。
可自行修改。

Here are the templates used by the build and deploy scripts.
Just customize away.

**`web/` Nginx 网络文件夹**

**The `web/` nginx web folder:**

目前使用的网络文件夹。你可以修改 `.openshift/tmpl/nginx.conf.tmpl` 文件来修改网络文件夹的位置。

The web folder currently used. You can change this in `.openshift/tmpl/nginx.conf.tmpl`.

使用   |   Usage
-----

要让 PHP 5.4 在 OpenShift 上运行，你需要进行以下步骤：

To get PHP 5.4 working at OpenShift, you have to do the following:

* 1. 创建一个新的 Openshift "Do-It-Yourself" 应用；
 -  1. Create a new Openshift "Do-It-Yourself" application
* 2. 创建时使用本 repo；
 - 2. Use this repo when creating application
* 3. 通过 SSH 连接到你的 gear ；
 - 3. SSH into your gear
* 4. cd 到 action_hooks ；
 - 4. cd to action_hooks
* 5. 运行 `sh build` ；
 - 5. run `sh build`
* 6. 等待编译完成（这将持续至少一个小时）；
 - 6. Wait for build to finish (This may take at least an hour)
* 7. 运行 `sh deploy` ；
 - 7. run `sh deploy`
* 8. 打开 http://appname-namespace.rhcloud.com/ 来验证安装是否成功。
 - 8. Open http://appname-namespace.rhcloud.com/ to verify


**在重启app时可能会出现端口被占用的情况，解决方法如下：**

**When restarting app, it may appear the `Port in use` error, you can solve it by do the following:**

* 1. `lsof -i :8080` ；
* 2. 找到占用8080端口的pid号，使用 `kill -9 pid` 杀掉进程（pid为占用端口的pid号）；
 - 2. Find the pid of process that use the 8080 port, use `kill -9 pid` to kill the process ("pid" is the pid number of the process)
* 3. 再次重启应用。
 - 3. restart your app again.

其他   |   Other
-----

当在你自己的工程中通过复制粘贴使用 action hooks 时候别忘记使用 `git update-index --chmod=+x -- $(git ls-files .openshift/action_hooks/*)`。

When using the action hooks within you own project by copy-paste method don't forget todo `git update-index --chmod=+x -- $(git ls-files .openshift/action_hooks/*)`.


**上一句话仅对使用 `git push` 搭建 OpenShift 者有效**

**The sentence before just suit for the people who use `git push` to set up OpenShift application.**

目前 [nodejs](http://nodejs.org/) 只会在版本与已安装的不相同时才会安装，它只创建一个到 npm 的代理，通过这样避免更多的错误。

Currently [nodejs](http://nodejs.org) will only be build when the version is not the same a the one installed by default, it will just create a proxy for npm so it can be used with less problems.

鸣谢   |   Thanks
------

感谢:

Thanks to the following people:

* [@sgoettschkes](https://github.com/Sgoettschkes)
* [@drejohnson](https://github.com/drejohnson)
* [@openshift](https://github.com/openshift/)
* [@boekkooi](https://github.com/boekkooi)

计划   |   Todo's
------
这是一些将要去做的计划，请随意提出请求。

This is stuff which needs to be done right now. Feel free to do a pull request!

* 让 PHP `--with-mcrypt` 可以编译
 - Get php `--with-mcrypt` to compile
* 测试更新功能更加彻底
 - Test update functionality more thoroughly
* 利用 Jenkins (http://jenkins-ci.org/) 测试
 - Test with Jenkins (http://jenkins-ci.org/) builds
* 喝杯[咖啡](https://www.gittip.com/Warnar%20Boekkooi/)
 - Get a [cup of coffee](https://www.gittip.com/Warnar%20Boekkooi/)

