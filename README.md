# FuxiCV-Projects
 
---
pageClass: home-page
# some data for the components

name: Fuxi CV
profile: /fuxi.png

socials:
  - title: email
    icon: "/icons/email.svg"
    link: 'mailto:yyshawn@163.com'

# cv: https://en.wikipedia.org/wiki/Harry_Potter
bio: Computer Vision Group at Netease Fuxi AI Lab
# email: yyshawn (at) 163 (dot) com
---

<ProfileSection :frontmatter="$page.frontmatter" />

## About

[网易游戏伏羲实验室](https://fuxi.163.com/)图像组致力于以AI技术赋能游戏制作和玩法交互，增强游戏沉浸感，这里列出了我们在探索AI+游戏落地中总结出的部分高价值研究课题，欢迎所有对此有兴趣的同仁与我们合作，共同推进课题落地和论文发表。

<!--

## Education & Experiences

- **Hogwarts School of Witchcraft and Wizardry** <br/>
Sept 1991 - 1997
-->
   
## Research Projects

<ProjectCard hideBorder=false>

  ### SingleView Object Reconstruct


  课题背景：

  - 通过RGB图像的物体三维重建一直都是图形图像的经典课题，但是经典的物体三维重建方法没有办法根据单视角RGB图像进行重建，而深度学习的方法对于基于单视角RGB图像的物体三维重建问题有令人激动的效果。
  
  问题定义：

  - 输入：某物体的单视角RGB图像
  - 输出：该物体对应的三维网格模型

  问题挑战：

  - 由于输入图像只有单视角，缺乏物体背部足够的信息。
  - 由于输入图像是RGB图像，缺乏物体的深度信息，对于重建问题也有一定的难度。

  评价指标：

  - 定性指标：就是主观判断重建的物体与输入图像是否相似。
  - 定量指标：包括CD（Chamfer Distance），EMD（Earth Mover’s distance ），IoU（intersection-over-union）

  数据集描述：

  - ShapeNetCore：ShapeNet数据集是一个大规模的3D CAD 模型数据集，ShapeNetCore是从ShapeNet数据集中挑选的55类，约51,300个独特的3D模型。具有干净的3D模型和手动验证的类别和对齐注释。

</ProjectCard>

<ProjectCard hideBorder=true>

  ### SingleView Face Reconstruct


  课题背景：

  - 人脸三维模型重构是当前计算机图形学热门研究方向。目前基于单张人脸图像进行三维重建的方法很多，但这些方法往往都主要关注于重建人脸形状，而忽视了人脸贴图的生成。特别是对于侧脸图像来说，如何预测一张完整的、去除光照影响的漫反射（Diffuse）贴图，是使得重建的三维人脸能够在游戏中应用的关键。此外，为了提高重建的三维人脸的真实感，还可以进一步生成法线贴图、高光贴图等相关数据。

  问题定义：

  - 输入一张玩家上传的人脸图片，人脸图片中可能含有诸多复杂因素，例如侧脸、光照、阴影、刘海和眼镜等物体的遮挡等等，目标是生成一个给定拓扑结构的三维人脸，以及对应的漫反射贴图、法线贴图等，并且贴图中要去除刘海等遮挡物。  

  问题挑战：

  - 如何生成指定拓扑结构的人脸Mesh
  - 在缺少公开数据集的条件下，如何去除复杂的光照、遮挡与自遮挡等因素，生成完整的漫反射贴图
  - （可选）为了提高生成的人脸的仿真程度，还可以生成法线贴图、高光贴图等其它数据

  评价指标：

  三维人脸重建可以从和定量两个指标进行评价：
  - 定性指标：人眼主观评价，即人眼评价重建的三维人脸和输入的图片是否相似
  - 定量指标：包括使用人脸识别网络评估两者的相似度以及Landmarks的L1 distance
  
  数据集描述：

  - 三维人脸Mesh模板，生成的人脸Mesh拓扑结构需与该模板一致
  - 人脸Mesh模板对应的贴图模板
  - 二维人脸图片数据集
  - 也可以使用目前公开的三维人脸重建相关数据集，包括Basel Face Model（BFM），  Large Scale Facial Model（LSFM）等。

</ProjectCard>

<ProjectCard hideBorder=true>

  ### Face Reenactment

  
  课题背景：

  - 换脸以及表情迁移是计算机视觉领域热门研究方向。不久前，一个deepfakes换脸引爆了知乎和朋友圈。然而表情迁移还是停留在3d程度上，我们也许可以使用生成网络把表情迁移在2d上实现。
  
  问题定义：

  - 输入：单张人脸 + 一张带有表情的人脸
  - 输出：或者带有B表情的A的人脸

  问题挑战：

  - 不同id的脸部形状可能差异较大，如何在保证模型能够处理这种输入的差异性是个值得研究的问题
  - 通过GAN生成的图片往往有arifacts，如何优化？
  - 能否在变换表情的同时，尽量保证细节（如首饰，妆容，背景等）不丢失
  - （可选）为了提高生成效果，可以加入时序信息，生成平滑的结果
  
  评价指标：

  - 人眼主观评价。
  - SSIM
  - FID
  - IS
  - 生成结果和输入的脸部相似度
  
  数据集描述：

  - faceforensics++ ，可提供检测的关键点（68 3d点 和 240 2d点两个版本）
  - VoxCeleb 1 & 2

</ProjectCard>

<ProjectCard hideBorder=true>

  ### AutoSkinning
  

  问题背景：

  - 游戏角色骨骼动画中，模型皮肤(mesh)往往通过定义骨骼(skeleton)并设定合适的关联性(skinning)后以骨骼的运动来进行驱动，其中模型绑定到骨骼上的过程是为蒙皮。业界主要通过美术同学应用绑定工具手动对所有mesh点设置权重的方式完成，往往极为繁琐耗时，对于美术风格较为相似的模型在遵守一定规范与标准的情形下，模型相似部位的骨骼权重有一定规律性，可以考虑自动蒙皮算法。
  
  问题定义：

  - 输入：模型的mesh数据(vertices/faces/normal等), 骨骼数据
  - 输出：每一个mesh vertex与目标骨骼的关联性(LBS权重)
  
  问题挑战：

  - 数据中的噪声
  - 权重的非确定性，合理的权重与该角色的动作应用相关
  - 骨骼、mesh的语义
  - 问题的建模形式
  
  数据集描述：

  - 真实游戏中积累的历史蒙皮数据(每个模型包括mesh/骨骼及相应蒙皮权重)

</ProjectCard>

<ProjectCard hideBorder=true>

  ### Face Appearance Rating
  

  课题背景：

  - 不同人对于美有着各自的标准，不同人对于同一个游戏角色有着不同的评价打分。捏脸颜值打分是帮助算法捏出符合玩家审美游戏脸的一个重要技术。
  
  问题定义：

  - 给定一个游戏内捏的脸的截图，获得评分。
  
  问题挑战：

  - 数据集缺少，以及如何定义符合大众审美的标准。

</ProjectCard>

<ProjectCard hideBorder=true>

  ### Image SuperResolution
  

  课题背景：

  - 图像分辨率是指在计算机中保存和显示一幅数字图像所具有的分辨率，也可以理解为图像的像素数。当显示设备相同时，图像分辨率越高，图像尺寸就越大，图像包含的细节信息也就越多。但是在现实世界中，由于硬件限制、网络传输等不可抗力，我们通常只能获得较低分辨率的图像，这为某些应用场景造成了诸多不便。图像超分辨是通过某种方法，提升图像分辨率的技术。在学术界，根据处理目标的不同，可分为单幅图像超分辨和多幅图像超分辨（考虑时序信息，可用于视频超分辨）。

  - 在游戏制作与后期营销的过程中，我们通常会遇到现有美术资源（低分辨率）无法满足网站或海报展示要求的问题，直接将美术资源（低分辨率）放大会造成细节模糊，而让美术人员重新创作清晰（高分辨率）的美术资源是极为耗时的。图像超分辨技术可以即时对美术资源（低分辨率）进行处理，并具有比直接放大更为清晰的图像细节。

  - 另外，图像超分辨的效率也是一项至关重要的问题。NVIDIA公司在2019年初推出了一项深度学习超级采样（Deep Learning Super-Sampling）技术，该技术基于图像超分辨，可以使显卡以较低分辨率（1080p）渲染画面，并以较高分辨率（2K或4K）进行输出与展示，并且达到抗锯齿的效果，这样就大大降低了3A大作特效全开的显卡渲染压力，提高了帧率。DLSS基于RTX显卡架构，RTX显卡具有适用于加速神经网络计算的Turing Tensor，Turing Tensor独立于CUDA Tensor，可以在不影响游戏渲染速度的前提下，实时对渲染帧进行超分辨处理。

  - 值得注意的是，通常情况下，超分辨技术是特定于任务（task-specific）的，即对于不同的任务，通常需要制定专用的超分辨技术，以达到较为理想的效果。此外，超分辨技术无法将一张模糊的图像变清晰。

  问题定义：

  - 给定一张低分辨图像，预测对应的高分辨图像。

  问题挑战：

  - 图像超分辨是一个不适定问题（ill-posed inverse problem），即对于一张低分辨图像，它可以由多种不同的高分辨图像通过同样的降采样过程得到，这使得图像的降质过程是不可逆的。

  指标评价：

  - 对于图像超分辨指标的评价，通常分为有参考指标与无参考指标两个方面：
  - 有参考指标：
   - 峰值信噪比（Peak Signal-to-Noise Ratio）：在像素维度衡量超分辨图像与高分辨图像的（均方）误差，指标通常在20~40之间，值越高表示图像越相似。
   - 结构相似度（Structural SIMilarity）：通过计算像素的均值、方差、协方差等指标，衡量超分辨图像与高分辨图像的感知误差，指标在0~1之间，值越高表示图像越相似。
  - 无参考指标：
   - Perceptual Index：由Ma score与NIQE计算得到，表示图像的“真实度”，指标在0~1之间，值越高表示图像越“真实”

  数据集描述：

  - DIV2K
  - Flickr2K 
  - OutdoorSceneTraing
  - Set5
  - Set14
  - BSDS100
  - Urban100
  - Manga109

</ProjectCard>

<ProjectCard hideBorder=true>

  ### Hair Reconstruct
  

  课题背景：

  - 3D 头发重建是图形学中的一个重要课题，对数字化人具有重要的地位。该课题还可以应用于换发型应用。目前存在3d头发重建按照输入数据分为带有深度信息的图像、单张图像和多张图像三种方法。

  问题定义：

  - 输入一张或多张含有头发的上半身图像，生成3d头发模型。最终的输出是发丝级别的数据。

  问题挑战：

  - 图像超分辨是一个不适定问题（ill-posed inverse problem），即对于一张低分辨图像，它可以由多种不同的高分辨图像通过同样的降采样过程得到，这使得图像的降质过程是不可逆的。

  指标评价：

  - 对于图像超分辨指标的评价，通常分为有参考指标与无参考指标两个方面：
  
  数据集描述：

  - [[HairNet](https://github.com/papagina/HairNet_DataSetGeneration)]

</ProjectCard>

## Engineering Projects
<ProjectCard hideBorder=true>

  ### 跨平台的计算机视觉库
  

  课题背景：

  - 现如今，计算机视觉算法在全平台（Windows、Linux、Mac、iOS和Android）的部署变得越来越常见，为了帮助算法在全平台的高效和稳定的运行，  同时也为了保证算法接入的便捷性，因此构造一个高兼容性、强拓展性、低功耗和低占用的跨平台的计算机视觉库也变得至关重要。


  问题定义：

  - 能够保证全平台（Windows、Linux、Mac、iOS和Android）的兼容性。
  - 保证该库的接口友好，方便使用者接入。
  - 具备低功耗和库占用较小的特点，保证将该库接入的模块的最终包体小且运行稳定。
  - 为了满足低占用的特性，该库只要能够满足基础的图像单元增删改功能，具体可参考opencv的core模块，同时接口设计具有较强的拓展性，方便之后模块和功能的添加。

  问题挑战：

  - 全平台的兼容性需要对全平台具有全面的理解。
  - 稳定和低功耗需要不断的完善和优化。

  指标评价：

  - 高兼容性是否满足，能够在哪些平台上运行。
  - 强拓展性是否满足，接口的设计方便后续拓展。
  - 低功耗和低占用是否满足，接入后是否能够稳定运行。

</ProjectCard>

<ProjectCard hideBorder=true>

  ### 动作风格化
  

  课题背景：

  - 人物动作是视频游戏的核心表达能力之一。传统的游戏设计过程中，往往采用专业演员动作捕捉或动画师调节动画曲线的方式，获得精细的人物动作表现。随着游戏世界观、故事线不管丰富扩展，不同角色的动作数据需要投入大量的人力进行生产。动作风格化算法在现有动作数据基础上，生成针对不同角色风格、人设的多样化动作表现，提高动作数据的生产效率。


  问题定义：

  - 通过基准动作数据与风格化动作数据在编码空间中的混合编辑，生成目标风格化动作。
  
  - 输入 1）基准动作数据 2）参考风格动作数据， 输出：带有参考动作风格的基准动作。
  
  - 例：输入行走序列作为基准动作数据，以及醉酒序列作为参考风格动作数据，生成带有醉酒风格的行走动作序列。


  问题挑战：

  - 全平台的兼容性需要对全平台具有全面的理解。
  - 稳定和低功耗需要不断的完善和优化。


  指标评价：

  - 高兼容性是否满足，能够在哪些平台上运行。
  - 强拓展性是否满足，接口的设计方便后续拓展。
  - 低功耗和低占用是否满足，接入后是否能够稳定运行。

</ProjectCard>

<ProjectCard hideBorder=true>


  ### 动作数据增强管线
  
  课题背景：

  - 在动作生成算法中，动画数据集的扩充能够有效地提升模型在不同场景配置中的通用性效果，避免生成具有交互性的动作时动作在不同尺寸物体上出现穿模，不匹配等效果。[SIGGRAPH Asia 2019] Neural State Machine for Character-Scene Interactions 提出了针对坐下、搬运等动作的数据集扩充方案。


  问题定义：

  - 定义增强管线，根据动作内容，定义动作约束，调整动作约束，反推动作曲线，生成新动作，检验新动作


  问题挑战：

  - 管线依赖工具平台
  - 动作约束的泛用性
  - 反推运动曲线算法
  - 整体工程的结构性及管线高效性
  - 适用场景开放性

</ProjectCard>

<ProjectCard hideBorder=true>

  ### 基于视频的动作捕捉优化
  
  课题背景：

  - 动作捕捉是游戏制作中动作来源的主要方式之一，目前成熟方案主要通过高成本硬件设备进行捕捉，低成本的RGB视频捕捉技术在面向玩家的内容制作上有更广阔的空间，视频捕捉通过姿态估计方法提取视频中的人物3D动作并进行必要的后处理以驱动骨骼角色


  问题定义：

  - 给定包含人物身体运动的视频，生成驱动骨骼的动作信息(关节旋转)


  问题挑战：

  - 视频姿态估计的准确性
  - 相机抖动情形的优化
  - 未知相机参数下相机空间与世界空间的转化
  - 动作提取的稳定性、真实性

</ProjectCard>

<ProjectCard hideBorder=true>

  ### 游戏图像画质优化
  
  课题背景：

  - 在计算机中，因为与具有连续平滑曲线和线条的现实世界对象不同，计算机屏幕向观众显示大量的小正方形，称为“像素”。这些像素都有相同的大小，每个像素都只有一种颜色，一条线只能显示为一组像素。因此除非它是完全水平或垂直的，否则其中像素化的边缘会显示为锯齿状。由于显卡的栅格化渲染，锯齿在游戏中普遍存在，出于硬件限制，在移动端游戏中锯齿化更为明显。
  
  - 抗锯齿即用于从计算机游戏或其他生成图像的计算机程序中渲染的图像中消除锯齿。根据抗锯齿方法的原理，传统的抗锯齿方法可分为两种：（1）通过增加图像的采样率，提高实际渲染的图像分辨率，进而降采样至需求的分辨率，达到抗锯齿的效果，其代表方法有超级采样抗锯齿（Super-Sampling Anti-Aliasing）、多重采样抗锯齿（Multi-Sampling Anti-Aliasing）等；（2）显卡以原始采样率渲染图像，然后使用一系列模糊边缘等后处理操作进行抗锯齿，其代表方法有快速近似抗锯齿（Fast Approximate Anti-Aliasing）、随机采样抗锯齿（Temporal Anti-Aliasing）等。
  
  - NVIDIA公司在2019年初推出了一项深度学习超级采样（Deep Learning Super-Sampling）技术，这是首个使用神经网络技术进行图像抗锯齿的成功尝试。DLSS技术基于图像超分辨，可以使显卡以较低分辨率（1080p）渲染画面，并以较高分辨率（2K或4K）进行输出与展示，并且达到抗锯齿的效果，这样就大大降低了3A大作特效全开的显卡渲染压力，提高了帧率。但是，DLSS基于RTX显卡架构，RTX显卡具有适用于加速神经网络计算的Turing Tensor，Turing Tensor独立于CUDA Tensor，可以在不影响游戏渲染速度的前提下，实时对渲染帧进行超分辨处理。


  问题定义：

  - 本项目是在通用显卡上运行的基于神经网络的游戏图像抗锯齿技术方案，并通过网络服务对移动端游戏的画面进行抗锯齿优化。


  问题挑战：

  - 在相同分辨率下，对游戏图像进行抗锯齿处理
  - 获取符合要求的训练集
  - 提高算法与部署服务的效率，满足玩家的正常需求

  指标评价：

  - 功能完整性，完成功能描述所列举的功能
  - 功能创新性，创造性设计功能描述中列举的功能，或者设计了其他创造性的功能
  - 技术新颖性，所用技术新颖
  - 技术难度，开发功能和使用技术具有一定的难度

</ProjectCard>

## Publications

<ProjectCard image="/projects/8.jpg" hideBorder=true>

  #### Towards High-Fidelity 3D Face Reconstruction from In-the-Wild Images Using Graph Convolutional Networks

  Jiangke Lin, Yi Yuan\*, Tianjia Shao, Kun Zhou

  Computer Vision and Pattern Recognition (**CVPR**), 2020
  
  [[PDF](https://arxiv.org/pdf/2003.05653.pdf)] [[arXiv](https://arxiv.org/abs/2003.05653)]

</ProjectCard>

<ProjectCard image="/projects/7.jpg" hideBorder=true>

  #### Fast and Robust Face-to-Parameter Translation for Game Character Auto-creation
  
  Tianyang Shi, Zhengxia Zou, Yi Yuan\*, Changjie Fan

  the Association for the Advance of Artificial Intelligence (**AAAI**), 2020

</ProjectCard>

<ProjectCard image="/projects/6.jpg" hideBorder=true>

  #### FDN: Feature Decoupling Network for Head Pose Estimation
  
  Hao Zhang, Mengmeng Wang, Yong Liu, Yi Yuan

  the Association for the Advance of Artificial Intelligence (**AAAI**), 2020

</ProjectCard>

<ProjectCard image="/projects/5.jpg" hideBorder=true>

  #### Face-to-Parameter Translation for Game Character Auto-Creation
  
  Tianyang Shi, Yi Yuan\*, Changjie Fan, Zhengxia Zou, Zhenwei Shi, Yong Liu

  International Conference on Computer Vision (**ICCV**), 2019

  [[PDF](https://arxiv.org/pdf/1909.01064.pdf)] [[arxiv](https://arxiv.org/abs/1909.01064)]

</ProjectCard>

<ProjectCard image="/projects/4.jpg" hideBorder=true>

  #### NeuroSkinning: Automatic Skin Binding for Production Characters with Deep Graph Networks
  
  Lijuan Liu, Youyi Zheng, Di Tang, Yi Yuan, Changjie Fan, Kun Zhou

  ACM Transactions on Graphics (**SIGGRAPH**), 2019 (**Oral**)

  [[PDF](https://nos.netease.com/mg-file/mg/neteasegamecampus/art_works/20190624/201906242016238583.pdf)] [[Data](http://fuxi.163.com/thesis/neuro.html)] 

</ProjectCard>

## Reports
- [九游：《逆水寒》AI智能捏脸及双脸融合功能系统上线](http://www.9game.cn/news/2696879.html)
- [机器之心：只需一张自拍，网易伏羲用这种方法直接生成「个人专属」游戏角色](https://www.jiqizhixin.com/articles/2019-09-09-18)
- [机器之心：人工智能改变游戏未来？网易伏羲AI Lab展示游戏开发黑科技](https://www.jiqizhixin.com/articles/2019-05-22-14)


<!-- Custom style for this page -->

<style lang="stylus">

.theme-container.home-page .page
  font-size 14px
  font-family "lucida grande", "lucida sans unicode", lucida, "Helvetica Neue", Helvetica, Arial, sans-serif;
  p
    margin 0 0 0.5rem
  p, ul, ol
    line-height normal
  a
    font-weight normal
  .theme-default-content:not(.custom) > h2
    margin-bottom 0.5rem
  .theme-default-content:not(.custom) > h2:first-child + p
    margin-top 0.5rem
  .theme-default-content:not(.custom) > h3
    padding-top 4rem

  /* Override */
  .md-card
    margin-top 0.5em
    .card-image
      padding 0.2rem
      img
        max-width 120px
        max-height 120px
    .card-content p
      -webkit-margin-after 0.2em

@media (max-width: 419px)
  .theme-container.home-page .page
    p, ul, ol
      line-height 1.5

    .md-card
      .card-image
        img 
          width 100%
          max-width 400px

</style>