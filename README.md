# IEModeSiteList - IE 模式网站清单  

[toc]  

## 1、介绍  

**本项目维护了一份 IE 模式站点适配清单文件（适用于用于 Microsoft Edge 的 Internet Explorer 模式）**。  

**🔴 这样做的原因是**：在国内，目前仍然有相当数量的网站仍然需要使用 Internet Explorer 才能正常访问，这其中政企相关的网站占了绝大多数。微软推出的基于 Chromium 的 Microsoft Edge 浏览器加入了「Internet Explorer 模式」，可以将这些网站自动通过 Internet Explorer 在 Microsoft Edge 中打开。  

一个个将这些网站设置并切换到 Internet Explorer 模式打开是一个很繁琐且枯燥的工作，**创建一份清单文件可以一劳永逸，更加快捷方便地达到上述目的**。  

---

## 2、启用「Internet Explorer 模式」并进行预先配置

**⚠️ 注意：以下涉及到「组策略」配置相关的操作不支持家庭版授权的 Windows，因为「组策略」仅在专业版或更高版本授权中支持，如遇到此情况，请考虑将你的家庭版授权升级到专业版**。

**⚠️ 对家庭版用户的提示：如果你正在使用的是家庭版授权的 Windows，可尝试下载使用项目仓库中的 `EnableIEModeList.reg` 文件来开启相应功能，该文件未经测试，效果未知，需自行承担后果**。

### 第一步：获取策略模板 

