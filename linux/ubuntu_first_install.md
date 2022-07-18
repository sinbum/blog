

## 우분투 앱 모음

우분투 설치시 자주 사용하는 앱 모음.

> first_install.sh
```shell

install_list=(
              "
              zip
              unzip
              git-all
              "
              )

for app in $install_list
  do
    if [ `dpkg -l | grep -c $app` -eq 0 ]
    then
        sudo apt-get install $app
    fi
  done

```