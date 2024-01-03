# ROS2
my ros2 learning process
# How to connect windows with ROS2 in jetson TX2?
Now I have a Jetson TX2, and I want to connect Jetson with windows remote screen, the following is the steps. If you think it is a good thing to help you, please give me a star, thankyou:)
## 1.set windows
you need 
## 2.
1、笔记本电脑连接wifi，使用网线把笔记本电脑和nano/nx连接起来
2、点击笔记本电脑右下角的wifi设置，点击“未识别的网络”

3、点击右侧的“更改适配器选项”

4、点击“WLAN”，然后右键，选择“属性–>共享”

5、笔记本电脑打开“cmd”，输入

arp -a
1

nano的ip地址即是：192.168.137.198
6、安装putty，下载链接

7、打开putty，输入上面ip地址，open，输入nano的账号密码


8、nano上配置vnc，在putty终端Terminal上输入

sudo apt-get install xrdp vnc4server xbase-clients
1
9、进入nano/nx桌面，打开“Setting–>Desktop sharing”，没反应，据说是bug，我试过nano和nx都一样。首先输入下面命令编辑配置文件

sudo vim /usr/share/glib-2.0/schemas/org.gnome.Vino.gschema.xml
1
10、vim的操作命令（i是进入编辑，esc–>:wq!是强制保存退出），在文件的后面添加代码

    <key name='enabled' type='b'>
      <summary>Enable remote access to the desktop</summary>
      <description>
        If true, allows remote access to the desktop via the RFB
        protocol. Users on remote machines may then connect to the
        desktop using a VNC viewer.
      </description>
      <default>false</default>
    </key>

1
2
3
4
5
6
7
8
9
10
13、编译生效，无报错即可

sudo glib-compile-schemas /usr/share/glib-2.0/schemas

1
2
14、打开“Setting–>Desktop sharing”，设置如下

15、安装dconf-editor解除加密，依次打开org–>gnome–>desktop–>remote-access，取消require-encryption的勾选

sudo apt-get install dconf-editor
dconf-editor
1
2

16、打开终端Terminal，输入下面代码，开启VNC server

/usr/lib/vino/vino-server
1
17、在笔记本电脑端安装VNC Viewwe链接，输入ip地址，点击继续



三、Window10的远程桌面连接
1-15步骤与上面二、VNC Viewer远程连接完全一致
16、笔记本电脑上打开远程桌面连接，输入ip地址连接后，再输入nano的账号密码登录




17、如果远程桌面显示“败家之眼”后，出现闪退问题，需要先用显示器和键盘连接到nano上进行设置


17、安装xfce4文件并编辑

//打开终端，输入
sudo apt-get install xfce4
echo xfce4-session >~/.xsession
touch .session
sudo vim/etc/xrdp/startwm.sh
//编辑文件,在打开的startwm.sh文件前面加
xfce4-session
//重启xrdp
sudo service xrdp restart
1
2
3
4
5
6
7
8
9
18、重新打开电脑远程连接，输入ip地址以及nano账号密码，成功打开一个xfce4-panel远程桌面

19、xfce4-panel远程桌面有可能无法打开终端Terminal，需要先在nano/nx那边的unity系统打开终端Terminal，输入代码

sudo update-alternatives --config x-terminal-emulator  // 修改terminal指向,输入xterm对应的数字:6
1


20、需要在nano/nx那边的unity系统退出用户登录Logout，否则xfce4-panel远程桌面打开浏览器或者文件夹，只会在unity系统显示
————————————————
版权声明：本文为CSDN博主「Stars-Chan」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/weixin_44942126/article/details/118754248
