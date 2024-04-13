# Awesome-interview-questions-on-Autonomous-Driving

自动驾驶之心为大家准备了自动驾驶感知、融合、规控、标定、预测、NeRF等领域的经典问题，面向春招、求职、社招等求职使用，后期将会持续更新，完整答案将在[【自动驾驶之心】](https://mp.weixin.qq.com/s?__biz=Mzg2NzUxNTU1OA==&mid=2247542481&idx=1&sn=c6d8609491a128233c3c3b91d68d22a6&chksm=ceb80b18f9cf820e789efd75947633aec9d2f1e8b58c29e5051c05a64b21ae63c244d54886a1&token=11182364&lang=zh_CN#rd) 知识星球内公布，更多干货学习，欢迎加入自动驾驶之心经典课程，涉及近20个方向，助力面试！



## 3D&4D毫米波雷达 100 问

1 看了第一章基础知识，有没有相应的数据和代码，看看对应到真实的雷达数据，是怎么完成从数据解析，到测距，测速，测角度的.



2 磁场对毫米波雷达信号有何影响？例如在毫米波雷达附近有一块磁铁，对毫米波的TX/RX有何影响？



3 各个厂家的雷达出数据的帧间隔不同，有的70ms，有的100ms，这个间隔就是PPT里的Tsweep吗？图中两次混频和采样，一个是收发直接混频，一个是发送移相90°再和接收混频，这样起什么作用呢？



3-1 那有的厂家雷达的输出点云或目标的帧间隔达到100ms，这个和普遍70ms比，能说明两者性能上有差距或者问题吗？



3-2 这个100ms纯粹是我作为用户观察到的从雷达收到数据的间隔，确实有明显差异



3-3 大陆雷达ARS408是70ms，按照说明，如果数据量太大，它是准时出255个目标或点云，其余的就丢弃，保证70ms间隔的。我提的这个100ms，不仅仅是厂家提供的参数，而且是实际测试得到的每帧间隔，也就是上一次从can口获得数据到这一次从can口获得数据的时间间隔，所以也不存在厂家是从哪里算起哪里结束的问题。



3-4 嗯嗯，我猜也是纯粹软件的策略。所以不能以此判断某款雷达的最大检测距离、距离速度角度分辨率的性能比较好或差，是吧？



3-5 混频的问题



3-5 PPT里最大探测距离和采样频率成正比，如果想增加最大探测距离，可以调高采样频率。但是如果减小带宽，并且保持扫描周期不变，则S变小，也会增大最大探测距离。在实际中，这两种方式哪种比较常用，比较容易实现？还得考虑减小带宽会对距离分辨率有负面影响。第三种方式，拉长扫描周期，也起到相同效果吧



3-6 感谢。之所以问这个问题，主要是看到有些雷达号称支持远程模式和近程模式，意思是通过修改配置就可以达到目的，我不太清楚修改了什么配置。发射功率肯定是最重要的，但是这些都不是随随便便就可以调的吧？一款雷达同时支持远程和近程，这种硬件同时支持，只是开关控制，不在考虑范围哈。有雷达支持频点和带宽可调，他们的工程师和我说，增加带宽，探测距离就短了。按这个说法，他们可能确实支持调带宽了，不确定真假。总之，我的理解是，一款雷达在设计阶段已经定好指标，一般硬件就做相应的设计，后面就不太会动。如果市面上的某些雷达号称能调各种参数，从而修改各种性能指标，我不知道是否可行，对硬件设计的冗余度要求有多高



3-7 Tsweep一般是40us左右，测速时Tc的数量级是多少？速度分辨率里的N是否就是发射天线的数量？角度分辨率里的N是接收天线的数量？



3-8 fmcw是连续发送的，这里谈N,怎么谈呢？一帧是怎么定义的？我理解一个chirp是从频率最低到最高的一个过程。



4 请教下老师，为什么毫米波雷达有非常多的多径点，而摄像头却没啥多径（除了照到镜子或水面）？另外频率介于两者之间的激光雷达呢？



5 课程里面讲到的标定的方法，如果是雷达做动态标定，如果想去找路上的护栏，要怎么找这个护栏。还有就是激光雷达可以用同样的思路进行动态标定吗？



 5-1 毫米波雷达在动态标定之前，不知道角度，这种情况怎么寻找静止点啊？动静判断是需要已知角度吧？另外一个问题是 如果场景静止点比较少，或者认为不可信，是否也可以用运动点做动态标定啊？



 6 请问峰值点在多普勒通道方向进行移动，代表什么含义啊？



 6-1 请问幅度(Z轴)代表什么，和什么有关系啊，是反映目标物体的能量高低吗？



 7 视觉BEV常用网络将透视图转换到BEV空间，得到BEV特征。 想问一下，有没有研究用网络将毫米波雷达的RDmap直接转换到BEV空间的啊



8  因为我看现在很多毫米波雷达公司使用ti4片级联的方案，里面会使用的fpga做一些高性能运算，我最近接触到一些激光雷达的方案也基本都使用了fpga，因为我对这方面不是太了解，想问一下在毫米波雷达上，把我们常见的信号处理算法放在fpga里面处理，比我们在dsp上效率会提升很多吗？还有就是为什么大家都比较倾向于使用fpga这个东西用于开发？



9 怎么理解“速度维FFT是在帧与帧之间进行”。 RD MAP图显示的是一帧数据，也就是速度FFT在chirp与chirp之间；此外，根据测速原理，通过两个chirp就可以测出来速度，也不需要对帧之间的数据进行FFT。我们加窗是对一帧数据加窗还是对一个chirp加窗？ 例如，如果速度FFT维是对chirp与chirp之间操作，可以认为一个chirp是一个周期，那应该对每个chirp进行加窗。



10 请问在同一个Range下，多普勒维度（速度）方向出现两个峰值点，这种情况该怎么理解呢，可能时什么情况啊？



11 请问一下:雷达部署在车上，是在一个相对坐标系下做的跟踪吗？这个坐标系应该是非惯性系吧？可以做跟踪吗？



11-1 没太看明白，实际在追踪的时候，自车直行和转弯的时候，请问老师，这个虚拟的惯性力是如何体现的?



12 雷达测的是径向速度，假设在后轮中心直角坐标系下做跟踪(vcs坐标系):1.H矩阵应该不是线性的吧？目标在它探测到的径向的垂直方向还有个切向速度啊？我们只是观测到了径向？2.在vcs下，t0时刻的预测和t1时刻的观测，因为车身在动，他们之间是不是有个旋转平移啊？3.正常情况下，跟踪相对速度和跟踪绝对速度哪个更好？



12-1 测量矩阵应该是非线性的吧，观测到的是径向速度，然后把观测转到笛卡尔坐标系，计算得到径向速度分解后的绝对速度，真实的运动应该还有个切向速度也要分解到笛卡尔坐标系吧？

## BEV感知 100 问

### 一、 BEV感知相关的基础知识

1 BEV是什么？



2 BEV感知算法中纯camera的2d->3d是像素坐标转到世界坐标，纯lidar的3d->2d是世界坐标转到像素坐标，可以这样理解吗？



3 2d转3d原理有什么资料推荐吗？



4 如何理解bev空间呢，是俯视视角下的一个平面吗，bev空间里的每个点是用(x,y)表示的吗，还是一个三维表示？还有您说的把图像提取出来特征(C,H,W）转换到3D空间后(C,D,H,W）再拍扁到bev空间，具体是什么意思呢，拍扁后的维度是什么，这里不太清楚



### 二、BEV论文/算法相关

1 请问这里的blob channel怎么理解？



2 BEVfusion的算法把3D lidar的数据用view transformer变成了2D的，是不是会更省算力？那Lidar的距离信息会丢失嘛？



3 老师，你好，请教个问题，BEVFormer中有六层编码器，每一层的输出都作为下一层的BEV查询输入。不明白的地方在于，每一层的输出应该是提取到的特征图才对，为什么会作为BEV查询输出给下一层，BEV查询只是一些可学习的权重参数，特征图为什么变成了权重参数？



4 那就是说，论文中提到的“bev_query是网格型可学习参数”仅在第一层是这样，第二层及其以后在一定程度上都是特征图了。换句话说，特征图的初始值是学习来的，因为初始值与骨干网络提取的特征无关，只能习得一些位置相关的信息了。



5 老师，请问这门课着重会讲解的BEV方法是BEVFusion和BEVFormer吗？我看课程框架介绍可知BEVFusion和BEVFormer都有实战、代码详解部分。初学者选哪一种方法自学较合适？



6 老师，有没有BEV或视觉注意力，transformer相关的demo代码供学习入门的？就是很简洁，包含了关键结构的那种，一些论文开源的代码目前感觉比较吃力



7 我有试过引入transformer在 lidar-base 的3D目标检测任务，但是我数据量比较小，目前来看效果不如之前的Anchor-base和Center-base方法，所以transformer是不是需要更多的训练数据啊？才能达到更好的效果？



8 老师你好，请教个问题：在BEVFormer的时域特征提取过程中（transformer.py文件的get_bev_features()方法中），从can_bus中获得平移（delta_x，delta_y）和旋转角度ego_angle，计算出bev_angle和平移（shift_x，shift_y），这两组平移和旋转分别代表什么，为什么bev_angle = ego_angle - translation_angle？



9 为什么nuscenes榜单上面纯视觉是former形式的性能更好，但是融合的是lss+深度监督更好



10 我想请问一下，我看课程里我们介绍的bev的输入都是multi-view images的，那么单目相机的bevfusion有推荐的方法吗，类似Kitty数据集这种？



11 LSS的lift环节，将深度分布特征和图像特征做外积之后，得到的结果为什么叫做视椎特征（frustum-shaped point cloud）？而且是近大远小的视椎特征？



12 bevformer中怎么建模高度信息的？



13 bevfusion论文中有关数据增强操作的的这句话怎么理解？意思是只要有multi view img的输入，就不用数据增强吗？那是不是指单camera支路和fusion步骤都没有数据增强，只有单lidar支路有？bevdet视频中讲到了，为了缓解过拟合问题，bevdet作者在bev特征编码阶段，也加入了bev的数据增强操作。那bevfusion中 有这个操作吗？看论文中的第二句标红的话，是不是bevfusion中 也用了bev的特征增强？单camera 单lidar和fusion这三条路，都有bev特征，那是都有bev的数据增强吗？单camera支路，不就是和bevdet一样吗，bevdet用了bev aug，bevfusion不用，不会造成bevdet遇到的过拟合问题吗？



14 BEVDet论文中NxDx64xH/16xW/16这部分是怎么转换成Point Cloud的呢，Point Cloud又是怎么转换成BEVfeature形成 64x128x128的feature的呢？我理解是，N个图通过视角转换模块，再结合深度图D和内外参，转换到点云坐标系，然后通过画网格进行AvgPooling得到这个Bev feature。depth Refinement是怎么做的呢？



15 现在点云和图像融合的工作，有用query查询机制，自上而下建立bev空间的工作吗？类似于bevformer的思路，但是 是用于多传感器的，有类似工作吗？



16 bevdepth论文中将离散深度分布替换为软硬随机数并没有崩，这是什么原因呢？



17 bevformer的dataset的时间轴上的读取问题。论文中说是以当前时刻为基准、在过去2秒中任意取3个过去的sample和当前的sample，这个操作怎么弄的，源码中在哪里写的 是data loader么？



18 BEVFormer网络通过backbone提取出来的特征具体是什么？是位置？方向？还是别的什么？



19 BevFormer中什么是bev空间特征上的对齐？为什么要实现特征对齐？



20 在bev空间上，要检测A目标，肯定要用对应的A目标特征，拿其他目标的特征过来有啥用？



21 BevFormer里在temproal self-attention，和spatial self-attention两个模块的Q、K、V分别是什么？



22 Bevdet4D中有个grid_sample warp 这个怎么理解？



23 请问bevformer是不是3D到2D方法的隐式映射？



24 BEVFormer的get_bev_features()函数中，ego angle、bev angle、rotate angle具体指的是什么相对什么的偏移角度啊？以及这个BEV空间是以哪个坐标系构建的，BEV坐标原点是？



25 PETR主体结构，这里将3D position维度变换到和2D feature特征维度一致，怎么理解啊，感觉就是为了凑，两个维度原本不一样，现在强制变成相同维度，最终会不会造成在不同的3D position出现相同的2D feature 或者在同一个3D position出现很多个2D feature？



26 image的数据增强，例如翻转等操作，如果投影到BEV空间点不变的话，和image数据增强前一样，这样的训练是不是有问题啊？图像相对之前翻转了，原来图像对应的BEV空间点是不是也得做相应变动？视频里老师讲到图像增强时BEV空间保持不变，导致了BEV encoder过拟合，所以会出现图像翻转但BEV空间不变的情况吗？改进方法中，为了防止BEV encoder过拟合，增广图像的逆变化是不是取消掉了？这个增广是2d图像域的数据增广吗？



27 麻烦请教下，配置文件里面，bev_w,bev_h设为200，这个200的单位是啥？是pixel，还是长度米？



28 lss过程中kept根据范围过滤掉了一些点，从137w点变成了55w点。为什么会有点不符合200，200，16的bev范围呀？因为我看get geometry生成世界坐标都时候，就是按照点云的范围生成的呀，经过一个转换过程为什么会有点出界？



29 想问一下特征维度和高度格子数，两个数相乘就代表融合了，那我直接拿两个数字相乘和用torch的方法来相乘有什么区别啊？



30 detr3d中，query转center points，然后转到2d图像，最后怎样利用2d信息更新query的？其中的offset是指query与3d bbox的offset吗？



31 Bevdet4d中运动的物体不对齐不会对检测结果产生影响吗？那这种运动的物体，bevdet4d怎么对齐的呢，是直接根据tracking按框累加吗？动态目标怎么和静态目标一样抹去自车运动偏移的，刚才想到的是根据每个目标的速度按照框累加特征，这样运动目标不会产生拖影吗？为什么不考虑呢？动态目标在运动，前后帧的动态目标在抹去自车偏移的情况下，仍然是不对齐的啊，这样拼接会产生一个长长的拖影目标，和标注没关系。



32 batch_size的大小会影响模型最后的检测精度吗？大的batch_size是否容易造成过拟合？那应该如何选择一个最优的batchsize呢？不断调参吗？以及学习率需要相应调整吗？



33 关于bevfusion中图像输入尺寸的问题，我看配置文件，无论是单图像分支还是融合分支，默认的图像尺寸都是800\*448的，但我看nuscene的图像，都是1600，900的呀，这个默认➗2的设置是通用操作吗？如果改成1600\*900的会提高性能嘛？原论文中给的实验结果表格，也没有标注训练的图像尺寸是多大，所以他这个结果表格中比较的方法，都是基于800\*448的图像大小训练的吗？



34 bevfusion有了权重文件了，怎么可视化检测结果呀，也即在图像和点云上画框的结果。输出了两个obj文件 一个点云的 一个框的，怎么用open3d可视化出来啊，拿cloudcompare确实可以读取这个文件，但是可视化效果不好。



35 mmpycocotools和pycocotools相互冲突的问题



36 请问bevformer每个模块的反向传播是怎么实现的，代码在哪个位置？是怎么调用的啊？插入一个模块怎么让它的参数加入反向传播，插入方法就和sca、tsa差不多？比如说自己写了一个class，一个小模块，怎么加到这个mmdet3d的体系里面，让其可以再config文件中调用？有以下报错，怎么解决？



37 BEVDet4D中关于时序部分的代码，也就是将上一周期的BEV特征拼接到当前帧的代码在什么位置？



38 BEVFormer的可视化怎么实现？



39 BEVFormer里面transormer.py的get_bev_features函数这里面ego_angle, rotation_angle,translation_angle都是什么区别啊?那ego angle是相对于最开始的时候的坐标系的角度吗?平移偏差角度和旋转角有什么区别呢?



40 BEVFormer代码中tmp_prev_bev = rotate(tmp_prev_bev, rotation_angle,center=self.rotate_center) 如果跑tiny网络的话 tmp_prev_bev的大小是[50,50], 这里的center为[100,100]作者是不是写错了,还是按照[200,200]设置的中心点?



41 nusc的全局坐标系和ego坐标系一个朝向吗？global是？为啥角度需要提前计算为-yaw-pi/2后送到lidarinstances3dboxes呢？



42.1 在BEVFormer的六层编码器中，为什么每一层生成的BEV特征在下一层中仅仅用于生成MSDA（Multi-Scale Deformable Attention）所需要的采样偏移和注意力权重，为什么每一层都要完全重新提取新的BEV特征？而不是叠加到既有的BEV特征上？为什么每一层都要重复训练将query转换成采样偏移和注意力权重的线性网络？（2）六层编码器中，3D参考点的位置是固定不变的，唯一能学习的参数只有将query转换成采样偏移和注意力权重的线性网络，六层都在重复学习这个线性网络，学到的到底是什么？好像只学到了3D的稀疏BEV特征点和2D图像上有限的几个特征点之间的映射关系，而且六层都在重复干同样的事情，六层之间会有什么区别？（3）query转成offset之后，感受野可能扩大了，但是通过MSDA提取到BEV特征之后，在下一层中又把这个特征再次转化成了offset，又去重新提取新的BEV特征，BEV特征本身没有保存下来，形不成累积的效应。对于这一点我不是很理解。（4）虽然bevquery的初始值也能学习，但是感觉编码器的这部分网络结构似乎就是想在图像上找到某几个最关键的像素位置，也就是学习相机内外参，然后就用这几个关键像素位置来决定一切，而不是尽可能多的将图像特征转换到BEV特征。不知道我的理解是否正确。BEVFusion4D的LGVT模块看起来也是类似的架构，只不过参考点换成了点云预训练的BEV，大家都这么干，自然有道理，但是不明白。



42.2 msda 模块在用的时候都是嵌在 for 循环里面的，所以六个 layer 是串联结构，并不是完全独立模块。另外，query 转换成 offset 的一个好处其实是扩大感受野了，全局感知能力会更充分一点。



42.3 不只是 offset 参数可学，bevquery 本身也是可学的。offset 使用六层我们猜测还是因为参考了 transformer 原始结构的，其实还是挺冗余的，你可以魔改试试，我们之前尝试过缩到 4 层性能也几乎没影响。



42.4 offset只是一个去图像特征采样的偏移量，offset最终还是会形成output，i-1 layer的output是作为 i-th layer的query去用的，所以还是一个串联的结构，并不是独立存在的。



42.5 这种deformable attention的方式对于bev上一个grid来讲，是1对k的关系，1个bev grid对到camera上k个位置，但是对于bev feature而言，就是n个grid和n*k的对应关系了，并不仅仅是几个点的对应。而且我觉得这种并不是相机内外参的对应关系，如果仅仅是相机内外参，bev上一个确定位置的grid只能映射到确定位置的camera pixel上，而不是现在说的offset关系。



43 刚刚看bevformer代码讲解，bevformer对于历史帧的特征并不是保存起来，而是获取历史帧队列再提取一遍是这样吗？



44 请问bevformer参数量大概有多少呢？



45 请教一个问题，对bevfusion的图像流进行训练，训练出的权重用来做仅图像流的测试，发现结果map是0请问这是什么问题呢？



46 在训练BEVFusion的时候，相机流和激光雷达流都能分别训练起来，但是融合的配置文件里面的权重文件不知道在哪儿下载?



47 我想问下bevfusion仅图像流训练的话，一般要迭代多少个epoch呢？



48 我自己训练的权重用来测试map为0，但是用他们训练好的测试就正常，这是什么问题呢？因为显存的问题，bs只能等于1，这样的话是不是epoch要大些，才能收敛？但是是ddp呀，每张卡bs为1 也不好收敛嘛？emmm，作者训练用的显卡是？论文中有提吗？



49 学习BEV需要哪些前置的知识？



50 如果使用BEV的空间的话，那BEV里的标注是如何产生的呢？ 如果我目前有相机的标注数据，然后有激光雷达的标注数据。是不是要通过这两个数据进行融合才能得到bev的标注数据。但是我又了解到只有%5的相机数据和摄像头数据是可以匹配的。这样岂BEV的标注数据是不是不太行



51 老师，轻量化的bev算法有哪些呢？



52 3d空间是基于点云做的吗



53 老师。您好，lidar做检测的时候，如果不同厂商的激光雷达，拼接后使用一个模型，这个intensity的使用，有没有什么办法啊？



54 bev鸟瞰矩阵[200 200 4]，对应的物理空间大小是多少？纯视觉方案一般可以稳定做多远距离？距离有限主要受限因素是什么？可以通过哪些方案去做距离延伸？



55 想把bev用于传感器标定，有什么好的思路吗？



56 如果我训练了10个类别的目标检测模型，但只需要对其中2个类别进行推理，可视化查看其性能，这种情况一般在哪里修改代码（不限模型）？



57 老师训练bevfusion在自己数据上（前视加lidar采集的），自己的数据类似kitti这种标注，需要转成nuscenes有没有比较好写的方案呢？ nuscenes转kitti有借鉴的，我自己的数据类别比kitti多！



58 新版的mmdet3d集成了bevfusion，区别和课程大吗？



59 有什么论文和方法可以解决遮挡重投影的问题？



60 请教一下目前BEVFormer这类top-to-down的纯视觉BEV方案，虽然已经不需要进行深度估计了，但是性能和lidar方案仍有较大差距，这是为什么呢，有相关的研究吗？

## TensorRT部署和CUDA编程 100 问

### CUDA编程入门

1、CUDA核函数嵌套核函数的用法多吗？



2、代码里的 grid/block 对应硬件上的 SM 的关系是什么



3、jetson系列，一般都是共享内存，是不是不需要使用cudaMemcpy这个函数了? 要使用其他的memcpy方式吗?



4、host内存应该不能直接传到share memory吧？肯定要过一次显存，我理解的没问题吧？如果遇到只需要读一次的情况，比如说resize操作，是不是就不需要用到共享内存了呢



5、对这个图有点疑问，按照左边的启动方式，如果d2h1需要等kernel3之后才运行，那为什么kernel1不需要等h2d3之后？



6、2.4章节，定义宏的时候，加call与不加call有什么区别呢？



7、求助一下大家，不知道这块的访存量怎么理解，是不是缺少了cin输入read的feature项呢



8、图像数据在GPU显存中的排列顺序是chw还是hwc？



9、Texture memory 是off chip 还是 on chip? 



10、8704个cuda  core是怎么算的？int32  Fp32  fp64加起来每个SM  160个cuda core？



11、它去计算8或16位，是硬件电路简单或复杂的方式来实现的，无论乘法器如何设计，结果以一个时钟周期为准，如果cuda core时钟周期内能做一次FMA，就等于2次 FLOPS。老师是这么讲的，这些信息里有啥修正的吗？



### TensorRT基础入门

1、为什么trtexec转换engine时，采用FP16推理、INT8量化，推理延时可能变得更久？



2、什么是Myelin？



3、constant cache和constant memory的区别？



4、在cuda, cudnn, tensorrt版本相同的情况下，可以将其他电脑上转换好的trt直接在自己电脑运行吗？



5、请教一个问题：对于比较大的模型，对于边缘设备trtexec搜寻时间太长有什么好的方法或者技巧么？（转engin搜寻最优的layer的过程时间过长）



### TensorRT模型部署优化

1、模型部署后，用什么手段分析推理性能？



2、神经网络中吞吐和延迟的关系？



3、tensorrt量化方法？



4、模型导出fp32的trt engine没有明显精度损失，导出fp16损失很明显，可能的原因有哪些？



5、onnx模型推理结果正确，但tensorRT量化后的推理结果不正确，大概原因有哪些？



6、采用tensorRT PTQ量化时，若用不同batchsize校正出来模型精度不一致，这个现象是否正常？



7、关于对齐内存访问的疑问：如果使用L1cache，访问的颗粒度为128B，对齐的首地址应该为128B偶数倍，不应该是0B，256B，512B.......吗？



8、TensorRT如何设置混合精度推理 在int8模式下如何单独设置某一层的精度。



9、如何使用nsight或CUDA runtime api分析模型推理性能？



10、如何尽量减少GPU和CPU之间的数据交互或内存分配与回收？



11、如果QAT可以使模型尽可能减少量化带来的误差，那么可以不做敏感层分析，直接将整个网络量化为INT8吗？



12、模型量化到INT8后，推理时间反而比FP16慢，这正常吗？



13、请教一下，engine推理的时候，batchsize=1和batchsize=4，推理时间相差也接近4倍合理吗？有什么办法让多batch的推理时间接近单batch吗？比如加大显存？



14、在device固定的情况下呢？有什么参数设置或者增加streams的方式吗？试过把workspace设到最大，只有轻微的提升



15、问题描述如下:在取出A矩阵的i,k的值的时候为什么是(float)_A[i*_wa+k]，而不是(float)_A[i+k]



17、cuCtxCreate(&cu_context, flags, cu_device)；  // 这个函数耗时长，单次大约3s，大家有没有遇到过？



18、老师，想请问一下，在进行多流处理的时候，为什么分流后他们不重叠呀



19、我们在双线性插值计算图中B的坐标的时候，采用的是src_y1, src_x1为目标点x,y还原到原图后对应的点的最近的左上整数坐标点



20、老师讲stream那节课说一般是overlap核函数和内存之间的拷贝，但是两张图展示的效果肯定是上面这个好，但是和老师说的就有点违背了上面那个全部是核函数之间的重叠，下面那个虽然核函数执行把memcpy给overlap了但效果并不好（老师可不可以讲解一下这两个图的区别）



21、问题描述如下：

问题1、三个红箭头调用都是异步的： 

1. 异步调用后cpu不会阻塞而是立刻返回往下执行？  因此cpu调用函数  不等于 函数在gpu上真正launch？              
2. 什么是k函数启动（launch）？是指代码中kernel函数被cpu调用时刻 ，还是 k函数在gpu上真正开始运行时？  
3. 老师能描述下代码中异步调用kernel函数后发生的过程吗？比如资源沾满要排队时，这算是被cpu调用了吗，cpu会继续往下执行代码还是阻塞在那一句代码处？ 又或者算是被启动了吗？   我想知道cpu执行到异步调用kernel函数，和这个kernel函数启动，以及这函数真正在运行，三者是什么关系？



### 部署分类器

1、请问一下，如果有多个input host ，多个output host,在infer这里，那bindings那那些该怎么写呢？可以提供个模板吗



2、deformconv在opeset19支持了，所以我不用custom 符号，而是用这个opset19支持的算子。 结果export onnx失败，是为什么呢？



3、layernorm在opset17才开始支持，那为什么将opset12的onnx加载后，可以替换为LayerNorm onnx算子，opset12是没有这个算子的吧？我猜opset版本只在export那一步时使用？会到12.py去搜对应算子。 而通过surgeon.register的会全局搜算子？



### 环境配置BUG解决

1、两个问题想请教下（1）我的服务器用户名是kemove，图中所有的${user}都要改成kemove吗；（2）我要用的文件夹是/hdd/spp/，我可以把75行注释掉然后把76行和82行的路径都改成/hdd/spp/吗？



2、当sleepMutilstream 改 用multistream 计算5个不同的乘法 这种更实际的情况时，引入了几个问题，请同学帮忙一起看看：



3、同样的量化代码和预处理的校准数据集A_data，在A模型上没有问题，int8的map只比fp32掉了0.3%。但是量化代码和预处理数据集B_data，在B模型上量化掉点30%，如果B模型转成fp16是完全不掉点的。针对B模型int8量化掉点问题，我试了所有的校准器也依然失败的。现在怀疑是某些层（敏感层）的问题，但是将输入输出的好几个层换成fp16，依然掉点30%。请问有没有其他方式来改进掉点问题，最好是有代码example



4、生成onnx遇到不支持的操作那里还是没学会，比如用到了torch_scatter的scatter_max，还是生成不了onnx模型，怎么能导出onnx模型然后去写plugin呢？参考例子里的CustomOp总是遇到问题导不出来。



5、关于spconv这块，示例中生成的onnx的input size是5\*1的,但生成对应trt推理引擎的input size实际应该是voxelNumber\*5。libspconv库在生成推理引擎时是做了动态shape的转换吗？



6、5.1节make老师的sampleonnxmnist_cn出现报错，但是make tensorrt samples里面带的sampleonnxmnist成功为什么？



### 其他补充知识

1、什么是边缘设备？



2、学习cuda书籍推荐？



3、nsight的使用平台说明



4、如何升级AGX ORIN平台中的tensorrt版本？



5、(保姆式教学) Win10 + Ubuntu 20.04——双系统安装方法 + 配置显卡 + root权限 + flash调配



6、spconv的部署吗？推荐👇稀疏卷积的高性能部署



7、问一下hopper架构对于transformer优化会有多大影响呢？



8、地平线采用IPM 映射这块有没有什么办法不放在cpu上做呢？或者有什么推荐的方案呢？ 参考资料: https://developer.horizon.ai/forumDetail/118364000835765864


## Occupancy Perception 100 问

1 一个关于说从入门到精通的入门的点。就occupancy的数据格式而言，PPT讲了它是基于体素。但是如果我想修改occupancy到其他设备要改这个范围跟格子大小的时候，应该怎么改呢？这个xyz具体是怎么组织的，位置索引里是中心点还是端点？这些都没有提过。



2 相机我可以理解为体素投影到图像上只学习能投影上的，lidar的话如果不是机械雷达该怎么算呢？



3 请问一下，我在运行surroundocc训练指令的时候找不到chamfer这个包，但是我安装的时候现在安装了这个包，然后我pip list也没找到这个包，好像是按照在python里面了，我去找了网上的方法说重新编译，但是我编译了几次都不行，然后我尝试直接pip安装这个包，但是好像只能通过代码来安装，pip也失败了。



4 可以解答一下，关于3D语义分割和Occupancy两种评价方式的区别吗，真值的区别，以点来评价还是以体素来评价



5 以激光雷达语义分割结果生成真值的多模态occ和ssc的具体区别在哪里，有没有加visible mask吗？我的意思是如果把free作为一个语义的话这两个任务是不是都是在对所有体素进行分类，还有一个问题想请教一下小助教，就是一个scene里面往往激光雷达也只能扫到一部分，那么这样一辆车可能也就只有四分之三的体素标记为车，这样在大量数据的训练下网络能补全出完整的车辆吗？



6 请问将bevfusion的3d检测头替换为占用和语义头可行吗？



7 这些OCC真值，和nuScenes里面的点云标注文件的区别是不是只是稠密跟稀疏的区别，那在训练的时候，还会读取nuScenes里面的bin文件吗，那如果我不生成GT，直接把nuScenes里面的bin转成npy当做OCC真值来训练可以吗？我还想问如果想输出密集的占用预测，是不是应该用带语义分割的雷达点云数据合并生成密集的占用真值作为监督？



8 能不能把3d occ的算法几何头和语义头分开训练呢？如果几何头训练完换一个场景还能进行准确的占用预测吗？课程里面提到3d occ的一个优势是把几何和语义解耦开，老师能不能具体解释一下这句话？



9 单目和环视的occ除了输入不同以外方法上有什么区别吗？



10 SurroundOcc在计算loss的时候，需要修改occ_size吗，如果换了范围的话，改了范围之后维度不对了，转真值的时候我也改了范围的，不知道训练的时候，除了配置文件要改范围，还有没有其他地方要改，老师给的数据



11 请问一下，怎么把surroundocc的可视化调大一点，那个画板空一大片，调小了voxel也跟着小，有什么方法能把可视化的体素调大点



12 Occ的优化是从哪些方面做的？



13 想请教一下每个视角的可视化改怎么做呢？或者有没有什么项目也是这样做的。我现在得到了npz文件用open3d可视化只能拖拽了看，没法得到每个视角的occ结果



14 想请教一下有没有用3d occ和激光雷达点云做融合的方案



15 请问有没有轻量实时的occ模型,想把这个当做base code



16 关于占用网络，有没有类似nuScenes Tasks那样的Leaderboard？



18 两位老师早上好,我这边是做封闭场景重型机械的应用,目前用的是纯Lidar的方案,想在Lidar的基础上把Occ链路打通,所以有些问题想请教

1. 老师课程中提及,Occ如果把voxel size无限缩小, 那就是和点云是同一表示, 请教一下老师, 如此看来, 纯视觉Occ和点云的栅格化地图有什么区别?

2. 纯视觉Occ是否能提供障碍物的深度信息/类别信息? 课程中老师提及汽车做行车安全不需要知道障碍物类别,只需要知道能不能撞,几何有没有占用. 那如果对不同的障碍物避障逻辑不同(比如人是直接刹停,其他车辆选择绕障),Occ是否可以满足这个需求?

3. Lidar+Camera的Occ方案 和 纯视觉Occ方案相比 有哪些优势?

4. Lidar+Camera的Occ方案 和 点云语义分割/点云目标检测 相比有哪些优势?



19 想请教一下SSC和3D Occ之间的差异



20 最近在看openocc模型，作者把lidar camera融合的过程中是不是并没有用lidar做深度监督呢，感觉是直接把两个模型特征相加，两个传感器的特征相互没有关系，那如果其中一个分支预测出现偏差，这种自适应融合能够纠正吗？



21 occupancy 数据集只能通过segmentation 结果生成吗？在工程上，怎么让标注人员标注呢？先将点云生成voxel，然后再标注吗？



22 想问下目前主机厂对于Occupancy Prediction持什么态度，目前的进展是什么，实测的话一般部署在什么设备上？



23 请问，我又同一区域不同尺度的点云（无人机获取的30m与50m），需要制作高精度地图，我应该先进行点云拼接呢，还是单独先作点云语义分割呢？



24 大家知道自动驾驶落地的定位技术常用的有哪些啊,尤其是传感器只有GPS，imu和双目的话



25 特斯拉这种类似mesh的车机渲染是occ后处理嘛？大概多高分辨率能有这个效果呀？



26 想请教一下，特斯拉的人形机器人，上面只装了三个RGB相机，有人知道训练occupancy map时，深度的真值从哪儿来的吗？

1. 那机器人和汽车运动时，不只是平移，还有旋转，怎么办呢？

2. 那仅依靠单目视频重建出来的场景，也缺乏真实尺度?

3. 那还需要imu、轮速这种来提供物理尺度吗？

4. 那这样说的话，他们在人形机器人上也不应该会使用深度传感器来提供真值。



27 MonoScene不是单目嘛？这怎么算？就是他是单目获得的深度信息是吧？只是他获得的深度信息不太可靠，是这个意思嘛？



28 Surroundocc是不是就是只用了lidar做监督，没有用于推理？

## Nerf 100 问

1 目前NeRF在业界应用比较多的是什么领域呢？未来能应用在什么领域呢，除了自动驾驶？



2 MARS中的NSG可以认为是官方的那个代码的pytorch&nerfstudio版本实现吗？



3 F2-NeRF 是什么？



4 对于新学NeRF的小白，需要补哪些基础内容啊，有没有推荐啊？



5 对于代码的学习，需要学哪些论文的代码来入门啊？



6 Nerf的发展怎么样了？



7 NeRF还存在哪些问题需要研究？



8 Taichi NeRF这个大家了解么？



9 为什么3dgs渲染颜色感觉过曝了？



10 另外Mars跑Nuscene的数据集有简单的办法吗？



11 缝合单目深度估计和RGBD的nerfslam有前途么？



12 nope-nerf算是nerf slam的工作不？



13 MERF如何bake？



14 mobilenerf的上采样抗锯齿操作具体用在哪个地方？bake之后的渲染如何抗锯齿？



15 mobile nerf用的3个MLP分别是什么样的结构？



16 mobile nerf在建模无边界场景的时候有没有warp？如果有，它是怎么warp的？



17 像UniSim和NeuRas这种，有没有类似效果的复现呢?

## 车道线检测答疑手册

### 一、引言概述和环境部署

1：车道线检测出来后有哪些实际用途？

## 二、标注相关

1：想请教一下有关地图重建论文中的GT都是从哪获得的阿？为什么在原始数据集中没找到相关的描述呢？



2：老师您好，还想再请教一下。您说的3D车道线，标注的话应该怎么标呢？我们做LiDAR点云车道线都是用的传统算法基于高度和reflectivity算的。没有用深度学习。



3：假如说图像中有一条车道线看得清楚，有一条车道线被挡住了，那么被遮挡的这条车道线需要标注吗？

### 三、车道线跟踪匹配

1：老师您好，想请教一下评估两个车道线匹配程度，用DTW算法可以吗？



2：请教大佬们一个问题，现在我想搞一个高速目标车辆的意图识别，采用混合高斯去做，特征值初步选定:目标车辆相对其车道中心线的横向位置，yaw角度，和加速度。我想知道每条训练的数据如何标注-----对于车辆的一条变道轨迹，应该截取哪一段比较合适?

### 四、MapTR

1：MapTR中initial 状态为什么是很多条不同的polyline，之前地平线视频定义为anchors，如何理解？



### 五、PETR

1：PETR预测车道线是预先设置了anchor还是用anchor直接去预测？



2：这个anchor lane 有设置vis可见度这个属性嘛？

### 六、LaneNet

1：LaneNet中的HNet（用于获取单应性矩阵H），可以解决颠簸或者上下坡时候的IPM转化问题嘛，如果不能解决，目前工业界采用那种方式？



2：讲解视频中提到LaneNet在弯道及分叉路口效果较好，基于Row-wise方案的CondLaneNet，RIM支持分叉路口但是在工程中应用比较少，所以想了解下，目前业内工程落地场景比如城市主干道场景会涉及到弯道和分叉路口，更多的选择的是LaneNet还是什么模型？



3：2D图像分割生成的是什么坐标系？如果是像素坐标系为什么不能直接通过内外参得到世界坐标系，然后再拟合方程？

### 七、车道线后处理

1：得到车道线坐标点后，使用opencv中的fitline函数拟合直线有时候会报错，其可能的原因？



2：如果一根车道线被检测成两根车道线（并排两根或者前后两段），有什么后处理方法？



3：完全无车道线场景检出了车道线，有什么方法过滤吗？



4：目前感知输出了车道线参数（车道线曲线中的C0/C1/C2/C3值、检测的置信度等），但是从输出的原始数据看，曲线比较杂乱，且不稳定。通常是采用什么样的方法对原始数据进行处理，以保证可以得到稳定且连续的车道线输出结果？



5：用分割做车道线要把分割结果mask拟合成一条曲线，为什么要有拟合曲线这一步，mask为什么不能直接作为结果？

### 八、基于雷达的车道线检测

1：为什么行业用Lidar做车道线检测的方案较少？



### 九、LaneNet

1：lanenet的两个分支是分别同时进行训练，然后每个分支各有各的损失函数和训练参数吗？



2：这个算法和多类分割的区别在于lanenet预先没有定义标签数，而多类分割开始就定义了标签最大数量，不能适用于检测车道线数量变换的场景，对吗？



3：h-net网络也是训练前一个网络的时候训练的吗？

### 十、UltraFastLane

1：UltraFastLane里为什么要用FC（Full Convolutional）不用GAP（Global Average Pooling），目前大部分paper貌似都用GAP替换FC了，这边用FC有什么优势吗？



### 十一、Gen-LaneNet

1：这里怎么理解“anchor points in a coordinate frame not aligned with the underlying visual features”？



2：这里的anchor不是定义在俯视图上的嘛，从俯视图上得到为啥会和图像不一样呢？

### 十二、BEV

1: BEV车道线检测和IPM的区别是什么？



2：基于地平假设将Zw置0后，已经求出了车道线上各点的世界坐标Xw和Yw。那此时根据XY把线画出来，车道线已经都是平行的了么？



3：IPM修正的方法里，拟合曲面具体有哪些方法，曲面参数表达是什么呢？

### 十三、2D车道线分割

1: BEV车道线检测和IPM的区别是什么？先对图像做2D的分割，再对车道线信息聚类，然后使用IPM方法获得3D车道线结果的方案 有比较好的开源算法作为参考吗？



2：laneNet可以用聚类得到车道像素值，但是车道id怎么区分呢 就是 当前左右 两侧左右这种情况，计算车道的x平均坐标吗？



# 自动驾驶学习社区

自动驾驶之心知识星球是过国内首个以自动驾驶技术栈为主线的交流学习社区（也是国内最大哦），这是一个前沿技术发布和学习的地方！我们汇总了自动驾驶感知（BEV、多模态感知、Occupancy、毫米波雷达视觉感知、车道线检测、3D感知、目标跟踪、多模态、多传感器融合、Transformer等）、自动驾驶定位建图（在线高精地图、高精地图、SLAM）、多传感器标定（Camera/Lidar/Radar/IMU等近20种方案）、Nerf、视觉语言模型、世界模型、规划控制、轨迹预测、领域技术方案、AI模型部署落地等几乎所有子方向的学习路线！

除此之外，还和数十家自动驾驶公司建立了内推渠道，简历直达！这里可以自由提问交流，许多算法工程师和硕博日常活跃，解决问题！初衷是希望能够汇集行业大佬的智慧，在学习和就业上帮到大家！星球的每周活跃度都在前50内，非常注重大家积极性的调度和讨论，欢迎加入一起成长！

[加入链接：自动驾驶之心知识星球 | 国内首个自动驾驶全栈学习社区，近30+感知/融合/规划/标定/预测等学习路线](https://mp.weixin.qq.com/s?__biz=Mzg2NzUxNTU1OA==&mid=2247580846&idx=1&sn=8bef76bf11bb0d5a92c32efdff315750&chksm=ceb99167f9ce18712e01dbbdb3991405ea619b5c8c57681c4f27debc8cc117cfb6d2690da9da&scene=21&token=85321819&lang=zh_CN#wechat_redirect) 

# 自动驾驶课程

### 1）感知算法

[国内首个BEV感知全栈系列学习教程](https://www.zdjszx.com/p/t_pc/goods_pc_detail/goods_detail/course_2MjRdDQO8jGkz1Sx4AoJ0sytlIU)

[多模态融合3D目标检测全栈教程](https://www.zdjszx.com/p/t_pc/goods_pc_detail/goods_detail/course_2SYwAhLiNWCyKhwUhSDjFihH7tx)

[国内首个基于Transformer的分割检测+视觉大模型教程](https://www.zdjszx.com/p/t_pc/goods_pc_detail/goods_detail/course_2TfDGv45mQbTBKS5km4MoQ4Vu66)

[Occupancy从入门到精通全栈教程](https://www.zdjszx.com/p/t_pc/goods_pc_detail/goods_detail/course_2TerMWEsK9xR32mtgXwaFdxeSYs)

[国内首个面向量产的车道线感知教程](https://www.zdjszx.com/p/t_pc/goods_pc_detail/goods_detail/course_2UdY0Nw3nbRWYDJv9o9lgMcOvti)

[点云3D目标检测理论与实战教程](https://www.zdjszx.com/p/t_pc/goods_pc_detail/goods_detail/course_2WTzeULfAL2IZ32ezqrHhIQyrKG)

[单目3D与单目BEV全栈教程](https://www.zdjszx.com/p/t_pc/goods_pc_detail/goods_detail/course_2Uc2U3dSQMqMX3FhA498V2x78Nd)

[国内首门毫米波&4D毫米波雷达理论实战教程](https://www.zdjszx.com/p/t_pc/goods_pc_detail/goods_detail/course_2WZpSw1X4P6FdSF1OMgj5aAe90p)

### 2）多传感器标定融合

[多传感器融合与目标跟踪全栈教程](https://www.zdjszx.com/p/t_pc/goods_pc_detail/goods_detail/course_2SHcc3nnl15j1f7EDGl0B22Vbg4)

[多传感器标定全栈系统学习教程（相机/Lidar/Radar/IMU近20+种在线/离线实战方案）](https://www.zdjszx.com/p/t_pc/goods_pc_detail/goods_detail/course_2PHSMppQhtUsLZ2R18GWOMOK5GW)

[毫米波雷达和视觉融合感知全栈教程（深度学习+传统方式）](https://www.zdjszx.com/p/t_pc/goods_pc_detail/goods_detail/course_2OpLfiVIGEGIt0vdHhqie7LqFbG)

### 3）模型部署

[基于TensroRT的CNN/Transformer/检测/BEV模型四大部署代码+CUDA加速全栈学习教程](https://www.zdjszx.com/p/t_pc/goods_pc_detail/goods_detail/course_2Qzh2CekDJZMNuZq1Gfp3HOgIqx)

### 4）规划控制与预测

[规划控制理论&实战教程（从0到1彻底搞懂PNC算法）](https://www.zdjszx.com/p/t_pc/goods_pc_detail/goods_detail/course_2R0KKH62Mo6UrSn6oxV6nL2LlH9)

[轨迹预测理论与实战教程（国内首个轨迹预测系列）](https://www.zdjszx.com/p/t_pc/goods_pc_detail/goods_detail/course_2VBk5awcjfEpgwzJ0RFdP7ZcIqg)

[轨迹预测论文带读教程（从论文角度分析轨迹预测领域）](https://www.zdjszx.com/p/t_pc/goods_pc_detail/goods_detail/course_2WOHt6sLxFGUTazapwEVLI3qeqq)

### 5）Nerf与自动驾驶

[国内首个Nerf与自动驾驶论文带读教程](https://www.zdjszx.com/p/t_pc/goods_pc_detail/goods_detail/course_2VIPT5xg9bCdQpg2c9GaWELR38N)

### 6）大模型专场

[国内首个大模型与自动驾驶应用论文带读教程](https://www.zdjszx.com/p/t_pc/goods_pc_detail/goods_detail/course_2YGQzZEjc5f7Z7zpdlGrsD9gNl7)

[世界模型与自动驾驶论文带读课程](https://www.zdjszx.com/p/t_pc/goods_pc_detail/goods_detail/course_2ZIw7WP2H3SPvnc2PiVCnP0trJv)

### 7）定位与建图

[在线高精地图与自动驾驶论文带读教程](https://www.zdjszx.com/p/t_pc/goods_pc_detail/goods_detail/course_2ZXECfaORjGOsNH5ro5kULmfIOA)

### 8）自动驾驶仿真

[自动驾驶离不开的仿真！Carla-Autoware联合仿真实战](https://www.zdjszx.com/p/t_pc/goods_pc_detail/goods_detail/course_2bCKkNYcHG2Vs9Nnynr5bZZQwBr)

### 9）大专栏系列

[多传感器融合感知标定全栈教程](https://www.zdjszx.com/p/t_pc/goods_pc_detail/goods_detail/course_2PiRligVG0RyIohy6A3covkScbw)

[多传感器标定/融合感知/模型部署全栈教程](https://www.zdjszx.com/p/t_pc/goods_pc_detail/goods_detail/course_2R2ZQoo9TK4wuCbVsP2Pg0l0dZ8)

[感知算法与模型部署全栈教程](https://www.zdjszx.com/p/t_pc/goods_pc_detail/goods_detail/course_2R2VoF87LmdBvw2RnGBSgj2l2zL)

[自动驾驶全栈算法工程师系列](https://www.zdjszx.com/p/t_pc/goods_pc_detail/goods_detail/course_2RCJlwWnGdgbFJAnXa5vaOK7Nh2)

[多模态融合感知大专栏](https://www.zdjszx.com/p/t_pc/goods_pc_detail/goods_detail/course_2TkVCn9jpK4b1nQfuil54Cb58hL)

[自动驾驶全栈大专栏教程](https://www.zdjszx.com/p/t_pc/goods_pc_detail/goods_detail/course_2VOGLKr9TaAcqURAey1MaX00Rv6)

[规划控制&轨迹预测大专栏](https://www.zdjszx.com/p/t_pc/goods_pc_detail/goods_detail/course_2WmTf6RRZcWqT43ttRMnDBlSKGw)
