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

## default.custom.yaml

    patch:
      switcher:
        abbreviate_options: true
        caption: 〔切换〕
        fold_options: true
        hotkeys:
          - "Control+grave"                                  # control + `
          - "Control+s"                                      # 添加 Ctrl+s
        save_options:
          - full_shape
          - ascii_punct
          - simplification
          - extended_charset
      menu:
        page_size: 5                                         # 候选词数量

      schema_list:                                           # 激活的输入方案选单，这里只保留朙月拼音・简化字
        - schema: luna_pinyin_simp

      ascii_composer:
        switch_key:
          Caps_Lock: noop
          Control_L: noop
          Control_R: noop
          Eisu_toggle: clear
          Shift_L: commit_code
          Shift_R: commit_code

## squirrel.custom.yaml/weasel.custom.yaml

    patch:
      show_notifications_via_notification_center: true
      us_keyboard_layout: true                               # 美式键盘布局
      show_notifications_when: appropriate                   # 状态通知条，默认growl_is_running，也可设置为全开（always）全关（never）

      style:
        color_scheme: light                                  # 配色方案名称

      preset_color_schemes:
        light:
          name: register                                     # 作者名
          author: "register <registerdedicated(at)gmail.com>"# 作者

          horizontal: true                                   # 候选条横向显示
          inline_preedit: true                               # 启用内嵌编码模式，候选条首行不显示拼音
          candidate_format: "%c\u2005%@\u2005"               # 用 1/6 em 空格 U+2005 来控制编号 %c 和候选词 %@ 前后的空间。

          corner_radius: 5                                   # 候选条圆角半径
          border_height: 7                                   # 窗口边界高度，大于圆角半径才生效
          border_width: 7                                    # 窗口边界宽度，大于圆角半径才生效
          back_color: 0xFFFFFF                               # 候选条背景色
          border_color: 0xE0B693                             # 边框色
          font_face: "PingFangSC-Regular"                    # 候选词字体
          font_point: 18                                     # 预选栏文字字号
          label_font_face: "PingFangSC-Light"                # 候选词编号字体
          label_font_point: 18                               # 预选栏编号字号
          candidate_text_color: 0x000000                     # 预选项文字颜色
          text_color: 0x000000                               # 拼音行文字颜色，24位色值，16进制，BGR顺序
          comment_text_color: 0x999999                       # 拼音等提示文字颜色
          hilited_text_color: 0xFF6941                       # 高亮拼音 (需要开启内嵌编码)
          hilited_candidate_text_color: 0xFF6941             # 第一候选项文字颜色
          hilited_candidate_back_color: 0xFFFFFF             # 第一候选项背景背景色
          hilited_comment_text_color: 0xFF6941               # 注解文字高亮

      app_options:
        com.blacktree.Quicksilver: &a
          ascii_mode: false
        com.googlecode.iterm2: *a
        com.alfredapp.Alfred: *a
        com.runningwithcrayons.Alfred-2: *a
        org.vim.MacVim: *a
        com.apple.Terminal: *a

## luna_pinyin.simp.custom.yaml

    patch:
      switches:
        - name: ascii_mode
          reset: 0
          states: ["中文", "西文"]
        - name: full_shape
          states: ["半角", "全角"]
        - name: zh_simp
          reset: 1
          states: ["漢字", "汉字"]
        - name: ascii_punct
          states: ["。，", "．，"]

      simplifier:
        option_name: zh_simp

      "engine/filters/@next": cjk_minifier
      "engine/translators/@next": reverse_lookup_translator

      translator:
        dictionary: luna_pinyin.extended                     # 扩展词库
        enable_charset_filter: true                          # 罕见字过滤

      "speller/algebra/@before 0": xform/^([b-df-hj-np-tv-z])$/$1_/

      punctuator:                                            # 符号快速输入和部分符号的快速上屏
        import_preset: symbols
        full_shape:
          "\\": "、"
        half_shape:
          "#": "#"
          "`": "`"
          "~": "~"
          "@": "@"
          "=": "="
          "/": ["/", "÷"]
          '\': "、"
          "'": {pair: ["「", "」"]}
          "[": ["【", "["]
          "]": ["】", "]"]
          "$": ["¥", "$", "€", "£", "¢", "¤"]
          "<": ["《", "〈", "«", "<"]
          ">": ["》", "〉", "»", ">"]

      recognizer:
        patterns:
          email: "^[A-Za-z][-_.0-9A-Za-z]*@.*$"
          uppercase: "[A-Z][-_+.'0-9A-Za-z]*$"
          url: "^(www[.]|https?:|ftp[.:]|mailto:|file:).*$|^[a-z]+[.].+$"
          punct: "^/([a-z]+|[0-9]0?)$"
          reverse_lookup: "`[a-z]*'?$"

## luna_pinyin.extended.dict.yaml

    ---
    name: luna_pinyin.extended
    version: "2015.12.02"
    sort: by_weight
    use_preset_vocabulary: true
    import_tables:
      - luna_pinyin                                      # 内置词库
      - luna_pinyin.hanyu
      - luna_pinyin.poetry
      - luna_pinyin.sogou
      - luna_pinyin.computer
      - luna_pinyin.name
      - luna_pinyin.daily
    ...

## installation.yaml

该文件仅作为参考，如果需要同步，则添加下面一行。

    installation_id: "Rime"

譬如在 OS X 下，同步工具的目录创建一个文件夹 **Rime**，并软链接到 **~/Library/Rime/sync**

    ln -s /your/synctool/path/Rime  ~/Library/Rime/sync/

如果你也想使用 iCloud Drive 来同步，那么，请参见文章 [给 Rime 添加第三方词库](http://havee.me/mac/2015-05/add-dic-for-rime.html) 的最后 **同步** 部分。
