自定义banner

* 基于Viewwpager,将getcount设置到integer.max
* realcount 真实数量 ,取余对应
* 自动滚动用Handler postdelay
* 暂停用标记 ,在ontouchlistener的 move中暂停,在acton_up中继续
* 