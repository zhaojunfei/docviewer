# docviewer
源码bug已经修复

#创建数据库
CREATE DATABASE docviewerdb DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;
#创建用户并授权
grant all privileges on docviewerdb.* to docviewer@localhost identified by 'docviewer';
#刷新权限
flush privileges;

use docviewerdb;

create table documentrelation(
id int auto_increment primary key,
filename varchar(255) not null,
location varchar(2000) not null,
createDate timestamp not null);

安装openoffice

wget http://jaist.dl.sourceforge.net/project/openofficeorg.mirror/4.1.3/binaries/ast/Apache_OpenOffice_4.1.3_Linux_x86-64_install-rpm_ast.tar.gz

tar -zxvf Apache_OpenOffice_4.1.3_Linux_x86-64_install-rpm_ast.tar.gz

cd zh-CN/RPMS/

rpm -Uvh *.rpm desktop-integration/openoffice4.1.3-redhat-menus-4.1.3-9783.noarch.rpm

#使用图形桌面首次配置openoffice
#命令行下执行
openoffice4  
#启动服务

soffice -headless -accept="socket,host=127.0.0.1,port=8100;urp;" -nofirststartwizard
#后台启动服务
nohup soffice -headless -accept="socket,host=127.0.0.1,port=8100;urp;" -nofirststartwizard &
#检查服务是否启动成功
netstat -nap|grep 8100

安装pdf2swf
#centos 7 安装开发编译工具

yum install gcc* automake zlib-devel libjpeg-devel giflib-devel freetype-devel


wget http://www.swftools.org/swftools-0.9.2.tar.gz
tar vxzf swftools-0.9.2.tar.gz
cd swftools-0.9.2
./configure --prefix=/usr/swftools
make

make install
#如果make install出错,请修改：Makefile Makefile.in
#参考http://blog.csdn.net/zhizaibide1987/article/details/28902229

#设置环境变量

vim /etc/profile
export PATH=$PATH:/usr/swftools/bin/
