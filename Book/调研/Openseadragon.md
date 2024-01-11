# openseadragon中图片添加header
```javascript
    OpenSeadragon.extend(OpenSeadragon.DziTileSource.prototype, {
        getTileAjaxHeaders: function( level, x, y ) {
            return {
                'Authorization': x,
                'Date': y,
                'x-oss-security-token': '',
                'Canonicalized Resource': ''
            };
        }
    })

    初始化要添加
    loadTilesWithAjax:  true
```