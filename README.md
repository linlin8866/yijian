bash <(curl -sSL https://raw.githubusercontent.com/linlin8866/yijian/main/jiaobei.sh)


bash <(curl -sSL https://ghproxy.com/https://raw.githubusercontent.com/linlin8866/yijian/main/jiaobei.sh)


一键关闭防火墙

sudo ufw disable

一键更新系统

apt update -y

发行版

bash <(curl https://i.hiddify.com/release)

开发版

bash <(curl https://i.hiddify.com/dev)

beta版

bash <(curl https://i.hiddify.com/beta)


# 系统更新 + 安装依赖工具
apt update -y && apt install -y curl socat wget

# 关闭防火墙（ufw）
sudo ufw disable





# 系统更新
yum update -y

# 安装依赖工具
yum install -y curl socat wget



；CentOS 系统常用  systemctl stop firewalld && systemctl disable firewalld



#!/bin/bash

# 定义颜色输出
RED='\033[0;31m'
GREEN='\033[0;32m'
NC='\033[0m' # No Color

echo -e "${GREEN}=== 系统初始化一键脚本 ===${NC}"

# 检测系统类型
if [ -f /etc/os-release ]; then
    . /etc/os-release
    OS=$ID
elif type lsb_release >/dev/null 2>&1; then
    OS=$(lsb_release -si)
else
    OS=$(uname -s)
fi

OS=$(echo "$OS" | tr '[:upper:]' '[:lower:]')

echo -e "${GREEN}[+] 检测到系统: ${OS}${NC}"

# 1. 更新系统并安装依赖
case $OS in
    debian|ubuntu)
        echo -e "${GREEN}[+] 正在更新系统并安装依赖 (Debian/Ubuntu)...${NC}"
        apt update -y && apt install -y curl socat wget
        ;;
    centos|rhel|almalinux|rocky)
        echo -e "${GREEN}[+] 正在更新系统并安装依赖 (CentOS/RHEL)...${NC}"
        yum update -y && yum install -y curl socat wget
        ;;
    *)
        echo -e "${RED}[!] 不支持的系统类型: ${OS}${NC}"
        exit 1
        ;;
esac

# 2. 关闭防火墙
case $OS in
    debian|ubuntu)
        echo -e "${GREEN}[+] 正在关闭 ufw 防火墙...${NC}"
        if command -v ufw >/dev/null 2>&1; then
            ufw disable
            echo -e "${GREEN}[+] ufw 防火墙已禁用${NC}"
        else
            echo -e "${RED}[!] 未检测到 ufw 防火墙，跳过${NC}"
        fi
        ;;
    centos|rhel|almalinux|rocky)
        echo -e "${GREEN}[+] 正在关闭 firewalld 防火墙...${NC}"
        systemctl stop firewalld
        systemctl disable firewalld
        echo -e "${GREEN}[+] firewalld 防火墙已禁用${NC}"
        ;;
esac

echo -e "${GREEN}=== 所有操作完成 ===${NC}"





bash <(cat << 'EOF'
#!/bin/bash

# 定义颜色输出
RED='\033[0;31m'
GREEN='\033[0;32m'
NC='\033[0m' # No Color

echo -e "${GREEN}=== 系统初始化一键脚本 ===${NC}"

# 检测系统类型
if [ -f /etc/os-release ]; then
    . /etc/os-release
    OS=$ID
elif type lsb_release >/dev/null 2>&1; then
    OS=$(lsb_release -si)
else
    OS=$(uname -s)
fi

OS=$(echo "$OS" | tr '[:upper:]' '[:lower:]')

echo -e "${GREEN}[+] 检测到系统: ${OS}${NC}"

# 1. 更新系统并安装依赖
case $OS in
    debian|ubuntu)
        echo -e "${GREEN}[+] 正在更新系统并安装依赖 (Debian/Ubuntu)...${NC}"
        apt update -y && apt install -y curl socat wget
        ;;
    centos|rhel|almalinux|rocky)
        echo -e "${GREEN}[+] 正在更新系统并安装依赖 (CentOS/RHEL)...${NC}"
        yum update -y && yum install -y curl socat wget
        ;;
    *)
        echo -e "${RED}[!] 不支持的系统类型: ${OS}${NC}"
        exit 1
        ;;
esac

# 2. 关闭防火墙
case $OS in
    debian|ubuntu)
        echo -e "${GREEN}[+] 正在关闭 ufw 防火墙...${NC}"
        if command -v ufw >/dev/null 2>&1; then
            ufw disable
            echo -e "${GREEN}[+] ufw 防火墙已禁用${NC}"
        else
            echo -e "${RED}[!] 未检测到 ufw 防火墙，跳过${NC}"
        fi
        ;;
    centos|rhel|almalinux|rocky)
        echo -e "${GREEN}[+] 正在关闭 firewalld 防火墙...${NC}"
        systemctl stop firewalld
        systemctl disable firewalld
        echo -e "${GREEN}[+] firewalld 防火墙已禁用${NC}"
        ;;
esac

echo -e "${GREEN}=== 所有操作完成 ===${NC}"
EOF
)



