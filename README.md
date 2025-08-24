# ConfigServer Security & Firewall (CSF)

## Installation

Installation is quite straightforward:

```bash
cd /usr/src
rm -fv csf.gz
wget https://raw.githubusercontent.com/afgshayan/CSF-Latest-24-AUG-2025/main/csf.gz
tar -xzf csf.gz
cd csf
sh install.sh
```

Next, test whether you have the required iptables modules:

```bash
perl /usr/local/csf/bin/csftest.pl
```

Don't worry if you cannot run all the features, so long as the script doesn't report any **FATAL** errors.

You should not run any other iptables firewall configuration script. For example, if you previously used APF+BFD you can remove the combination (which you will need to do if you have them installed otherwise they will conflict):

```bash
sh /usr/local/csf/bin/remove_apf_bfd.sh
```

That's it. You can then configure **csf** and **lfd** by reading the documentation and configuration files in:

- `/etc/csf/csf.conf`
- `/etc/csf/readme.txt`

directly or through the CSF User Interface.

- CSF installation for **cPanel** and **DirectAdmin** is preconfigured to work on those servers with all the standard ports open.
- CSF auto-configures your SSH port on installation where it's running on a non-standard port.
- CSF auto-whitelists your connected IP address where possible on installation.

You should ensure that kernel logging daemon (**klogd**) is enabled. Typically, VPS servers running RedHat/CentOS v5 have this disabled and you should check `/etc/init.d/syslog` and make sure that any `klogd` lines are not commented out. If you change the file, remember to restart syslog.

See the `csf.conf` and `readme.txt` files for more information.

---

## Perl Modules

While most should be installed on a standard Perl installation, the following may need to be installed manually:

**On RPM-based systems:**
```bash
yum install perl-libwww-perl.noarch perl-LWP-Protocol-https.noarch perl-GDGraph
```

**On APT-based systems:**
```bash
apt-get install libwww-perl liblwp-protocol-https-perl libgd-graph-perl
```

**Via CPAN:**
```bash
perl -MCPAN -eshell
cpan> install LWP LWP::Protocol::https GD::Graph
```

---

## InterWorx

1. Enable CSF in **InterWorx > NodeWorx > Plugins > csf**
2. See the InterWorx section in `/etc/csf/readme.txt`

---

## Webmin Module Installation/Upgrade

To install or upgrade the CSF webmin module:

1. Install CSF as above  
2. Install the CSF webmin module in:  

   ```
   Webmin > Webmin Configuration > Webmin Modules >  
   From local file > /usr/local/csf/csfwebmin.tgz > Install Module
   ```

---

## Uninstallation

Removing CSF and LFD is even more simple:

```bash
cd /etc/csf
sh uninstall.sh
```