在浏览器中打开[该地址](https://www.microsoft.com/zh-cn/edge/business/download)，并按照顺序选择对应的「频道/版本」、「版本」和「平台」。一般而言，如无特殊需要，  

- **「频道/版本」**选择**「稳定 & 受支持的最新版」**；

- **「版本」**选择**当前频道下的最新版本**；  

- **「平台」**选择**「Windows 64 位」或「Windows 32 位」**，**根据你当前使用的系统决定**。  

[![2F45DA.png](https://z3.ax1x.com/2021/05/28/2F45DA.png)](https://imgtu.com/i/2F45DA)  

选择好并确认无误后，单击下方的「获取政策文件」下载对应的组策略模板「MicrosoftEdgePolicyTemplates.cab」。  

**下载到的是一个以 `.cab` 为后缀名的文件，对其进行解压，解压后是一个 `MicrosoftEdgePolicyTemplates.zip` 压缩包，再次对这个 zip 包进行解压，直到所有文件被完全解压完毕即可**。  

### 第二步：打开 Internet Explorer 模式  

打开 Microsoft Edge，转到「设置 - 默认浏览器」，将「允许在 Internet Explorer 模式下重新加载网站」这一项勾选为启用状态，若要求重新启动 Microsoft Edge，请重新启动。  

[![2F4XvQ.png](https://z3.ax1x.com/2021/05/28/2F4XvQ.png)](https://imgtu.com/i/2F4XvQ)  

### 第三步：添加组策略模板  

转到第一步中解压缩好的组策略模板根目录，打开 `windows` 文件夹，再打开 `admx` 文件夹，该文件夹下应该如图所示：  

[![2FIg6e.png](https://z3.ax1x.com/2021/05/28/2FIg6e.png)](https://imgtu.com/i/2FIg6e)  

[![2FI5kt.png](https://z3.ax1x.com/2021/05/28/2FI5kt.png)](https://imgtu.com/i/2FI5kt)  

将上图中**红框标注的文件/文件夹中的内容**复制到 `%SYSTEMDRIVE%\Windows\PolicyDefinitions`（一般来说是 `C:\Windows\PolicyDefinitions`）文件夹中。具体是：  

- `admx` 根目录下的 `msedge.admx`、`msedgeupdate.admx`和`msedgewebview2.admx` 这三个文件，直接复制到`%SYSTEMDRIVE%\Windows\PolicyDefinitions` 根目录下；  

- `admx\zh-CN` 文件夹中的 `msedge.adml`、`msedgeupdate.adml`和`msedgewebview2.adml` 这三个文件，复制到 `%SYSTEMDRIVE%\Windows\PolicyDefinitions\zh-CN`目录下；

- `admx\en-US` 文件夹中的 `msedge.adml`、`msedgeupdate.adml`和`msedgewebview2.adml` 这三个文件，复制到 `%SYSTEMDRIVE%\Windows\PolicyDefinitions\en-US`目录下；  

复制完成后打开组策略管理器，就可以找到与 Microsoft Edge 有关的组策略模板了。  

[![2FTqds.png](https://z3.ax1x.com/2021/05/28/2FTqds.png)](https://imgtu.com/i/2FTqds)  

### 第四步：配置组策略  

打开组策略管理器，转到「计算机配置 - 管理模板 - Microsoft Edge」。找到并配置以下项目：  

- **允许访问 Enterprise Mode Site List Manager 工具**：将状态配置为「已启用」；
- **配置 Internet Explorer 集成**：将状态配置为「已启用」，选项配置为「Internet Explorer 模式」；
- **配置企业模式站点列表**：将状态配置为「已启用」，选项配置为「https://cdn.jsdelivr.net/gh/WitherZuo/IEModeSiteList@master/IEModeWebsiteList.xml」；
- **允许 Internet Explorer 模式测试**：将状态配置为「已禁用」或「未配置」。

修改完成后，**重新启动 Microsoft Edge**。在浏览器中访问 `edge://compat` ，转到「企业模式站点列表」，在右侧界面中单击「强制更新」按钮，就会从指定地址获取新的站点列表。   

[![2FHwjO.png](https://z3.ax1x.com/2021/05/28/2FHwjO.png)](https://imgtu.com/i/2FHwjO)  

### 第五步：其它检查

在按照上述步骤完成配置后，Microsoft Edge 应该具有如下变化：  

- **「设置」**页面顶部会出现**「你的浏览器由你的组织进行管理」的横幅**；  
- 单击**三点菜单**后，在**最底部会出现「由你的组织管理」字样**；
- 在**三点菜单中的「更多工具」下**，会**出现「在 Internet Explorer 模式下重新加载」或「在 Internet Explorer 模式下刷新选项卡」**；
- **「Microsoft Edge 兼容性」页面（`edge://compat`）**中会**出现「企业网站列表管理器」一项**。  

现在你可以访问列表中的网站，或是在已打开的选项卡中尝试切换 Internet Explorer 模式，检查是否按照预期工作。  

---

## 3、贡献本项目  

你也可以对本项目进行贡献，添加更多需要 Internet Explorer 模式才能正常访问的网站网址。可通过给本项目提交 Issue 的方式请求添加尚未在列表中的网站。  

---

## 4、参考链接

[1] [微软：什么是 Internet Explorer （IE） 模式？]([什么是 Internet Explorer 模式？ | Microsoft Docs](https://docs.microsoft.com/zh-cn/deployedge/edge-ie-mode))  

[2] [Add single sites to the Enterprise Mode site list using the Enterprise Mode Site List Manager (schema v.2)]([Add sites to the Enterprise Mode site list using the Enterprise Mode Site List Manager (schema v.2) (Internet Explorer 11 for IT Pros) - Internet Explorer | Microsoft Docs](https://docs.microsoft.com/en-us/internet-explorer/ie11-deploy-guide/add-single-sites-to-enterprise-mode-site-list-using-the-version-2-enterprise-mode-tool))  

[3] [微软：IE 模式疑难解答和常见问题解答]([IE 模式疑难解答和常见问题解答 | Microsoft Docs](https://docs.microsoft.com/zh-cn/deployedge/edge-ie-mode-faq))  

[4] [微软：在 Windows 上配置 Microsoft Edge 策略设置]([配置适用于 Windows 的 Microsoft Edge | Microsoft Docs](https://docs.microsoft.com/zh-cn/deployedge/configure-microsoft-edge))  

[5] [微软：The future of Internet Explorer on Windows 10 is in Microsoft Edge]([The future of Internet Explorer on Windows 10 is in Microsoft Edge | Windows Experience Blog](https://blogs.windows.com/windowsexperience/2021/05/19/the-future-of-internet-explorer-on-windows-10-is-in-microsoft-edge/))  

