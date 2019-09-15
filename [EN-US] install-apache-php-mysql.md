# How to install Apache / PHP / MySQL on Solaris11.3 SPARC

**Link direct to the Oracle documentation:**

- <a href="https://docs.oracle.com/cd/E53394_01/html/E54831/gnvkd.html#scrolltoc" target="_blank">`Install MySQL`</a> 
- <a href="https://docs.oracle.com/cd/E36784_01/html/E54155/mysql.html" target="_blank">`Install Mysql`</a> 

---

**Before install some recommended packages** 
```console
-bash-3.2# pkg install system/library/gcc-3-runtime
-bash-3.2# pkg install developer/library/lint 
-bash-3.2# pkg install developer/gcc-3 
-bash-3.2# pkg install text/gnu-grep 
-bash-3.2# pkg install developer/macro/gnu-m4 
-bash-3.2# pkg install developer/build/gnu-make 
-bash-3.2# pkg install system/library/security/libgcrypt 
-bash-3.2# pkg install library/gnutls
-bash-3.2# pkg install security/kerberos-5/kdc
-bash-3.2# pkg install system/library/security/rpcsec
-bash-3.2# pkg install developer/build/make
-bash-3.2# pkg install developer/linker
-bash-3.2# pkg install system/header
-bash-3.2# pkg install developer/object-file
-bash-3.2# pkg install developer/library/profiled-libc
-bash-3.2# pkg install compatibility/ucb
-bash-3.2# pkg install compatibility/ucb
-bash-3.2# pkg install library/libxslt
-bash-3.2# pkg install library/gnutls
-bash-3.2# pkg install library/security/openssl
-bash-3.2# pkg install library/pcre
```

---

**Alternatively, you can install the group/feature/amp package. This package contains Apache HTTP Server, MySQL database, and PHP.**
```console
-bash-3.2# pkg install group/feature/amp
```

---

**Enable the server so that it listens to the incoming HTTP requests:**
```console
-bash-3.2# svcadm -v enable /network/http:apache24
```

---

**Enable the database service**
```console
svcadm enable mysql
```

**Start the terminal to administration**
```console
mysqladmin -u root password pVIDzep3Xlhw4L8oU2zK
```

**Type mysql in a terminal window to access the mysql> prompt. For example:**
```mysql
mysql> show databases;
  Database
  information_schema 
  mysql 
  test
  3 rows in set (0.01 sec)

mysql> quit;
  Bye
```

---

**Test on browser http://localhost:80 link in a web browser. A web page should be displayed**





