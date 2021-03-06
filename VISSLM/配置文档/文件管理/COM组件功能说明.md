#COM组件转换Office文件说明
##功能说明
启用COM组件转换office文件需要在平台【系统管理】-【站点设置】-【文件管理】中进行配置，三个文件转换配置分别表示word、excel、visio文件格式转换使用的插件，默认全部使用内置插件进行转换，如果某种office文件需要使用COM转换，把对应的转换插件切换到COM组件即可。com组件转换具体影响的功能见下表：

|配置|前置需求|影响功能
|---|---|---|
|Wword转换启用COM组件|1.服务器必须安装Microsoft Word<br/>2.服务器正确配置Word COM组件|1.word文档预览：IE或不支持PDF文件的浏览器中Word文档被转换为html网页进行浏览；Chrome等支持PDF文件的浏览器被转换为PDF预览，此时需要服务器安装的Word 2010或更高，否则会自动使用内置插件进行转换。<br/>2.导入doc格式Word文档：需开启允许导入doc格式文档的配置，此时会使用COM组件把doc格式文档转换为docx格式|
|Excel转换启用COM组件|1.服务器必须安装Microsoft Excel<br/>2.服务器正确配置Excel COM组件|1.Excel文档预览：IE或不支持PDF文件的浏览器中Excel文档被转换为html网页进行浏览；Chrome等支持PDF文件的浏览器被转换为PDF预览，此时需要服务器安装Excel 2010或更高版本，否则会自动使用内置插件进行转换。|
|Visio转换启用COM组件|1.服务器必须安装Microsoft Visio<br/>2.服务器正确配置Visio COM组件|1.富文本插入visio文件或本地编辑visio文件后自动生成visio预览图<br/>2.visio文件扩展名是.vsdx等2013及以上版本支持的格式时，服务器需安装2013及以上版本的visio软件，否则无法支持使用COM组件进行预览图生成功能，自动切换为内置插件|
##注意事项
1.转换插件选择使用COM组件时，会验证当前服务器COM组件是否可用，验证成功后才可以启用。<br/>
2.当COM组件不可用时请检查对应office软件是否已经安装并激活，COM组件权限配置是否正确，检查完成后重试。<br/>
3.注意服务器安装的各Office软件是否支持上传或预览的文档版本，如果版本过低，不能支持，会自动切换为内置插件提供相应功能。
##COM权限配置

###步骤
（1）打开开始菜单的运行对话框，输入dcomcnfg命令，确定，这时会弹出组件服务窗口<br/>
（2）展开计算机-〉我的电脑-〉DCOM配置，找到Microsoft Excel应用程序节点(配置word寻找Microsoft Word 97-2003文档，配置visio寻找Microsoft Visio 2003-2010绘图)<br/>
（3）单击右键-〉属性，选中“安全”选项，在下面三个项目都选择“自定义”，并单击编辑按钮<br/>
（4）在启动权限对话框中点击添加按钮，添加"NETWORK Service"(或"Everyone")用户并赋予最大权限<br/>
（5） 选择”身份标识”,再选择”交互式用户”即可
###注意
1、某些版本的某些office程序（如Word2016）在按照上述配置后使用COM组件仍会有问题，此时将步骤（5）的身份标识选择“下列用户”，然后填写windows用户和密码<br/>
2、有时在配置完成后可能不会立即生效，建议每次配置后重启机器<br/>
3、如果一台机器上曾经反复安装过不同版本的office，可能会出现根据名称找不到对应COM组件配置，此时程序组件名称变成了ID，可根据ID进行查找，Word程序ID为：{00020906-0000-0000-C000-000000000046},Excel程序ID为：{00020812-0000-0000-C000-000000000046}，Visio程序ID为：{00021A14-0000-0000-C000-000000000046}