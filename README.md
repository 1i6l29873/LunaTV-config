# MoonTV/LunaTV 配置编辑器
https://hafrey1.github.io/LunaTV-config  

# 加速
https://gh-proxy.com/
--- 

##  MoonTV/LunaTV配置
订阅使用：复制下面链接  

👉 Base58编码订阅链接[精简版🎬源链接](https://raw.githubusercontent.com/hafrey1/LunaTV-config/refs/heads/main/jin18.txt)    （推荐使用自己部署的代理）精简版禁18源

```bash
https://pz.v88.qzz.io?format=2&source=jin18
```
```bash
https://raw.githubusercontent.com/hafrey1/LunaTV-config/refs/heads/main/jin18.txt
```
👉 Base58编码订阅链接[精简版🎬+🔞源链接](https://raw.githubusercontent.com/hafrey1/LunaTV-config/refs/heads/main/jingjian.txt) （推荐使用自己部署的代理）精简版剔除无搜索结果和污染搜索结果源                             
```bash
https://pz.v88.qzz.io?format=2&source=jingjian
```
```bash
https://raw.githubusercontent.com/hafrey1/LunaTV-config/refs/heads/main/jingjian.txt
```

👉 Base58编码订阅链接[完整版🎬+🔞源链接](https://raw.githubusercontent.com/hafrey1/LunaTV-config/refs/heads/main/LunaTV-config.txt) （推荐使用自己部署的代理）                          
```bash
https://pz.v88.qzz.io?format=2&source=full
```
```bash
https://raw.githubusercontent.com/hafrey1/LunaTV-config/refs/heads/main/LunaTV-config.txt
```

--- 

# 🌐 CORSAPI（API 代理 & JSON 订阅器）

这是一个基于 **Cloudflare Workers** 的中转代理 + JSON 配置前缀替换工具。

支持将 API 请求通过 Worker 转发，并自动为 JSON 配置中的 `api` 字段添加/替换前缀。

同时支持生成 **Base58 编码的订阅格式**，并提供**多种配置源选择**，方便在外部应用中快速使用。

---

<details>
  
<summary>✨ 功能特性</summary>
  
# 

### 1. 通用 API 代理

使用 `?url=` 参数转发任意 API 请求

**示例：**

```
https://<你的域名>/?url=https://ikunzyapi.com/api.php/provide/vod/
```

### 2. 多配置源支持

使用 `?source=` 参数选择不同的资源配置：

- **`source=jin18`** - 精简版（31个资源，仅普通内容）
- **`source=jingjian`** - 精简+成人版（61个资源）
- **`source=full`** - 完整版（88个资源，**默认**）

### 3. 统一的 format 参数

使用 `?format=` 参数控制输出格式

- **`format=0`** 或 **`format=raw`** - 原始 JSON
- **`format=1`** 或 **`format=proxy`** - 添加代理前缀的 JSON
- **`format=2`** 或 **`format=base58`** - 原始 JSON 的 Base58 编码
- **`format=3`** 或 **`format=proxy-base58`** - 代理前缀 JSON 的 Base58 编码

--- 

</details>

<details>
  
<summary>🚀 部署方法</summary>
  
#   

🌐 部署到 Cloudflare Workers

1. 登录 [Cloudflare Dashboard](https://dash.cloudflare.com)。
2. 进入 Workers & Pages → 创建应用程序（Create Application） → Workers → 从 Hello World! 开始 → 项目命名 → 部署 → 编辑代码。
3. 将项目中的 _worker.js 文件内容复制到在线编辑器中。
4. 点击 保存并部署（Save and Deploy） 完成上线。
5. （可选）若项目使用 KV 存储：
- 存储和数据库 → Workers KV → Ceate instance  → 命名空间名称（KV Namespaces） 创建一个新的命名空间。
- 命名空间名称可自定义，例如：MyKVNamespace。
- 在 Worker设置 绑定 → 添加绑定 → KV命名空间 → 添加绑定 → 变量名为：CONFIG_KV → 创建的KV命名空间 → 添加绑定 。
6. 绑定自定义域名：打开 Worker 设置 → Triggers(域和路由) → 添加 → Custom Domains(自定义域名)，添加你的域名并保存。

📦 部署到 Cloudflare Pages

1. 登录 [Cloudflare Dashboard](https://dash.cloudflare.com)。
2. 下载仓库中的 _worker.js 文件。
3. 在本地新建一个空文件夹（名称随意），将 _worker.js 放入其中。
4. 前往 Workers & Pages → 创建应用程序（Create Application） → Pages → 上传资产（开始使用） → 项目命名 → 创建项目 → 从计算机中选择 → 上传文件夹 → 选择新建的文件 → 部署站点（Deploy Site）。
5. （可选）如需使用 KV：
- 存储和数据库 → Workers KV → Ceate instance  → 命名空间名称（KV Namespaces） 创建一个KV命名空间。
- 新建命名空间（名称随意），绑定变量名为：CONFIG_KV。
- 部署完成后，前往 Pages 控制台 → 设置 → 绑定（Bindings） → 添加 → KV 命名空间  →  变量名为：CONFIG_KV → 选择创建的KV空间 → 保存。
- 保存后返回 “部署” 选项卡。
8. 点击 创建新部署（Create New Deployment），重新上传文件并点击 保存并部署 即可。

- 部署完成后，你就拥有了自己的 API 代理与订阅转换服务！

---   

</details>

<details>
<summary>🔗 使用示例</summary>
  
#  

假设你的 Worker 部署在：[`https://api.example.workers.dev`](https://api.example.workers.dev)

### 示例 1：代理任意 API

```
https://api.example.workers.dev/?url=https://ikunzyapi.com/api.php/provide/vod/
```

### 示例 2：获取原始 JSON 配置（精简+成人版）

```jsx
https://api.example.workers.dev/?format=0&source=jingjian
```

### 示例 3：获取代理前缀的 JSON 配置（精简+成人版）

```jsx
https://api.example.workers.dev/?format=1&source=jingjian
```

### 示例 4：获取原始 Base58 编码（精简+成人版）

```jsx
https://api.example.workers.dev/?format=2&source=jingjian
```

### 示例 5：获取代理前缀的 Base58 编码订阅（精简+成人版）

```jsx
https://api.example.workers.dev/?format=3&source=jingjian
```

### 示例 6：自定义代理前缀

```jsx
https://api.example.workers.dev/?format=1&source=full&prefix=https://my-proxy.com/?url=
```

---   
  
</details>

<details>
<summary>🛠️ 参数说明</summary>
  
# 
  
| 参数     | 说明             | 可选值                          | 示例         |        
| -------- | ---------------- | ------------------------------- | ------------ |
| `url`    | 代理任意 API 请求 | 任意有效 URL                     | `?url=https://...` |
| `format` | 配置模式         | `format=0 或 raw - 原始 JSON` <br> `format=1 或 proxy - 添加代理前缀` <br> `format=2 或 base58 - 原始 Base58` <br> `format=3 或 proxy-base58 - 代理 Base58` | `?format=0` |
| `source` | 配置源选择       | `source=jin18` - 精简版 <br> `source=jingjian` - 精简+成人 <br> `source=full` - 完整版） | `?source=jin18` |
| `prefix` | 自定义代理前缀   | 任意代理地址                      | `?prefix=https://.../?url=` |
| `errors&limit=10` | 查看错误日志 | `errors&limit=10`                 | `https://<你的域名>?errors&limit=10` |

---  

## 📦 配置源对比

| 配置源 | 资源数量 | 包含成人内容 | 适用场景 |
| --- | --- | --- | --- |
| **jin18** | 31个 | ❌ 否 | 家庭使用、轻量级应用 |
| **jingjian** | 61个 | ✅ 是 | 个人使用、中等需求 |
| **full** | 88个 | ✅ 是 | 完整功能、最大兼容性 |


🧩 **前缀替换逻辑**  
- 若 JSON 中的 `api` 字段已包含旧前缀（`?url=`），系统会自动去除旧前缀并替换为新的代理前缀。  
- 可自定义代理路径，方便接入私有 API 或多 Worker 配置。
  
---   
  
</details>

<details>
<summary> 📋 完整订阅链接模板</summary>
  
# 

将 `\<你的域名\>` 替换为你的实际 Worker 地址：

### 精简版（jin18）

```jsx
# 原始 JSON
https://<你的域名>/?format=0&source=jin18

# 带代理前缀的 JSON
https://<你的域名>/?format=1&source=jin18

# 原始 Base58 编码
https://<你的域名>/?format=2&source=jin18

# 代理 Base58 编码（推荐用于订阅）
https://<你的域名>/?format=3&source=jin18
```

### 精简+成人版（jingjian）

```jsx
# 原始 JSON
https://<你的域名>/?format=0&source=jingjian

# 带代理前缀的 JSON
https://<你的域名>/?format=1&source=jingjian

# 原始 Base58 编码
https://<你的域名>/?format=2&source=jingjian

# 代理 Base58 编码（推荐用于订阅）
https://<你的域名>/?format=3&source=jingjian
```

### 完整版（full，默认）

```jsx
# 原始 JSON
https://<你的域名>/?format=0&source=full

# 带代理前缀的 JSON
https://<你的域名>/?format=1&source=full

# 原始 Base58 编码
https://<你的域名>/?format=2&source=full

# 代理 Base58 编码（推荐用于订阅）
https://<你的域名>/?format=3&source=full
```

---   

</details>

<details>
<summary>📌 注意事项</summary>
  
# 
  
- **Workers 免费额度**：每天 10 万次请求，适合轻量使用。超出后需升级付费套餐。
- **代理替换逻辑**：如果 JSON 中 `api` 字段已包含 `?url=` 前缀，会先去掉旧前缀，再加上新前缀。
- **Base58 输出**：适合直接作为订阅链接在支持该格式的客户端中使用。
- **配置源更新**：配置源来自 GitHub，内容会定期更新。Worker 会缓存 7200 秒（2小时）。
- **超时设置**：默认请求超时时间为 9 秒，超时后会返回错误信息。
- **CORS 支持**：已启用完整的 CORS 支持，可直接在前端应用中调用。

---   
  
</details>

<details>
<summary>🔧 高级配置</summary>
  
# 

### 修改配置源地址

在 `worker.js` 中找到 `JSON_SOURCES` 对象并修改：

```jsx
const JSON_SOURCES = {
  'jin18': 'https://raw.githubusercontent.com/your-repo/jin18.json',
  'jingjian': 'https://raw.githubusercontent.com/your-repo/jingjian.json',
  'full': 'https://raw.githubusercontent.com/your-repo/full.json'
}
```

### 修改超时时间

找到以下代码并修改超时毫秒数：

```jsx
const timeoutId = setTimeout(() => controller.abort(), 9000) // 改为其他值
```

### 添加访问日志

可以在代码中添加日志记录：

```jsx
console.log(`Request from: ${request.headers.get('cf-connecting-ip')}`)
```

</details>

---

## 🆕 更新内容

- 📄 **Luna-TV配置编辑器**：专业的 JSON 配置文件可视化编辑器。  
- 🔍 **自动检测API状态**：每 1 小时检测一次 API 可用性，并记录最近 100 次测试报告。  
- 🧩 **源名称前添加图标**：源名称前添加图标，方便区分。  
- 🌐 **被墙资源自动中转**：为受限 API 提供 CF Worker 中转能力。  
- 📄 **添加_comment参数**：为异常源添加_comment参数以方便维护,不影响正常使用!(2025.12.06)

---   

## 🧪 测试与示例

### ✅ 使用中转API测试
- 通过 CORSAPI 转发后，大幅提升视频源可用率。  
- 可“复活”原本无法访问的资源。  

### ⚙️ 精简版源更新
- 去除污染源与无搜索结果源（如 🎬虎牙、🔞丝袜、🔞色猫）。  
- 精简后共 **57 个可用源**，在中转代理下全部可访问。  
<details>
<summary>示例</summary>
<img width="1025" height="486" alt="61" src="https://github.com/user-attachments/assets/81c80108-7c03-4583-87ab-b7b57cdfd3bd" />
  
  
</details>

---   
  
# IPV4/IPV6 TVBOX 电视直播点播源收集

# 目录

- [直播源](https://github.com/ngo5/IPTV?tab=readme-ov-file#直播源 "直播源")
- [点播源](https://github.com/ngo5/IPTV?tab=readme-ov-file#点播源 "点播源")
- [EPG](https://github.com/ngo5/IPTV?tab=readme-ov-file#epg)
  * [112114](https://github.com/ngo5/IPTV?tab=readme-ov-file#112114 "112114")
  * [ERW](https://github.com/ngo5/IPTV?tab=readme-ov-file#ERW "ERW")
- [推荐软件](https://github.com/ngo5/IPTV?tab=readme-ov-file#推荐软件 "推荐软件")
  * [空壳软件](https://github.com/ngo5/IPTV?tab=readme-ov-file#空壳软件 "空壳软件")
  * [自带源软件](https://github.com/ngo5/IPTV?tab=readme-ov-file#自带源软件 "自带源软件")
  * [电视浏览器](https://github.com/ngo5/IPTV?tab=readme-ov-file#电视浏览器 "电视浏览器")
- [GitHub镜像](https://github.com/ngo5/IPTV?tab=readme-ov-file#GitHub镜像 "GitHub镜像")
- [官方电视直播](https://github.com/ngo5/IPTV?tab=readme-ov-file#官方电视直播 "官方电视直播")
- [第三方电视直播](https://github.com/ngo5/IPTV?tab=readme-ov-file#第三方电视直播 "第三方电视直播")

------------

# 直播源

|名称|地址|类型|EPG|台标|
| ------------ | ------------ | ------------ | ------------ |------------ |
|[YanG-1989](https://yang-1989.eu.org/)|https://tv.iill.top/m3u/Gather|IPV4|✔️|✔️|
|[vbskycn](https://github.com/vbskycn/iptv)|https://live.zbds.org/tv/iptv6.m3u|IPV6|✔️|✔️|
|[vbskycn](https://github.com/vbskycn/iptv)|https://live.zbds.org/tv/iptv4.m3u|IPV4|✔️|✔️|
|[Guovin](https://github.com/Guovin/iptv-api)|https://raw.githubusercontent.com/Guovin/iptv-api/gd/output/ipv6/result.m3u|IPV6|✔️|✔️|
|[Guovin](https://github.com/Guovin/iptv-api)|https://raw.githubusercontent.com/Guovin/iptv-api/gd/output/ipv4/result.m3u|IPV4|✔️|✔️|
|[fanmingming](https://github.com/fanmingming/live "fanmingming")|https://live.fanmingming.cn/tv/m3u/ipv6.m3u|IPV6|✔️|✔️|
|[YueChan](https://github.com/YueChan/Live "YueChan")|https://raw.githubusercontent.com/YueChan/Live/refs/heads/main/IPTV.m3u|IPV4|❌|✔️|
|[Kimentanm](https://github.com/Kimentanm/aptv "Kimentanm")|https://raw.githubusercontent.com/Kimentanm/aptv/master/m3u/iptv.m3u|IPV4|✔️|❌|
|[BurningC4](https://github.com/BurningC4/Chinese-IPTV "BurningC4")|https://raw.githubusercontent.com/BurningC4/Chinese-IPTV/master/TV-IPV4.m3u|IPV4|❌|❌|
|[zwc456baby](https://github.com/zwc456baby/iptv_alive)|https://raw.githubusercontent.com/zwc456baby/iptv_alive/refs/heads/master/live.m3u|IPV4|✔️|✔️|
|[ChinaIPTV](https://github.com/hujingguang/ChinaIPTV)|https://raw.githubusercontent.com/hujingguang/ChinaIPTV/main/cnTV_AutoUpdate.m3u8|IPV4|❌|✔️|
|[myIPTV](https://github.com/suxuang/myIPTV)|https://raw.githubusercontent.com/suxuang/myIPTV/refs/heads/main/ipv4.m3u|IPV4|✔️|✔️|
|[myIPTV](https://github.com/suxuang/myIPTV)|https://raw.githubusercontent.com/suxuang/myIPTV/refs/heads/main/ipv6.m3u|IPV6|✔️|✔️|
|[传说引导页](https://oooo.cc.ua/)|http://tttttt.tttttttttt.top/jk.txt|IPV4|❌|❌|
|[iptv-sources](https://m3u.ibert.me/ "iptv-sources") |https://m3u.ibert.me/fmml_ipv6.m3u|IPV6|✔️|✔️|
|~~[joevess](https://github.com/joevess/IPTV)~~|https://raw.githubusercontent.com/joevess/IPTV/main/m3u/iptv.m3u|IPV4|❌|✔️|
|~~[Ftindy](https://github.com/Ftindy/IPTV-URL "Ftindy")~~|https://raw.githubusercontent.com/Ftindy/IPTV-URL/main/IPV6.m3u|IPV4|✔️|✔️|
|~~[AKTV](https://t.me/MYOKKTV)~~|https://aktv.space/live.m3u|IPV4|✔️|❌|

直播源有人卡有人不卡都是正常的，请测试后选择适合自己地区的直播源。20250115突然大部分IPV6直播源只能本省看，好多项目IPV6源也替换成IPV4源，现在看直播可试试“自带源软件”下几个软件。也可以先输入点播源，这样会自动填写点播源自带的直播源。

------------

其他直播源

- [iptv共享系统](https://gyssi.link/login.html)（TG获取密钥，稳定服务收费）
- [epg.pw免费电视节目表](https://epg.pw/test_channel_page.html?lang=zh-hans)
- [Pixman](https://pixman.io/)（普通人别折腾）
- ~~[stream link](https://www.stream-link.org/)（資源不支持中國大陸使用）~~

IPV6是否开启查询：https://testipv6.com

直播源检测有效性：https://github.com/zhimin-dev/iptv-checker

------------

# 点播源

|名称|地址|类型|
| ------------ | ------------ | ------------ |
|OK猫开发|http://ok213.top/tv|源|
|[饭太硬](https://www.饭太硬.com/ "饭太硬")|http://www.饭太硬.com/tv|源|
|[liucn](https://raw.liucn.cc/box/ "liucn")|https://raw.liucn.cc/box/m.json|源|
|王小二|https://9280.kstore.space/wex.json|源|
|[qist](https://github.com/qist/tvbox)|https://raw.githubusercontent.com/qist/tvbox/refs/heads/master/jsm.json|源|
|[讴歌](https://tv.nxog.top/)|https://xn--xkkx-rp5imh.v.nxog.top/api.php?id=1|源|
|[高天流云](https://github.com/gaotianliuyun/gao "高天流云")|https://raw.githubusercontent.com/gaotianliuyun/gao/master/js.json|源|
|[肥猫](https://肥猫.com/)|http://肥猫.com/|源|
|盒子迷|https://盒子迷.top/禁止贩卖|源|
|[摸鱼儿](https://www.xn--v4q818bf34b.com/ "摸鱼儿")|http://我不是.摸鱼儿.com|源|
|zwc365|http://kv.zwc365.com/tv.json|源|
|唐三|http://6080.eu.org/|源导航|
|FongMi|https://fongmi.eu.org/|源导航|
|~~[APP宫殿](https://gongdian.top/)~~|https://gongdian.top/tvbox/nanfeng/api.json|源|
|~~Guovin~~|https://raw.githubusercontent.com/Guovin/iptv-api/gd/source.json|源|
|~~安卓哥~~|https://安卓哥.com|源|

点播源容易失效和遭人举报，建议关注原发布地址。付费源不可信，毕竟不是版权方。推荐饭太硬以及他主页推荐的源。这些点播源一般影视APP（OK/FM版）都能用。

[OK猫开发(OK影视)TG](https://t.me/okdespace) [饭太硬TG](https://t.me/TVBoxxoo) [王小二TG](https://t.me/wangerxiaofangniuwa) [FM影视TG](https://t.me/fongmi_release) [肥羊TG](https://t.me/feiyangofficalchannel)

------------

# EPG

## [112114](https://epg.112114.xyz/ "112114")

    https://epg.112114.xyz/pp.xml

112114无法打开试试镜像：

    https://live.fanmingming.com/e.xml

------------

    https://live.fanmingming.cn/e.xml


## [ERW](https://e.erw.cc/ "ERW")

    https://e.erw.cc/e.xml


------------

# 推荐软件

## 空壳软件

|名称|地址|备注|
| ------------ | ------------ | ------------ |
|TVBOX|https://github.com/o0HalfLife0o/TVBoxOSC/releases|Android电视|
|影视(FongMi)|https://github.com/FongMi/Release/tree/fongmi/apk|Android电视/手机|
|OK影视|https://github.com/FongMi/Release/tree/okjack/apk/release|Android电视/手机|
|OrionTV|https://github.com/zimplexing/OrionTV/releases|Android电视|
|MoonTV|https://github.com/MoonTechLab/LunaTV|需自己构建|
|TV-Multiplatform|https://github.com/Greatwallcorner/TV-Multiplatform/releases|MacOS Windows Linux|
|影视仓|https://pd.qq.com/s/208da3cbs|Android电视/手机|
|TiviMate|https://tivimate.com/|Android电视|
|天光云影|https://github.com/mytv-android/mytv-android|Android电视|
|ZyPlayer|https://github.com/Hiram-Wong/ZyPlayer/releases|MacOS Windows Linux|
|M3U IPTV|https://m3u-ip.tv/|Android电视|
|APTV|https://apps.apple.com/cn/app/aptv/id1630403500|iOS|
|CMSPlayer|https://apps.apple.com/us/app/cmsplayer/id6450680262|美区iOS|
|XPTV|https://apps.apple.com/us/app/xptv/id6459409368|美区iOS|
|SteveWatch|https://apps.apple.com/us/app/stevewatch/id6478312533|美区iOS|
|Kodi|https://kodi.tv/|全平台|
|Potplayer|https://potplayer.tv/|Windows|
|IPTV Player|https://iptvplayer.stream|Web|
|~~[ZY Player](https://zyplayer.fun/)~~|https://github.com/Hunlongyu/ZY-Player|Windows/Mac/Linux|
|~~[ZY Player](https://zyplayer.fun/)~~|https://github.com/cuiocean/ZY-Player-APP|Android/iOS|

------------

TVBOX、影视和影视仓关系图：![](https://img.chkaja.com/e1f671cdbc3c0900.png)

TVBOX直播没有台标没有节目单，影视APP有。TiviMate不能扫码输入源，另外自动更新源和节目单需要付费解锁高级版。Kodi需要安装后设置中文，IPTV插件安装需要科学上网。TiviMate、Kodi和iOS的软件只能看直播。

## 自带源软件

电视直播 安卓电视APP

|名称|地址|备注|
| ------------ | ------------ | ------------ |
|油桃TV|https://www.utao.tv/|影视和直播|
|电视浏览器|https://github.com/Eanya-Tonic/CCTV_Viewer/releases|官方源|
|WebView 电视|https://github.com/hxh19950701/WebViewTvLive/releases|官方源|
|大吉电视|https://www.dajitv.com/dajitv-app/|免费受限|
|GD影视|https://www.gongdian.top/?p=4761|OK影视内置源|
|影用仓库|https://wmdz.com/|电视APP合集|
|~~OurTV~~|https://github.com/andandroidor/ourtv/releases|有广告但不影响观看|
|~~我的电视~~|https://github.com/yaoxieyoulei/mytv-android/releases|可配置源|
|~~我的电视~~|https://github.com/lizongying/my-tv/releases|少量台|
|~~我的电视·一~~|https://github.com/lizongying/my-tv-1/releases|可配置源|
|~~小微直播~~|http://www.xiaoweizhibo.net/mobile.html|第三方|
|~~我的电视·〇~~|https://github.com/lizongying/my-tv-0/releases|内置源|
|~~小飞电视~~|https://y977.com/tv/|天光云影内置源|


也可以用影视APP只设置直播源再设置打开软件启动直播。原版“我的电视”是lizongying开发，已经停更。202412021左右，接手版“我的电视”已删库，范明明.com域名被墙。

## 电视浏览器

|名称|地址|备注|
| ------------ | ------------ | ------------ |
|BrowseHere|[v6.44.011](https://tcl-img.b-cdn.net/BrowseHere/APK/release/ape_6.44.011_4f72312d_221221_gp_BrowseHere.apk)|官方|
|TV Bro|https://github.com/truefedex/tv-bro/releases|开源|

------------


# GitHub镜像
- https://ghfast.top/
- https://gh-proxy.com/

在国内网络无法打开GitHub相关地址时候使用，使用方法是在地址前加上面其中一个链接。举例：https://gh-proxy.com/https://raw.githubusercontent.com/fanmingming/live/main/tv/m3u/ipv6.m3u

解决无法打开GitHub还有一种方法是更换DNS。DNS合集：https://dns.iui.im/ DNS测速：https://ping.sx/ping

------------

# 官方电视直播

- 央视网：https://tv.cctv.com/live/
- 央视影音（移动/桌面版）：https://app.cctv.com/
- 央视频：https://www.yangshipin.cn/tv/home
- 广东荔枝网：https://gdtv.cn/tvChannelDetail/51
- 江苏荔枝网：https://live.jstv.com/
- 广西网络广播电视台：https://tv.gxtv.cn/
- 芒果TV：https://live.mgtv.com/
- 新蓝网・浙江网台：https://www.cztv.com/liveTV
- 官方APP等等
- 谷歌搜索：地方+电视直播
- 官方直播地址搜索：https://iptv-org.github.io/
- IPTV源搜索：https://tonkiang.us/ http://www.foodieguide.com/iptvsearch/


------------


# 第三方电视直播

不推荐

- http://www.freeintertv.com/
- http://tv.haoqu99.com/
- https://345iptv.com/


---

# 免责声明

> **在使用本仓库前，请务必仔细阅读本声明。**
> 任何以任何形式访问、使用、复制、修改或分发本仓库内容的行为，均视为已阅读并同意本免责声明的全部条款。

---

## 一、定义与范围

* **本仓库**：指本 GitHub 仓库及其直接或间接相关的其他仓库。
* **维护者**：指本仓库的管理员、维护者及任何参与内容整理与分享的人员。
* **仓库内容**：指本仓库中提供的全部配置文件、源定义、代码片段、文档说明及引用的外部资源信息。

---

## 二、仓库用途说明（MoonTV / LunaTV 源配置）

1. 本仓库主要提供 **MoonTV / LunaTV 等相关项目的源配置、订阅定义或配置示例**，内容均整理自互联网公开信息。
2. 本仓库内容 **仅用于学习、测试与技术研究目的**，包括但不限于配置格式研究、源聚合方式分析及客户端兼容性测试。
3. **本仓库不存储、不托管、不分发任何音视频文件、媒体流或受版权保护的内容**，亦不提供任何形式的媒体服务。
4. 除非另有明确书面声明，本仓库 **不授予任何商业使用许可**。
5. 严禁将本仓库内容用于任何违反法律法规、版权规则或所在司法辖区政策的用途。

---

## 三、无任何担保声明

本仓库及其内容均以 **“现状（AS IS）”** 方式提供，维护者不作出任何形式的明示或暗示担保，包括但不限于：

* 合法性
* 准确性
* 完整性
* 可用性
* 适用于特定目的

使用本仓库内容所产生的一切风险均由使用者自行承担。

---

## 四、责任限制

1. 因使用、误用、修改或分发本仓库内容而导致的任何直接或间接损失，包括但不限于数据丢失、系统故障、服务中断、法律风险等，维护者概不负责。
2. 用户在使用本仓库内容过程中，如违反其所在国家或地区的法律法规，所产生的一切法律责任均由用户自行承担，与本仓库及维护者无关。

---

## 五、第三方软件与项目声明

1. MoonTV、LunaTV 及任何在本仓库中提及的第三方软件、硬件、服务或项目，均 **与本仓库不存在任何隶属、合作、授权或背书关系**。
2. 本仓库不对任何第三方软件或服务的功能、合法性或可用性作出保证。
3. 因使用第三方软件或服务所产生的一切后果，均由使用者自行承担。

---

## 六、转载与分发限制

1. 未经维护者明确授权，**禁止以任何形式在其他平台、网站、公众号、自媒体或镜像站点转载、发布或再分发本仓库内容**。
2. 允许在 GitHub 平台内出于学习和研究目的进行 fork，但须保留本免责声明且不得改变仓库性质或用途。
3. 通过正常开发工具获取的域名、地址或配置信息，且未涉及逆向工程或网络攻击行为的，不构成对计算机系统的非法侵入。

---

## 七、知识产权与侵权处理

1. 若任何单位或个人认为本仓库内容可能侵犯其合法权益，请及时联系维护者，并提供有效的身份证明及权属证明材料。
2. 在核实相关材料后，维护者将依法依规尽快删除或处理相关内容。

---

## 八、使用期限与删除建议

1. 本仓库内容仅供 **临时学习与研究参考**。
2. 任何关于使用时限（如 24 小时）的表述，均属于风险提示性质，并非强制性法律义务（法律另有规定的除外）。
3. 建议用户在完成学习或研究后，及时删除本仓库内容的本地副本。
4. 如对相关功能存在长期或生产环境需求，请自行独立开发实现。

---

## 九、司法辖区提示

1. 本仓库内容 **不建议在中国大陆地区使用**，尤其是在相关应用或配置可能违反当地法律法规的情形下。
2. 用户应自行评估并承担因使用本仓库内容所带来的合规与法律风险。

---

## 十、免责声明的修改与接受

1. 维护者保留在不另行通知的情况下，随时修改或补充本免责声明的权利。
2. 任何对本仓库内容的访问、使用、复制、修改或分发行为，均视为已充分阅读并接受本免责声明的全部内容。



**若您不同意本免责声明中的任何条款，请立即停止使用并删除本仓库的全部内容。**


---



## ⭐ Star History
[![Star History](https://starchart.cc/hafrey1/LunaTV-config.svg?variant=light)](https://starchart.cc/hafrey1/LunaTV-config)


















































































































































































































