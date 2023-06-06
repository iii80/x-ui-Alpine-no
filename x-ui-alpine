#!/bin/sh
#

red='\033[31m\033[01m'
green='\033[32m\033[01m'
yellow='\033[33m\033[01m'
plain='\033[0m'
echo -e "${green}Alpine安装x-ui一键脚本by mocikate "
echo -e "${green}免手搓Alpine安装x-ui方法: "
echo -e "----------------------------------------------"
echo -e "${red}一路回车，啥也别说！"
echo -e "${red}安全起见，安装两遍！"
echo -e "${green}x-ui安装使用的是原版"
echo -e "${green}脚本只是让x-ui运行到Alpine"
echo -e "${green}并自动设置开机自启"
echo -e "${red}x-ui面板命令无效，请打开web管理操作"
echo -e "${green}用户名密码admin，port9000"
echo -e "${yellow}一路回车，啥也别说！"
echo -e "${yellow}安全起见，安装两遍！"
echo -e "----------------------------------------------"
read -p "回车键继续..."
echo -e "${green}x-ui install for alpine"
echo "检查安装环境"
apk add curl && apk add bash && apk add sudo && apk add wget
mkdir /lib64
cp /lib/ld-musl-x86_64.so.1 /lib64/ld-linux-x86-64.so.2

echo "安装Alpine所需文件"
curl -Ls https://github.com/ozersource/x-ui-Alpine/raw/main/xuidb/x-ui.db -o x-ui.db
curl -Ls https://github.com/ozersource/x-ui-Alpine/raw/main/xuidb/config.json -o config.json
curl -Ls https://github.com/ozersource/x-ui-Alpine/raw/main/xuidb/x-ui -o x-ui
mv x-ui.db /etc/x-ui/
mv x-ui /etc/init.d/
mv config.json  /usr/local/x-ui/bin/
chown 501.dialout /etc/x-ui/x-ui.db
chown 501.dialout /usr/local/x-ui/bin/config.json
chmod +x /etc/init.d/x-ui
chmod 0644 /etc/x-ui/x-ui.db
chmod 0644 /usr/local/x-ui/bin/config.json
rc-update add /etc/init.d/x-ui
/etc/init.d/x-ui start

show_menu() {
echo -e "
  ${green}选择x-ui 面板${plain}
  ${green}0.${plain} 退出脚本
  ${green}1.${plain} 安装 x-ui vaxilu（原版）
  ${green}2.${plain} 安装 x-ui MHSanaei（伊朗版,暂时无效！）"
}
show_menu
echo && read -p "默认原版，请输入选择 [0-2]: " num
    case "${num}" in
        0) exit 0
        ;;
        1) url="https://raw.githubusercontent.com/vaxilu/x-ui/master/install.sh"
        ;;
        2) url="https://raw.githubusercontent.com/mhsanaei/3x-ui/master/install.sh"
        ;;
        *) url="https://raw.githubusercontent.com/vaxilu/x-ui/master/install.sh"
        ;;
    esac


echo -e "${green}安装x-ui"
echo -e "${yellow}注意：安装完成x-ui，修改用户名时直接回车，不用理会错误"
echo -e "${red}注意：安装完成x-ui，修改用户名时直接回车，不用理会错误"
echo -e "${yellow}注意：安装完成x-ui，修改用户名时直接回车，不用理会错误"
echo -e "${red}注意：安装完成x-ui，修改用户名时直接回车，不用理会错误"
bash <(curl -Ls $url )


echo -e "${plain}x-ui安装完成"
#/usr/local/x-ui/x-ui setting -username admin -password admin -port 9000
echo -e "${green}用户名admin,密码admin,端口9000(访问注意映射)"
echo -e "${green}正在启动x-ui...."
/etc/init.d/x-ui restart
echo -e "${green}尝试重启sshd....如果有错误可以忽视"
rc-update add sshd
rc-service sshd restart
echo -e "${plain}全部完成，如果x-ui没启动成功，需要再安装一次"
echo -e "${plain}请不要用x-ui命令管理x-ui！！！直接在web里进行管理"
