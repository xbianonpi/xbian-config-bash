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
cp etc/bash_completion.d/* /etc/bash_completion.d/
cd /home/xbian/xbian-config-bash/gettext/
msgfmt -o /usr/share/locale/en/LC_MESSAGES/xbian.mo xbian.po
echo 'APT::Update::Post-Invoke-Success {"touch /var/lib/apt/periodic/update-success-stamp 2>/dev/null || true";};' > /etc/apt/apt.conf.d/15update-stamp
```

If you see wierd characters in xbian-config, followed the parts of these steps you didn't already do:
```
export LANG=C.UTF-8
export LC_ALL=C.UTF-8
export LANGUAGE=C.UTF-8

if [ $(grep 'echo -ne' /etc/profile | grep 47l | grep 47h | wc -l) -eq 0 ]; then
	sed -i "s/export PATH/echo -ne '\\\e%G\\\e[?47h\\\e%G\\\e[?47l'\nexport PATH/g" /etc/profile
fi

if [ $(grep ".UTF-8$" /etc/profile | wc -l) -lt 3 ]; then
	sed -i '/export LANG=/d' /etc/profile
	sed -i '/export LANGUAGE=/d' /etc/profile
	sed -i '/export LC_ALL=/d' /etc/profile
	sed -i 's/export PATH/export PATH\nexport LANG=C.UTF-8\nexport LC_ALL=C.UTF-8\nexport LANGUAGE=C.UTF-8/g' /etc/profile
	if [ $(grep ".UTF-8$" /etc/profile | wc -l) -eq 3 ]; then
		export LANG=C.UTF-8 &>/dev/null
		export LC_ALL=C.UTF-8 &>/dev/null
		export LANGUAGE=C.UTF-8 &>/dev/null
	fi
fi

wget -O - https://github.com/xbianonpi/xbian/blob/master/usr/bin/dialog?raw=true > /usr/bin/dialog
chmod +x /usr/bin/dialog
```
