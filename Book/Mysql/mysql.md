* 登录系统
mysql -p123456

* mysql中如果取两个字段合并为一个字段，取不为空的字段用 COALESCE
```mysql 
SELECT ksg.*, COALESCE(ksgr.originalSize, sasgr.originalSize) AS originalSize,COALESCE(ksgr.resourceIcon, sasgr.resourceIcon) AS resourceIcon,COALESCE(ksgr.tilizeStatus, sasgr.tilizeStatus) AS tilizeStatus,FROM kl_show_goods ksg LEFT JOIN kl_show_goods_resource ksgr ON ksg.resourceId = ksgr.resourceId LEFT JOIN sys_admin_show_goods_resource sasgr ON ksg.resourceId = sasgr.resourceId WHERE ksg.userId = ? AND ksg.updateTime < ? and ksg.status = 1 and ksg.close = 1 ORDER BY ksg.updateTime DESC LIMIT ?
```
