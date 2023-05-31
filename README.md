# Unity 后处理（Post-Processing）

**`关键词：`**：#post-process

### 为什么需要后处理（Post-Processing）流程

查阅Unity官方文档[Post Processing Stack v2 overview](https://docs.unity3d.com/Packages/com.unity.postprocessing@3.0/manual/index.html)可知如下解释：

> Post-processing is a generic term for a full-screen image processing effect that occurs after the camera draws the scene but before the scene is rendered on the screen. Post-processing can drastically improve the visuals of your product with little setup time.
>
> 后处理是全屏图像处理效果的总称，发生在相机绘制场景之后，场景渲染到屏幕之前。后处理可以在很短的设置时间内显着改善产品的视觉效果。

看完之后，感觉没有看一样。完全没有通俗地说明，因此，请我们的**GPT4**老师解析一下：

> Unity Post Process refers to the application of post-processing effects, which are used to improve the appearance of your game by simulating physical camera and film properties or creating stylized visuals [Source 0](https://docs.unity3d.com/Manual/PostProcessingOverview.html). These effects can be added using the Post Process Layer component and managed with the help of a Volume framework [Source 1](https://docs.unity3d.com/Packages/com.unity.postprocessing@3.0/manual/Quick-start.html).
>
> To enable post-processing in your scene, first add the `Post Process Layer` component to the Main Camera GameObject. Then, create a dedicated GameObject for each volume and add the `Post-process Volume` component to it [Source 1](https://docs.unity3d.com/Packages/com.unity.postprocessing@3.0/manual/Quick-start.html). You can add post-processing effects to the stack by clicking the "Add effect" button at the bottom of the `Post Process Volume` component and selecting the desired effect from the drop-down list [Source 1](https://docs.unity3d.com/Packages/com.unity.postprocessing@3.0/manual/Quick-start.html).
>
> For example, to add a Bloom effect:
>
> 1. Create a new GameObject and add the `Post-process Volume` component to it.
> 2. In the `Post-process Volume` component, click "Add effect" and select "Unity > Bloom" from the drop-down list.
> 3. Configure the Bloom effect properties as desired.
>
> You can also combine multiple effects, such as Bloom and Chromatic Aberration, within the same `Post-process Volume` component [Source 4](https://blog.logrocket.com/exploring-post-processing-unity/).

根据**GPT4老师**上述的解释，可知后处理就跟影视后期处理差不多，对已渲染的画面进行后期视觉的加强或特效的增添润饰。

因此，在日常的使用后处理中，其主要是为了配合游戏需要，添加适当的特效或色彩调整，从而增添画面的课观赏性。

### 如何设置后处理

后处理可分为局部后处理和全局后处理。其主要流程：

- 从**Packages Manager** 加载 **Post Processing依赖包**
- 自定义设置**Post Processing Layer**
- 添加**Post-process Layer**组件至**Camera**
- 添加**Post-peocess Volumn**组件至GameObject

----

#### 局部添加后处理（Post-Processing）

在游戏动漫里，经常会有这样的情节，主人公会碰触了某个特定的机关而进入了一个特定的环境。譬如：《加速世界》中，呼叫**”**Burst Link**“**就会进入蓝色的特定世界；又如《灼眼的夏娜》中，每次**紅世之徒**出现，主人公都会被带进 **红世**领域的特定红色空间。

![加速世界](https://cdn.staticaly.com/gh/Salmonberry/FigureBedBySalmon@master/Game/加速世界.61h343dxzd00.webp)

![fdfdf](https://cdn.staticaly.com/gh/Salmonberry/FigureBedBySalmon@master/Game/fdfdf.351xecmxs100.webp)

局部后处理，一般都是为了满足上述说的一些故事设定情节，让主人公触发了某个条件进入了特定领域空间的画面后期处理方法。

##### 从**Packages Manager** 加载 **Post Processing依赖包**

关键步骤：
- 下载**Post-processing**依赖包

![001](https://cdn.staticaly.com/gh/Salmonberry/FigureBedBySalmon@master/Game/001.68xw5m8zjlo0.webp)

##### 设置领域空间的**Collider**

为**GameObject对象**设置**Collider**的大小，**Collider**的空间范围即为局部**Post-processing**生效范围。

关键步骤：
- 为GameObject挂载**Collider组件**，并勾选为**Trigger**模式
- 设置**Collider**的大小

![collider](https://cdn.staticaly.com/gh/Salmonberry/FigureBedBySalmon@master/Game/collider.3wwl4ctzisg0.webp)

---



##### 配置屏幕后处理效果

为产生局部**Post-processing**效果的**GameObject**对象挂载**Post-process Volume**组件，并配置**Post-processing Profile**配置文件。

**Post-processing Profile**文件 用于存储用户设置的后处理效果及其设置集合的资产。它充当这些效果的容器，可以轻松地在不同的场景和相机中应用、修改和重用它们。

**Post-process Volume**组件 对于**Post-processing Profile**文件，是一个控制器开关，通过**Post-process Volume** 组件用于控制每个本地和全局**Post-process Volume**组件的优先级和混合。它允许您创建一组效果覆盖以在场景中自动混合后处理设置。对于**场景Scene**，**Post-process Volume**组件将其持有的**Post-processing Profile**文件，按需要实例化效果至场景中。

关键步骤：

- 添加**Post-process Volume**组件
- 挂载**Post-processing Profile**文件至**Post-process Volume**组件中
- Add effect
- 设置自定义的**Layer**：**PostProcessing**

###### 添加**Post-process Volume**组件 


![post-processing_volume](https://cdn.staticaly.com/gh/Salmonberry/FigureBedBySalmon@master/Game/post-processing_volume.341782b7c920.webp)

当在**Post-process Volume**组件 上点击**New**按钮生成**Post-processing Profile**文件并附加后，便可添加Unity内置的后处理特效。

###### Add effect

![post-processing_add_effect](https://cdn.staticaly.com/gh/Salmonberry/FigureBedBySalmon@master/Game/post-processing_add_effect.28dyzw2ynyf4.webp)

这里我选择添加**Color Grading**屏幕效果

![post_processing_effect_color_grading](https://cdn.staticaly.com/gh/Salmonberry/FigureBedBySalmon@master/Game/post_processing_effect_color_grading.51rjgff39gk0.webp)

![color_grading](https://cdn.staticaly.com/gh/Salmonberry/FigureBedBySalmon@master/Game/color_grading.6uo3aaiip680.webp)

###### 设置自定义的**Layer**：**PostProcessing**

![post_process_layer](https://cdn.staticaly.com/gh/Salmonberry/FigureBedBySalmon@master/Game/post_process_layer.48vnu39w9lk0.webp)


---



##### 配置Post-processing Layer

**后处理（Post-processing）**阶段的流程发生在**Camera**绘制场景之后，场景渲染到屏幕之前应用图像处理效果。

**Unity  Layer**的作用跟**Photoshop**中的图层的功能一致，将操作对象分配至不同的图层层级：

- 方便实现局部渲染处理
- 便于通过代码，对不同层级对象做物理检测的碰撞
- Layer的顺序，决定了层级对象的顺序，序号越小的越早被渲染

而**Post-process Layer**组件 的职责就是负责在将**后处理（Post-processing）**阶段所应用的图像处理效果传递给**Camera**，告诉**Camera**如何去图像处理。

关键步骤：

- 将**Post-process Layer**组件挂载至**Camera**上
- 设置**Layer为自定义的PostProcessing Layer**

![main_camera_layer](https://cdn.staticaly.com/gh/Salmonberry/FigureBedBySalmon@master/Game/main_camera_layer.6q2rq70r3000.webp)

---

##### 效果

![unity_effect](https://cdn.staticaly.com/gh/Salmonberry/FigureBedBySalmon@master/Game/unity_effect.7an4cw5zmc00.gif)

---

#### 全局添加后处理（Post-Processing）

##### 局部转全局

![post_process_volume_global](https://cdn.staticaly.com/gh/Salmonberry/FigureBedBySalmon@master/Game/post_process_volume_global.4ay035ibvo00.webp)

当将**Post-process Volume**挂载特定的**GameObject**上作为**局部后处理（Post-Processing）**时，此时可以通过设置**Post-process Volume**上的**Is Global**为**True**，将局部触发更改为默认全局效果，不需要**Player**触碰就能显示**后处理效果（Post-Processing）**。最后的效果如下：

![2023-05-30_1-35-19](https://cdn.staticaly.com/gh/Salmonberry/FigureBedBySalmon@master/Game/2023-05-30_1-35-19.a7z5n93yy8s.gif)



##### 全局设置方法

因为一旦设置**Post-process Volume**上的**Is Global**为**Ture**时，后处理效果就不需要触发**Collider**就可以全局显示了。因此，在不需要基于触发而显示的后处理效果，可以直接将相关的组件都挂载在**Camera**上。相关设置如下图所示，

![camera_global](https://cdn.staticaly.com/gh/Salmonberry/FigureBedBySalmon@master/Game/camera_global.5aaqxlqr5bs0.webp)

![2023-05-30_2-17-45](https://cdn.staticaly.com/gh/Salmonberry/FigureBedBySalmon@master/Game/2023-05-30_2-17-45.5lcjjdiyctg0.gif)

### References

----

[Using Post-Processing to improve visuals in Unity](https://www.youtube.com/watch?v=_PzYAbPpK8k&ab_channel=GameDevGuide)
[unity_post_processing_example](https://github.com/Salmonberry/unity_post_processing_example)