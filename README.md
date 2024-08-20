# 项目介绍

🌳🌇🏢

## 智慧园区前端3D场景

本项目是基于three.js和Vue构建的一个前端3D场景，旨在展示智慧园区的概念和特点。

## 功能特点

✨ 动态场景展示: 通过three.js创建逼真的3D场景，展示智慧园区的监测设备



## 快速开始

1. 安装依赖：

   ```
   npm install
   ```

2. 启动开发服务器：

   ```
   npm run serve
   ```

# 每个功能和文件的详细解读 📑🔍

## ZThree.js - 初始化和通用函数 🌌🔧

1. 🚀 `initThree()`: 初始化Three.js场景，包括创建场景、相机、渲染器等，并将渲染器的DOM元素添加到指定的HTML元素中。
2. 📍 `initHelper()`: 添加坐标轴辅助对象，有助于定位和调试。
3. 🎮 `initOrbitControls()`: 初始化轨道控制器，允许通过鼠标和触摸来控制相机的旋转、缩放和平移。
4. 💡 `initLight()`: 初始化灯光，设置环境光和平行光的位置和投影。
5. 📦 `loaderModel(option)`: 加载gltf或glb格式的模型文件。
6. 🔄 `iterateLoad(objFileList, onProgress, onAllLoad)`: 批量加载模型文件，并支持加载过程中和完成后的回调函数。
7. 🎯 `initRaycaster(callback, models = this.scene.children, eventName = "click")`: 初始化射线投射器，用于检测鼠标点击或触摸事件与场景中的模型的交互。
8. 🛑 `destroyRaycaster(eventName)`: 停止射线投射功能，移除事件监听器。
9. 🔫 `fireRaycaster(pointer, models)`: 发射射线并检测与模型的交互，返回交互结果。
10. 🌍 `getModelWorldPosition(model)`: 获取模型的世界坐标。
11. 🕊️ `flyTo(option)`: 控制相机以动画效果飞往指定位置和视角。
12. 🚶 `modelMove(option, obj)`: 控制模型以动画效果移动到指定位置。
13. 🎥 `render(callback)`: 渲染循环，每帧执行回调函数进行渲染。



## loaderModel.js - 模型加载和管理函数 🔄🗄️

1. 🚀 `loaderModel(app)`: 异步函数，加载模型并将其添加到场景中。
2. ❌ `destroyControlsGroupText(app, className)`: 移除指定类名的HTML元素的点击事件监听器。
3. ⚙️ `setModelDefaultMaterial(app)`: 恢复所有模型的默认材质。
4. 🧹 `destroyControlsGroup(app, className)`: 移除控制组中的模型。



## cssRender.js - 生成场景标签函数 🏷️

ps : 在本项目中,该方法并没有直接使用,而是通过在HomeView.vue中实例化后挂载到了instance方法中.

1. 🌟 `T.init`: 这个初始化函数准备CSS渲染器。它创建一个新的 `cssRender` 实例，设置大小，并将其附加到应用程序元素上。
2. ➕ `T.add`: 这个函数用于向场景添加CSS对象。它接受一个参数，该参数可以是一个对象或对象数组，并将其添加到3D场景中。
3. 🗑️ `T.removeAll`: 此函数用于从场景中删除所有CSS对象。它遍历父对象的子对象，并从场景和配置中删除所有CSS对象。





## material.js - 管理材质

如果要修改材质就直接在这里修改,其他方法使用材质时是直接引用这里暴露的材质,方便管理



## floorManage.js -管理楼层和房间的显示与操作

楼层管理中每栋楼的标签是通过查找到"楼顶"这个子模型,并在它的上方生成标签标签,而标签名是这个子模型的父模型名字,每层楼的标签也是要通过"F"关键词来查找的

1. 🚁 `loaderFloorManage`: 此函数将摄像机飞到特定位置，然后创建楼层文本标签。

2. 🏷️ `createFloorText`: 此函数在3D模型的楼层上创建文本标签。用户可以点击标签，然后摄像机将飞向该楼层，并显示楼层的详细信息。
3. 📝 `createRoomText`: 此函数在3D模型的房间中创建文本标签。当用户点击房间标签时，将触发一个事件，显示房间的详细信息。
4. 🎬 `setModelLayer`: 此函数控制楼层模型的动画移动。根据所选的楼层，模型会以动画的形式移动到合适的位置，并显示所选楼层的房间标签。





