## threeJs使用笔记
 + **模型表面法向量** ： 模型表面的法向量在加载过程中已经完成计算，那么模型旋转后，对应的法向量信息也要做同样的旋转变化。
 + **图片资源跨域问题** ： 在threejs中，图片加载使用 `textureloader` ，如果图片需要跨域，要设置 `crossOrigin` 属性。*注：img元素加载过的图片存于缓存，如果textureloader加载的为缓存图片，会出现跨域异常，因此img元素也要设置 `crossOrigin` 属性。*
 + **camera + controls 的奇怪问题** ：使用 `camera.position.set(v3)` 函数会导致控制器 update() 函数异常，影响相机变化的帧率，要改变相机坐标建议使用 `camera.position.copy(v3)`。
 + **深度测试(depthTest)** ：`Material` 的 `transparent` 属性为 `true` 时，`depthTest` 的设置才会有效。
 + **释放内存(dispose)** : 模型和纹理的内存释放是会阻塞主线程的耗时操作，要谨慎使用。
 ------
