# jellyfin-danmaku

## Jellyfin danmaku extension
![截图](https://raw.githubusercontent.com/RyoLee/dd-danmaku/res/S0.png)

## 安装

任选以下一种方式安装即可

**注：** 安装完首次使用时，确保只有当前一个客户端访问服务器，以方便根据当前用户id获取Session时能唯一定位到当前客户端设备id。（主要是由于非Jellyfin Web客户端没有默认在localstorage中存储deviceid）

### 浏览器插件(推荐)

[添加脚本](https://raw.githubusercontent.com/killgfat/jellyfin-danmaku/jellyfin/ede.js)

### 修改服务端

修改文件 `/jellyfin/jellyfin-web/index.html` (Docker版,其他类似,比如Debian下是`/usr/share/jellyfin/web/index.html`),在`</body>`前添加如下标签

```html
<script src="https://raw.githubusercontent.com/killgfat/jellyfin-danmaku/jellyfin/ede.js" defer></script>
```

Docker中的操作方式为，用root进入容器终端后，运行以下命令

```bash
sed -i 's#</body>#<script src="https://raw.githubusercontent.com/killgfat/jellyfin-danmaku/jellyfin/ede.js" defer></script></body>#' /jellyfin/jellyfin-web/index.html
```

该方式安装与浏览器插件安装**可同时使用不冲突**

### 修改客户端

类似服务端方式,解包后修改 dashboard-ui/index.html 再重新打包即可,iOS 需要通过类似 AltStore 方式自签,请自行 Google 解决

## 界面

**请注意Readme上方截图可能与最新版存在差异,请以实际版本与说明为准**

左下方新增如下按钮,若按钮透明度与"暂停"等其他原始按钮存在差异,说明插件正在进行加载

- 弹幕开关: 切换弹幕显示/隐藏状态
- 手动匹配: 手动输入信息匹配弹幕
- 简繁转换: 在原始弹幕/简体中文/繁体中文3种模式切换
- 过滤等级: 过滤弹幕强度,等级越高强度越大,0级无限制*
- 弹幕信息: 通过通知(以及后台log)显示当前匹配弹幕信息

    **除0级外均带有每3秒6条的垂直方向弹幕密度限制,高于该限制密度的顶部/底部弹幕将会被转为普通弹幕*

## 弹幕

弹幕来源为 [弹弹 play](https://www.dandanplay.com/) ,已开启弹幕聚合(A/B/C 站等网站弹幕融合)

## 数据

匹配完成后对应关系会保存在**浏览器(或客户端)本地存储**中,后续播放(包括同季的其他集)会优先按照保存的匹配记录载入弹幕

## 常见弹幕加载错误/失败原因

1. 译名导致的异常: 如『よふかしのうた』 Emby 识别为《彻夜之歌》后因为弹弹 play 中为《夜曲》导致无法匹配
2. 存在多季/剧场版/OVA 等导致的异常: 如『OVERLORD』第四季若使用S[N]格式归档(如OVERLORD/S4E1.mkv或OVERLORD/S4/E1.mkv),可能出现匹配失败/错误等现象
3. 其他加载BUG: ~~鉴定为后端程序猿不会前端还要硬写JS~~,有BUG麻烦 [开个issue](https://github.com/RyoLee/emby-danmaku/issues/new/choose) THX

**首次播放时请检查当前弹幕信息是否正确匹配,若匹配错误请尝试手动匹配**


[![Stargazers over time](https://starchart.cc/Izumiko/jellyfin-danmaku.svg)](https://starchart.cc/Izumiko/jellyfin-danmaku)
