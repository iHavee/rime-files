# Rime 配置

各平台配置文件路径

* Windows
    * Weasel: %APPDATA%\Rime
* Mac OS X
    * Squirrel: ~/Library/Rime
* Linux
    * iBus: ~/.config/ibus/rime
    * Fcitx: ~/.config/fcitx/rime

配置扩展词库需要文件

1. 快捷键、候选栏、输入方案选单等等定义
    * default.custom.yaml
2. 朙月拼音自定义
    * luna_pinyin.simp.custom.yaml
3. 扩充词库定义
    * luna_pinyin.extended.dict.yaml
4. 外观样式定义
    * weasel.custom.yaml (Windows)
    * squirrel.custom.yaml (Mac OS X)

# installation.yaml

该文件仅作为参考，如果需要同步，则添加下面一行。

    installation_id: "Rime"

譬如在 OS X 下，同步工具的目录创建一个文件夹 **Rime**，并软链接到 **~/Library/Rime/sync**

    ln -s /your/synctool/path/Rime  ~/Library/Rime/sync/

如果你也想使用 iCloud Drive 来同步，那么，请参见文章 [给 Rime 添加第三方词库](http://havee.me/mac/2015-05/rime-configuration-summary.html) 的最后 **同步** 部分。
