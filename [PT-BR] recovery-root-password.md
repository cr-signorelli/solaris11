# Solaris 11 - Recuperando / Reset da senha de root

---

Através da ILOM acesse "prompt ok" via console e faça o boot pelo CD/DVD ou RCDROM.
```console
{0} ok boot dvd
```

Selecione o teclado 27 (US-English).
```console
USB keyboard
1. Arabic             15. Korean
2. Belgian            16. Latin-American
3. Brazilian          17. Norwegian
4. Canadian-Bilingual 18. Portuguese
5. Canadian-French    19. Russian
6. Danish             20. Spanish
7. Dutch              21. Swedish
8. Dvorak             22. Swiss-French
9. Finnish            23. Swiss-German
10. French            24. Traditional-Chinese
11. German            25. TurkishQ
12. Italian           26. UK-English
13. Japanese-type6    27. US-English
14. Japanese
To select the keyboard layout, enter a number [default 27]:27
```

Selecione o idioma 3 (English).
```console
1. Chinese - Simplified
2. Chinese - Traditional
3. English
4. French
5. German
6. Italian
7. Japanese
8. Korean
9. Portuguese - Brazil
10. Spanish
To select the language you wish to use, enter a number [default is 3]: 3
```

Quando entrar no menu de instalação entre na opção 3 (Shell).
```console
Welcome to the Oracle Solaris installation menu

1 Install Oracle Solaris
2 Install Additional Drivers
3 Shell
4 Terminal type (currently xterm)
5 Reboot
Please enter a number [1]: 3
```

Realizado o import do Root Pool.
```console
root@solaris:/root# zpool import rpool
```

Listando o Boot Environment 
```
root@solaris:/root# beadm list
```

Saída esperada.
```
be_find_current_be: failed to find current BE name
BE Active Mountpoint Space Policy Created
-- ------ ---------- ----- ------ -------
solaris R - 2.32G static 2013-08-06 02:54
```

Montando o Boot Environment, em mount point temporário.
```console
root@solaris:/root# beadm mount solaris /a
```

Verifique se o filesystem foi montado corretamente.
```console
root@solaris:/root# df -h /a
```

Saída esperada.
```
Filesystem Size Used Available Capacity Mounted on
rpool/ROOT/solaris 274G 2.1G 264G 1% /a
```

Editando o arquivo de senhas, removendo a senha do root.
```console
root@solaris:/root# vi /a/etc/shadow
```

Apague a hash da senha do usuário root.

Exemplo de uma linha com a senha.
```console
root:$5$QfObWpuZ$J7G8MgJmXoNm35l1oGHw1j138gBKzzK20UtME.qhPNB:15923::::::22624
```

Exemplo de uma linha sem a senha.
```console
root::15923::::::22624
```

Editando o arquivo que permite usuários efetuarem login com senhas em branco.
```console
root@solaris:/root# vi /a/etc/default/login
```

Procure a opção PASSREQ e altere de YES para NO.
```console
PASSREQ=NO
```

Fazer a atualização do Boot Archive
```console
root@solaris:/root# bootadm update-archive -R /a
root@solaris:/root# reboot
```

Quando apresentar o prompt de login, digite root e tecle ENTER.
```console
ldom console login: root
Aug 6 21:13:50 ldom7 login: ROOT LOGIN /dev/console
Last login: Tue Aug 6 20:34:44 on console
Oracle Corporation SunOS 5.11 11.1 September 2012
root@ldom:~#
```