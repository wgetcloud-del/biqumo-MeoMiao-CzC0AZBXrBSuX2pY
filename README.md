

# 前言




  本篇编译osg3\.4\.0的msvc2017x64版本，之前使用的都是mingw32版本。



 

# OSG编译




## 步骤一：下载解压




  下载3\.4\.0版本。  ![在这里插入图片描述](https://img2024.cnblogs.com/blog/1971530/202412/1971530-20241202171527517-463320039.png)




## 步骤二：使用cmake配置




  ![在这里插入图片描述](https://img2024.cnblogs.com/blog/1971530/202412/1971530-20241202171527504-876148539.png)




  ![在这里插入图片描述](https://img2024.cnblogs.com/blog/1971530/202412/1971530-20241202171527513-990639863.png)




  ![在这里插入图片描述](https://img2024.cnblogs.com/blog/1971530/202412/1971530-20241202171527521-1342875338.png)




  因为是64位，可以通过后续配置cmake用x64，也可以直接选择构架：  ![在这里插入图片描述](https://img2024.cnblogs.com/blog/1971530/202412/1971530-20241202171527474-1065742102.png)




  继续：  ![在这里插入图片描述](https://img2024.cnblogs.com/blog/1971530/202412/1971530-20241202171527486-277028873.png)




  要修改下安装的路径，方便提取库：  ![在这里插入图片描述](https://img2024.cnblogs.com/blog/1971530/202412/1971530-20241202171527864-167646528.png)




  默认是32位，发现后续vs更改不行，得在cmake处更改，查看“入坑一”，修改如下图：  ![在这里插入图片描述](https://img2024.cnblogs.com/blog/1971530/202412/1971530-20241202171527923-1682065552.png)




  修改后需要重新configure。




## 步骤三：生成工程




  ![在这里插入图片描述](https://img2024.cnblogs.com/blog/1971530/202412/1971530-20241202171527929-61175621.png)




  ![在这里插入图片描述](https://img2024.cnblogs.com/blog/1971530/202412/1971530-20241202171527905-2112406069.png)




## 步骤四：打开vs2017打开工程




  ![在这里插入图片描述](https://img2024.cnblogs.com/blog/1971530/202412/1971530-20241202171527818-1346548868.png)




  装了多个vs，可能会打开错误，如果打开不是使用vs2017就自行使用  ![在这里插入图片描述](https://img2024.cnblogs.com/blog/1971530/202412/1971530-20241202171527749-569645375.png)




## 步骤五：VS2017编译




  编译debug版本，先创建x64版本  ![在这里插入图片描述](https://img2024.cnblogs.com/blog/1971530/202412/1971530-20241202171527795-232248486.png)




  卡住了，等一会儿：  ![在这里插入图片描述](https://img2024.cnblogs.com/blog/1971530/202412/1971530-20241202171527773-852206723.png)




  然后编译：  ![在这里插入图片描述](https://img2024.cnblogs.com/blog/1971530/202412/1971530-20241202171527856-742308403.png)




  ![在这里插入图片描述](https://img2024.cnblogs.com/blog/1971530/202412/1971530-20241202171527826-142415219.png)




  编译release版本：  ![在这里插入图片描述](https://img2024.cnblogs.com/blog/1971530/202412/1971530-20241202171527845-1107921535.png)




  ![在这里插入图片描述](https://img2024.cnblogs.com/blog/1971530/202412/1971530-20241202171527899-1673072549.png)




  ![在这里插入图片描述](https://img2024.cnblogs.com/blog/1971530/202412/1971530-20241202171527895-808808856.png)




## 步骤六：安装到目标位置




  安装debug版本：  ![在这里插入图片描述](https://img2024.cnblogs.com/blog/1971530/202412/1971530-20241202171527884-1509550104.png)




  ![在这里插入图片描述](https://img2024.cnblogs.com/blog/1971530/202412/1971530-20241202171527867-1319028271.png)




  安装release版本：  ![在这里插入图片描述](https://img2024.cnblogs.com/blog/1971530/202412/1971530-20241202171528091-1661265397.png)




  ![在这里插入图片描述](https://img2024.cnblogs.com/blog/1971530/202412/1971530-20241202171527891-453259703.png)




  检查install的文件：  ![在这里插入图片描述](https://img2024.cnblogs.com/blog/1971530/202412/1971530-20241202171527873-941856057.png)



 

## OSG原Demo迁移




  移植Demo过来，复现过去的两个bug，一个是从相机旋转中心，一个是球体透明截面  测试都使用纯C\+\+原始代码修改，非自建的引擎，也不是osgQt。  ![在这里插入图片描述](https://img2024.cnblogs.com/blog/1971530/202412/1971530-20241202171527849-366303439.png)



 

# :[veee加速器官网](https://youhaochi.com)入坑




## 入坑一：模块计算机类型“x86”与目标计算机类型“x64”冲突




### 问题




  这是个常规问题了，关键在于已经设置了x64怎么出来还是x86\_32，好几年没弄，又卡了一下。  ![在这里插入图片描述](https://img2024.cnblogs.com/blog/1971530/202412/1971530-20241202171527866-1250432394.png)




### 原因




  这是平台解决方案是x64，但是默认没有x64，还得新增配置，又由于新增解决方案卡住了，笔者就只新增活动方案，下面没点了，正确要勾选如下图：  ![在这里插入图片描述](https://img2024.cnblogs.com/blog/1971530/202412/1971530-20241202171527868-1597233645.png)




  经过测试还是不行，再往前退，在CMake配置得时候指定x64：  ![在这里插入图片描述](https://img2024.cnblogs.com/blog/1971530/202412/1971530-20241202171527897-938714390.png)




### 解决




  在CMake配置得时候指定x64：  ![在这里插入图片描述](https://img2024.cnblogs.com/blog/1971530/202412/1971530-20241202171527883-1015776554.png)




  然后重新再来一遍即可。




## 入坑二：编译运行直接异常




### 问题




  运行直接崩，一般是dll依赖缺少，检查了不缺。  ![在这里插入图片描述](https://img2024.cnblogs.com/blog/1971530/202412/1971530-20241202171527839-510601663.png)




### 尝试




  使用纯Qt程序，排除掉osg的，使用纯Qt程序，也是崩溃，本身Qt装的可能有问题，继续研究  ![在这里插入图片描述](https://img2024.cnblogs.com/blog/1971530/202412/1971530-20241202171527814-1631798674.png)




  新建了个新的是可以：  ![在这里插入图片描述](https://img2024.cnblogs.com/blog/1971530/202412/1971530-20241202171527772-646941084.png)




  怀疑是osg得shadow文件夹内部有问题，删掉shadow，再运行裸的只有界面的程序（去掉了osg的其他依赖）：  可以运行：  ![在这里插入图片描述](https://img2024.cnblogs.com/blog/1971530/202412/1971530-20241202171527910-1625548802.png)




  然后拷贝添加osg发现崩了，发现没有拷贝dll过去，检查脚本：  ![在这里插入图片描述](https://img2024.cnblogs.com/blog/1971530/202412/1971530-20241202171527804-581765122.png)




  有问题，以为是没复制过去覆盖32位的，复制过去也崩了，单独运行，还是0x7B错误，这是库连接错误，不理解了，后来经过dll对比，发现时间与32位一致，那么问题的原因就是晚上有点事，第二天上午才看，以为编了覆盖了64位的，实际没编译，install还是32位的，所以编译写程序还是连续时间比较好，第二天：  ![在这里插入图片描述](https://img2024.cnblogs.com/blog/1971530/202412/1971530-20241202171527916-769557518.png)




  重新编译并且install发现，时间还是没变，只好删除了build文件夹重新弄了，以为是粗心，结果不是，那么点击重新编译：  检查了是生成了：  ![在这里插入图片描述](https://img2024.cnblogs.com/blog/1971530/202412/1971530-20241202171527865-1064290870.png)




  但是install拷贝过去就是之前的时间：  ![在这里插入图片描述](https://img2024.cnblogs.com/blog/1971530/202412/1971530-20241202171527835-841522432.png)




  搞蒙了都（理论上一个build也可以更改参数然后install到不同文件夹，但是这里不管了）。




### 解决




  build全删掉，一刀切，从头新建build重新来一遍，确保生成了64位的并提取出来。  ![在这里插入图片描述](https://img2024.cnblogs.com/blog/1971530/202412/1971530-20241202171527841-1750986881.png)




  这里还少了release库，弄完好，再测是没问题了。



