xbian-config-bash
=================

```
sudo su
cd /home/xbian
git clone --depth 5 https://github.com/xbianonpi/xbian-config-bash.git
rm /usr/local/sbin/xbian-config
rm -r /usr/local/include/xbian-config/*
cd xbian-config-bash
cp xbian-config /usr/local/sbin/
cp -R functions /usr/local/include/xbian-config/
cp -R lang /usr/local/include/xbian-config/
cp -R modules /usr/local/include/xbian-config/
cp -R prereqs /usr/local/include/xbian-config/
cp -R struct /usr/local/include/xbian-config/
cp -R config /usr/local/include/xbian-config/
echo 'APT::Update::Post-Invoke-Success {"touch /var/lib/apt/periodic/update-success-stamp 2>/dev/null || true";};' > /etc/apt/apt.conf.d/15update-stamp
```
