Squirrel 鼠须管配置
-------------------

**installation.yaml**

该文件仅作为参考，如果需要同步，则添加下面一行。

    installation_id: "Rime"

在你同步工具的目录创建一个文件夹 **Rime**，并软链接到 **~/Library/Rime/sync**

    ln -s /your/synctool/path/Rime  ~/Library/Rime/sync/

如果你也想使用 iCloud Drive 来同步，那么，请参见文章 [给 Rime 添加第三方词库](http://havee.me/mac/2015-05/add-dic-for-rime.html) 的最后 **同步** 部分。
