- [x] 随系统缩放正常
- [x] 中文输入法正常
- [x] 进度条跳点不会有奇怪的声音（如果删除全部自带库的话，会出现这种情况，并报错`libmad error: bad main_data_begin pointer`）
- [ ] 进度条随机跳点多次，会导致偶然的小停顿，这是网易云自身的小bug，需上游修复
- [ ] 主界面前置时，托盘图标右键会闪烁，需上游修复

----

## 问题来源

网易云音乐linux版v1.2.1，在arch和manjaro中无法输入中文，原因是软件自带库qcef所导致的，具体为一下目录和文件：

```
/opt/netease/netease-cloud-music/libs/qcef
/opt/netease/netease-cloud-music/libs/libqcef.so
/opt/netease/netease-cloud-music/libs/libqcef.so.1
/opt/netease/netease-cloud-music/libs/libqcef.so.1.1.4
```

## 解决方案

- 重新编译qcef，并安装，具体请参考其[这里](https://github.com/springzfx/archlinux/tree/master/qcef)，（虽然archlinux官方源中有现成的安装包，但未及时更新，有缩放的bug，所以自行编译就好）
- 只删除网易云音乐自带库qcef, 详情见[PKGBUILD](https://github.com/springzfx/archlinux/blob/master/qcef/PKGBUILD)

```bash
# compile qcef 1.1.6
cd qcef
makepkg -si
# build 
cd netease-cloud-music
makepkg -si
```



致谢 

[@laomocode](https://aur.archlinux.org/account/laomocode) 找到的网易云音乐无法输入中文的原因