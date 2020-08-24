# How to create a Aggregation with Jumbo Frame (9000)

**List network interfaces**
```console
-bash-4.4# dladm show-phys
-bash-4.4# dladm show-phys -L
-bash-4.4# dladm show-link
```

---

**For our example we use net2 and net3, first remove all configuration**
```console
-bash-4.4# ipadm delete-ip net2
-bash-4.4# ipadm delete-ip net2
```

---

**Create Aggregation (aggr0)**
```console
-bash-4.4# dladm delete-aggr aggr0
-bash-4.4# dladm create-aggr -l net2 -l net3 aggr0
-bash-4.4# dladm modify-aggr -P L2 -L active -T short aggr0
-bash-4.4# dladm show-aggr
```

**Change MTU**
```console
-bash-4.4# dladm show-linkprop -p mtu aggr0
-bash-4.4# dladm set-linkprop -p mtu=9000 aggr0
-bash-4.4# dladm show-link aggr0
```

---

**Configure the aggregation as a network interface and add ip address**
```console
-bash-4.4# ipadm create-ip aggr0
-bash-4.4# ipadm create-addr -T static -a 192.0.2.10/29 aggr0/v4
-bash-4.4# ipadm 
```

**List network interfaces**
```console
-bash-4.4# dladm show-phys
-bash-4.4# dladm show-phys -L
-bash-4.4# dladm show-link
-bash-4.4# dladm show-aggr
```