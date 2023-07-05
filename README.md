# -deb
mkdir myscript && cd myscript

dh_make --native -y -p myscript_1.0

cd debian

rm *ex *EX

nano postinst

```
"!/bin/bash
cat <<EOF > /opt/myscript.sh
#!/bin/bash
echo "Что вы хотите сделать? 1. Примонтировать. 2. Отмонтировать"
read num
if [ $num =  1 ]; then
        sudo mkdir /mnt/usb
        sudo mount /dev/sda /mnt/usb
        ls /mnt/usb
else
        sudo umount /dev/sda
fi
EOF
chmod +x /opt/myscript.sh
```

chmod +x postinst

nano control

``` 
  GNU nano 2.7.4                               Файл: control                                        

Source: myscript
Section: unknown
Priority: optional
Maintainer: Sergey Bondar <morrisYT@yandex.ru>
Build-Depends: debhelper (>= 9)
Standards-Version: 3.9.8
```

cd ..

dpkg-buildpackage -us -uc

cd ..

sudo dpkg -i myscript_1.0_amd64.deb
