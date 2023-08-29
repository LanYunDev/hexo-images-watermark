严格遵循 [Semantic Versioning 2.0.0](http://semver.org/lang/zh-CN/) 语义化版本规范。

# 2.3.0

`2023-08-29`

提高各个依赖版本,将svg2png换为@resvg/resvg-js.修复sharp版本问题.

# 2.3.0

`2020-09-27`

-   🆕 feat :
    -   新增参数 `cache`，类型为 `boolean`。可以进行缓存配置

## 新增参数 `cache` 使用

为了兼容和不改变原来使用，默认值为：`false`

如果为`true`，第一次使用后，会在执行目录下生成 `spiritling/cache/pub/${package.name}` 的文件夹，里面将 `post/**/**.{png|jpg|gif}` 文件水印添加后放进去，用于缓存。

为了真正起效，请将这个文件一起上传到仓库。

在第二次构建时，会去进行**文件路径和名字对比**，如果不一致，则进行生成新的水印图片，并缓存，如果一致，则直接将文件读取放入到正常渲染后的路径中。

> 新功能请酌情使用

```js
/**
 * @description 判断已有渲染图片和准备渲染图片路径是否一致
 * @param {string} currentFilePath
 * @return {boolean} 一致返回true，否则返回false
 */
function IsEqual(currentFilePath) {
    const fileCachePath = path.join(process.cwd(), cachePath, currentFilePath)
    return fs.pathExistsSync(fileCachePath)
}
```

# 2.2.0

`2020-07-23`

-   🐛 fix :
    -   修复问题 [#14](https://github.com/SpiritLingPub/hexo-images-watermark/issues/14)
-   🆕 feat :
    -   新增参数 `directory` ，可以自定义配置渲染的目录

## 新增参数 `directory` 使用

渲染图片水印是在`public`生成后，所以目录指定为`public`下的目录

比如你的文章都在 `public/post` 下，你可以设置为：

```yml
watermark:
    directory:
        - posts
```

但是你的主题如果是其他，生成的文章可以是在 `public/2019`，`public/2020`这种目录下，可以设置为：

```yml
watermark:
    directory:
        - 2019
        - 2020
```

甚至如果你只想对某个文章处理水印，可以设置为：

```yml
watermark:
    directory:
        - 2019
        - 2020/07/09/example
```

# 2.1.0

`2020-07-03`

-   🧾 README 中的一些内容[1#card-41138753](https://github.com/SpiritLingPub/hexo-images-watermark/projects/1#card-41138753)
-   🆕 新增一些配置[1#card-41189622](https://github.com/SpiritLingPub/hexo-images-watermark/projects/1#card-41189622)

# 2.0.0

`2020-07-02`

-   🔥 对 1.1.x 版本进行优化，虽然兼容 1.1.x 版本，但是因为重构了代码，所以更新了大版本
-   🔥 添加动态图片处理
-   🔥 增加超限处理
