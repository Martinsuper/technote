# docker基础镜像安装ssh服务

```Dockerfile
# 选择一个已有的os镜像作为基础  
FROM centos
# 镜像的作者  
MAINTAINER martin "luyao.duan@martind.cn" 
  
# 安装openssh-server和sudo软件包，并且将sshd的UsePAM参数设置成no  
RUN yum install -y openssh-server sudo  
RUN sed -i 's/UsePAM yes/UsePAM no/g' /etc/ssh/sshd_config  
  
RUN echo "root:1234567" | chpasswd  
  
# 下面这两句比较特殊，在centos6上必须要有，否则创建出来的容器sshd不能登录  
#将基础镜像的/etc/ssh/目录下的ssh_host_rsa_key  ssh_host_rsa_key.pub  
#和ssh_host_dsa_key  ssh_host_dsa_key.pub 删除或者下面的不执行  
RUN ssh-keygen -t dsa -f /etc/ssh/ssh_host_dsa_key  
RUN ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key  
  
# 启动sshd服务并且暴露22端口  
RUN mkdir /var/run/sshd  
EXPOSE 22  
CMD ["/usr/sbin/sshd", "-D"]  
```