Linux系统是多用户多任务的分时操作系统，任何一个要使用系统资源的用户都必须申请一个账号进入系统。
用户的账号对使用系统的用户进行跟踪，并控制他们对系统资源的访问；也帮助用户组织文件，并为用户提供安全性保护
一、Linux系统用户账号的管理
              1、添加新的用户账号
                        useradd 选项 用户名
                        参数说明：
                                  -c comment 指定一段注释性描述。
                                  -d 目录 指定用户主目录，如果此目录不存在，则同时使用-m选项，可以创建主目录。
                                  -g 用户组 指定用户所属的用户组。
                                  -G 用户组，用户组 指定用户所属的附加组。
                                  -s Shell文件 指定用户的登录Shell。
                                  -u 用户号 指定用户的用户号，如果同时有-o选项，则可以重复使用其他用户的标识号。
              2、删除帐号
                        userdel 选项 用户名
                        常用的选项是 -r,把用户的主目录一起删除
              3.修改帐号
                        usermod 选项 用户名
                        可以使用选项：-l 新用户名
              4、用户口令的管理
                        用户账号刚创建时没有口令，但是被系统锁定，无法使用，必须为其指定口令后才可以使用，即使是指定空口令。
                        passwd 选项 用户名
                        可使用的选项：
                                    -l 锁定口令，即禁用账号。
                                    -u 口令解锁。
                                    -d 使账号无口令。
                                    -f 强迫用户下次登录时修改口令。
                        普通用户只能修改自己的口令
二、Linux系统用户组的管理
            1、增加一个新的用户组
                        groupadd 选项 用户组
                        可以使用的选项
                                      -g GID 指定新用户组的组标识号（GID）。
                                      -o 一般与-g选项同时使用，表示新用户组的GID可以与系统已有用户组的GID相同。
                         不指定选项则在当前已有的最大组标识号的基础上加1
                         # groupadd -g 101 group2
             2、如果要删除一个已有的用户组
                          groupdel 用户组
             3、修改用户组的属性
                          groupmod 选项 用户组
                          选项有：
                                  -g GID 为用户组指定新的组标识号。
                                  -o 与-g选项同时使用，用户组的新GID可以与系统已有用户组的GID相同。
                                  -n新用户组 将用户组的名字改为新名字
                                  # groupmod –g 10000 -n group3 group2   // 将组group2的标识号改为10000，组名修改为group3
             4、如果一个用户同时属于多个用户组，那么用户可以在用户组之间切换，以便具有其他用户组的权限。
                           $ newgrp root
三、与用户账号有关的系统文件
              1、/etc/passwd文件
                        每个用户都在/etc/passwd文件中有一个对应的记录行，它记录了这个用户的一些基本属性
                        每行记录又被冒号(:)分隔为7个字段
                                    用户名:口令:用户标识号:组标识号:注释性描述:主目录:登录Shell
                        伪用户在/etc/passwd文件中也占有一条记录，但是不能登录，因为它们的登录Shell为空
                        常见伪用户：
                                    bin 拥有可执行的用户命令文件 
                                    sys 拥有系统文件 
                                    adm 拥有帐户文件 
                                    uucp UUCP使用 
                                    lp lp或lpd子系统使用 
                                    nobody NFS使用
               2./etc/shadow文件
                        Linux系统都把加密后的口令字分离出来，单独存放在/etc/shadow文件中
                        若干个字段组成：
                                        登录名:加密口令:最后一次修改时间:最小时间间隔:最大时间间隔:警告时间:不活动时间:失效时间:标志
               3./etc/group文件
                        用户组的所有信息
                        干个字段：组名:口令:组标识号:组内用户列表
四、添加批量用户
                （1）编辑一个文本用户文件
                          每一列按照/etc/passwd密码文件的格式书写，其中密码栏可以留做空白或输入x号
                （2）以root身份执行命令 /usr/sbin/newusers
                          # newusers < user.txt
                          检查 /etc/passwd 文件是否已经出现这些用户的数据
                 （3）执行命令/usr/sbin/pwunconv
                          # pwunconv
                          将 /etc/shadow 产生的 shadow 密码解码，然后回写到 /etc/passwd 中，并将/etc/shadow的shadow密码栏删掉
                  （4）编辑每个用户的密码对照文件
                          user001:密码
                          user002:密码
                   （5）以root身份执行命令 /usr/sbin/chpasswd
                           # chpasswd < passwd.txt
                    （6）确定密码经编码写入/etc/passwd的密码栏后
                            # pwconv
                  
                          
           
              