## reprocessing.js -实现一些视觉效果，包括辉光、抗锯齿和边缘高亮。(很消耗性能,慎开)

1. 🎨 **Color Management**: 关闭颜色管理。

2. 🌟 **Bloom Effect (辉光效果)**: 为场景添加一个辉光效果。这通过使用`UnrealBloomPass`来实现。辉光效果使亮部分看起来更亮，类似于光晕。

   - `bloomThreshold`: 用于确定哪些像素将被认为是辉光的一部分。
   - `bloomStrength`: 控制辉光的明亮程度。
   - `bloomRadius`: 辉光效果的半径。

   该代码还包含一些GUI代码的注释，这些代码可以允许用户动态调整辉光效果的参数，但这已经被注释掉。需要时再开启

3. 📐 **Edge Highlighting (边缘高亮)**: 通过使用`OutlinePass`，为场景中的对象添加边缘高亮效果。可以调整边缘的强度，辉光，厚度以及脉冲周期（可能是闪烁）。

   - `edgeStrength`: 控制边缘线的粗细。
   - `edgeGlow`: 控制发光的强度。
   - `edgeThickness`: 控制光晕的粗细。
   - `pulsePeriod`: 控制闪烁的频率。

   和辉光一样，这部分代码也包含注释掉的GUI部分，用于动态调整。

4. 🎥 **Compositing**: 使用`EffectComposer`将这些效果合成到最终的渲染图像中。这涉及将渲染场景传递给不同的渲染通道，并使用着色器材料将它们组合在一起。



## parkElectricity.js 电力监测的功能,水力监测也同理

1. 🚀 `loaderParkElectricity`: 此函数使摄像机飞到特定位置，然后创建电力监控。
2. 💡 `createParkElectricity`: 此函数遍历模型中的对象，并检查是否有对象与电表有关。如果有，它将检查电量是否超过460度。如果是，则会发送通知警告。此外，它还可以放大电表模型，并初始化与电表相关的射线投射。
3. 🧨 `destroyParkElectricity`: 此函数用于销毁电力监控。它会清除所选对象，隐藏工具提示，并将模型材质重置为默认状态，然后销毁射线投射。



# 数据的处理

放在了assets文件夹的mock.js中.

存储了在房间模型里每个具体业务中的子模型的名称,样式,图片,数据







# Blender建模指南 🏗️

在Blender中为网页场景进行建模时，需要特别注意模型的命名和一些细节，以确保与前端开发的良好配合。以下是一些规范和注意事项：

## 1. 命名规范 📛

模型的命名是区分楼栋，楼层，以及监测设备的关键。正确的命名不仅有助于组织，还是模型与前端开发配合中至关重要的环节。

### 楼栋 🏢

- 楼栋的命名没有特殊限制。
- 每栋楼都需要包含一个名为**楼顶**的子模型。网页场景将通过这个楼顶子模型来识别一个楼栋。
- 楼栋的名称将被用作网页上的楼层管理模块的标签名称。

### 楼层 🏬

- 楼层的名称需要以**F**结尾，例如：“1F”, “2F”。网页场景将通过这个后缀来识别楼层。

### 监测设备 📡

- 监测设备的命名在具体业务中可能变化，因此需要与前端开发团队进行沟通。
- 前端开发人员需要在`mock.js`文件中更新监测设备模型的样式，并在以`park`为前缀的文件中通过监测设备的名称遍历所有模型，然后选择要监测的模型。

## 2. 建模注意事项 🔍

### 修改器的应用 ✅

- 如果在修改器中使用了类似于阵列的功能，请记得点击“应用”按钮。这样设置才会在网页上生效。如果没有应用，效果只会在Blender内显示。

### 优化复杂模型 🛠️

- 如果引入了网络上的复杂模型资源，建议在修改器中添加简化，以减轻网页渲染的压力。
- 可以删除一些不必要的父模型，只保留具有代表性外观和形状的模型。







# 整理关于功能实现的详细过程，面向过程编程

待续。。。

