---
date: 2020-01-22 11:34:18
tags:
    - 杂项
---

在RHEL中，yum的配置文件为/etc/yum.repos.d/redhat.repo
里面是空的，没有任何仓库。

在这个目录下新建一个tsinghua.repo文件，写入：
```
[rhel-8-baseos-beta-source-rpms]
name = Red Hat Enterprise Linux 8 - BaseOS Beta (Source RPMs)
baseurl = https://mirrors.tuna.tsinghua.edu.cn/redhat/rhel/rhel-8-beta/baseos/source/
enabled = 1
gpgcheck = 1
gpgkey = file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-beta,file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release

[rhel-8-for-aarch64-baseos-beta-rpms]
name = Red Hat Enterprise Linux 8 for ARM 64 - BaseOS Beta (RPMs)
baseurl = https://mirrors.tuna.tsinghua.edu.cn/redhat/rhel/rhel-8-beta/baseos/aarch64/
enabled = 1
gpgcheck = 1
gpgkey = file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-beta,file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release

[rhel-8-for-ppc64le-baseos-beta-rpms]
name = Red Hat Enterprise Linux 8 for Power, little endian - BaseOS Beta (RPMs)
baseurl = https://mirrors.tuna.tsinghua.edu.cn/redhat/rhel/rhel-8-beta/baseos/ppc64le/
enabled = 1
gpgcheck = 1
gpgkey = file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-beta,file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release

[rhel-8-for-s390x-baseos-beta-rpms]
name = Red Hat Enterprise Linux 8 for IBM z Systems - BaseOS Beta (RPMs)
baseurl = https://mirrors.tuna.tsinghua.edu.cn/redhat/rhel/rhel-8-beta/baseos/s390x/
enabled = 1
gpgcheck = 1
gpgkey = file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-beta,file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release

[rhel-8-for-x86_64-baseos-beta-rpms]
name = Red Hat Enterprise Linux 8 for x86_64 - BaseOS Beta (RPMs)
baseurl = https://mirrors.tuna.tsinghua.edu.cn/redhat/rhel/rhel-8-beta/baseos/x86_64/
enabled = 1
gpgcheck = 1
gpgkey = file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-beta,file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release

[rhel-8-appstream-beta-source-rpms]
name = Red Hat Enterprise Linux 8 - AppStream Beta (Source RPMs)
baseurl = https://mirrors.tuna.tsinghua.edu.cn/redhat/rhel/rhel-8-beta/appstream/source/
enabled = 1
gpgcheck = 1
gpgkey = file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-beta,file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release

[rhel-8-for-aarch64-appstream-beta-rpms]
name = Red Hat Enterprise Linux 8 for ARM 64 - AppStream Beta (RPMs)
baseurl = https://mirrors.tuna.tsinghua.edu.cn/redhat/rhel/rhel-8-beta/appstream/aarch64/
enabled = 1
gpgcheck = 1
gpgkey = file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-beta,file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release

[rhel-8-for-ppc64le-appstream-beta-rpms]
name = Red Hat Enterprise Linux 8 for Power, little endian - AppStream Beta (RPMs)
baseurl = https://mirrors.tuna.tsinghua.edu.cn/redhat/rhel/rhel-8-beta/appstream/ppc64le/
enabled = 1
gpgcheck = 1
gpgkey = file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-beta,file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release

[rhel-8-for-s390x-appstream-beta-rpms]
name = Red Hat Enterprise Linux 8 for IBM z Systems - AppStream Beta (RPMs)
baseurl = https://mirrors.tuna.tsinghua.edu.cn/redhat/rhel/rhel-8-beta/appstream/s390x/
enabled = 1
gpgcheck = 1
gpgkey = file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-beta,file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release

[rhel-8-for-x86_64-appstream-beta-rpms]
name = Red Hat Enterprise Linux 8 for x86_64 - AppStream Beta (RPMs)
baseurl = https://mirrors.tuna.tsinghua.edu.cn/redhat/rhel/rhel-8-beta/appstream/x86_64/
enabled = 1
gpgcheck = 1
gpgkey = file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-beta,file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release

[rhel-8-ha-beta-source-rpms]
name = Red Hat Enterprise Linux 8 - HighAvailability Beta (Source RPMs)
baseurl = https://mirrors.tuna.tsinghua.edu.cn/redhat/rhel/rhel-8-beta/add-ons/ha/source/
enabled = 1
gpgcheck = 1
gpgkey = file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-beta,file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release

[rhel-8-for-ppc64le-ha-beta-rpms]
name = Red Hat Enterprise Linux 8 for Power, little endian - HighAvailability Beta (RPMs)
baseurl = https://mirrors.tuna.tsinghua.edu.cn/redhat/rhel/rhel-8-beta/add-ons/ha/ppc64le/
enabled = 1
gpgcheck = 1
gpgkey = file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-beta,file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release

[rhel-8-for-s390x-ha-beta-rpms]
name = Red Hat Enterprise Linux 8 for IBM z Systems - HighAvailability Beta (RPMs)
baseurl = https://mirrors.tuna.tsinghua.edu.cn/redhat/rhel/rhel-8-beta/add-ons/ha/s390x/
enabled = 1
gpgcheck = 1
gpgkey = file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-beta,file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release

[rhel-8-for-x86_64-ha-beta-rpms]
name = Red Hat Enterprise Linux 8 for x86_64 - HighAvailability Beta (RPMs)
baseurl = https://mirrors.tuna.tsinghua.edu.cn/redhat/rhel/rhel-8-beta/add-ons/ha/x86_64/
enabled = 1
gpgcheck = 1
gpgkey = file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-beta,file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release

[rhel-8-rs-beta-source-rpms]
name = Red Hat Enterprise Linux 8 - ResilientStorage Beta (Source RPMs)
baseurl = https://mirrors.tuna.tsinghua.edu.cn/redhat/rhel/rhel-8-beta/add-ons/rs/source/
enabled = 1
gpgcheck = 1
gpgkey = file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-beta,file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release

[rhel-8-for-ppc64le-rs-beta-rpms]
name = Red Hat Enterprise Linux 8 for Power, little endian - ResilientStorage Beta (RPMs)
baseurl = https://mirrors.tuna.tsinghua.edu.cn/redhat/rhel/rhel-8-beta/add-ons/rs/ppc64le/
enabled = 1
gpgcheck = 1
gpgkey = file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-beta,file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release

[rhel-8-for-s390x-rs-beta-rpms]
name = Red Hat Enterprise Linux 8 for IBM z Systems - ResilientStorage Beta (RPMs)
baseurl = https://mirrors.tuna.tsinghua.edu.cn/redhat/rhel/rhel-8-beta/add-ons/rs/s390x/
enabled = 1
gpgcheck = 1
gpgkey = file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-beta,file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release

[rhel-8-for-x86_64-rs-beta-rpms]
name = Red Hat Enterprise Linux 8 for x86_64 - ResilientStorage Beta (RPMs)
baseurl = https://mirrors.tuna.tsinghua.edu.cn/redhat/rhel/rhel-8-beta/add-ons/rs/x86_64/
enabled = 1
gpgcheck = 1
gpgkey = file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-beta,file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release

[rhel-8-rt-beta-source-rpms]
name = Red Hat Enterprise Linux 8 - RT Beta (Source RPMs)
baseurl = https://mirrors.tuna.tsinghua.edu.cn/redhat/rhel/rhel-8-beta/add-ons/rt/source/
enabled = 1
gpgcheck = 1
gpgkey = file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-beta,file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release

[rhel-8-for-x86_64-rt-beta-rpms]
name = Red Hat Enterprise Linux 8 for x86_64 - RT Beta (RPMs)
baseurl = https://mirrors.tuna.tsinghua.edu.cn/redhat/rhel/rhel-8-beta/add-ons/rt/x86_64/
enabled = 1
gpgcheck = 1
gpgkey = file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-beta,file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release
```
然后执行命令：
```
sudo yum clean all
sudo yum makecache
sudo yum update
```

