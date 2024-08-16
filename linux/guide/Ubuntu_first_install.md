# 우분투 앱

우분투 설치시 기본 앱 모음.

> first\_install.sh

```shell
install_list=(
              "
              zip
              unzip
              git-all
              terminator
              "
              )
#virtualBoxInstall
#install_list=(
#              "
#              mailcap
#              gnome-menus
#              desktop-file-utils
#              hicolor-icon-theme
#              shared-mime-info
#              "
#              )

for app in $install_list
  do
    if [ `dpkg -l | grep -c $app` -eq 0 ]
    then
        sudo apt-get install -Y $app
    fi
  done


# 스냅 리스트

install_snap_list=(
  "
    notion-snap

  "
)
```
