# GameplayFramework
GameplayFramework for CocosCreator Instant Games  
The HTML form of the documentation can be found on: [https://huangx916.github.io/2019/01/01/gameplayframework/](https://huangx916.github.io/2019/01/01/gameplayframework/)

来源：https://huangx916.github.io/2019/01/01/gameplayframework/

项目工程目录细分

游戏引擎一般都会提供一个开发过程中存放各种资源的文件夹(如creator、u3d的assets，ue4的content等)。我们首先需要了解特定文件夹的作用，如resources。然后在assets下细分各种资源建立相应的文件夹，并告知美术人员。好处就是清晰、一目了然，模块化的texture创建AutoAtlas后更能减少drawcall以及防止未使用功能的资源提前下载载入内存。各个游戏资源划分大同小异 

框架使用简介

GameMain

游戏入口，挂Canvas下。

所有管理类使用单例模式，使用getInstance()获取实例。

AudioManager

音效及背景音乐管理类，负责游戏音乐音效开关，状态可在GameData中序列化保存。

ConfigManager

配置文件管理类，配置文件使用json格式存储，通过继承BaseConfigContainer，反序列化json文件数据。然后交给ConfigManager统一管理。

GameController

游戏控制类，负责游戏初始化、场景跳转等。

GameDataManager

数据管理类，所有游戏数据存放在GameData中，视图层可通过GameDataManager进行数据读写操作。

ListenerManager

监听管理类，观察者模式，解耦调用视图层。
UI中注册：ListenerManager.getInstance().add(ListenerType.GameStart, this, this.onGameStart);
管理类中触发：ListenerManager.getInstance().trigger(ListenerType.GameStart);

TimeManager

时间管理类，可获取系统当前时间(单位毫秒)

UIManager

UI管理类，可通过类名打开、关闭、显示、隐藏、获取对应UI。 UI类需继承BaseUI
打开：UIManager.getInstance().openUI(LoadingUI);
关闭：UIManager.getInstance().closeUI(LoadingUI);
获取:let tipUI = UIManager.getInstance().getUI(TipUI) as TipUI

Shader

感谢小伙伴的分享，就不重造轮子了。
ShaderComponent挂到Sprite下，选择自定义的Shader
ShaderLab中添加自定义Shader
ShaderManager
ShaderMaterial 

Utils

MathExtension数学扩展库
StringExtension字符串格式化
UIHelpTip提示

Others

自定义*.d.ts编码提示等
