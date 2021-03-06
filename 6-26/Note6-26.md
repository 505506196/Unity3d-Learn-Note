#Unity3D基础组件对象

一、**MonoBehaviour** 脚本：
=================================
**Unity**引擎的所有脚本类对象都必须来自`MonoBehaviour`的继承关系;
`MonoBehaviour`是**Unity**引擎中非常重要的实时运行对象，他是所有游戏对象中组件 的唯一执行类，所以他是一定的执行顺序，并且这样执行方法是特定的不能随意改动：

1. **`void Awake()`** : <br/>
  只在脚本挂在游戏个体上执行 ；
  >__注意：__ 只会执行一次

2. **`void Start()`** : <br/>
  只在更新函数之前执行一次 ；
  >__注意：__ 在Awake之后

3. **`void FixedUpdate()`** : <br/>
  固定化更新，默认的时候是每0.02秒执行一次 ；
  >__注意：__ 主要是用来更新物理函数.

4. **`void Update()`** : <br/>
  更新函数 ；
  >__注意：__ 只要这个游戏个体存在他就会永远执行下去，直到他被删除或者工程停止，更新函数才会停止

5. **`void LateUpdate()`** : <br/>
  稍后更新 ；
  >__注意：__ 他是在 Update 函数之后执行，而且也是永远执行.主要是用来处理摄像机操作的，滞后操作可以保证画面的稳定性.

6. **`void OnDestroy()`** : <br/>
  销毁函数，当我们删除一个游戏个体或者删除当前脚本的时候，他就执行了；

以上为`MonoBehaviour`类的特定方法，并且是按照这个顺序执行的；

`MonoBehaviour`脚本存在__失活__和__激活__两种状态：
* __失活__ : 失去了活性，所以更新函数和状态函数都不执行了，但是并不代表他被销毁了，所以他的销毁函数绝对不会执行，并且他永远保持着内存占用；
* __激活__ : 让这个脚本的所有更新函数和状态函数立即恢复事件监听；

对于当前脚本的 __失活__/__激活__ 我们可以对脚本中的`enable`属性进行`true`（__激活__）、`false`（__失活__）的设定；
>__注意：__ 失活后所有的更新函数都会终止，只能通过外界方法再次激活当前脚本；

二、**GameObject** 类
==================================
`GameObejct`类是**Unity**引擎中表示每个游戏个体的主类，他可以操作每个游戏个体上的所有组件 ；

1. __作为搜索游戏个体:__

  * `GameObject Find(string name)` : <br/>
    通过游戏个体的名称直接找到游戏个体实体，只能找一个。
    >__注意：__ 游戏个体的名字是可以重复的，会导致找到的游戏个体并不是你想要的；

  * `GameObejct FindWithTag(string tag)` : <br/>
    通过游戏个体的标签来找到实体对象，只能找一个。 
    >__注意：__ 游戏个体的标签也是可以重复的；

  * `GameObject[] FindGameObjectsWithTag(string tag)` : <br/>
    通过游戏个体的标签来找到实体对象，当前场景全部带有这个标签的游戏个体；
    >__注意：__ 这个搜索只能搜索根目录的内容，不能搜索子对象。对于子目录你需要指定相应的父目录，才可以再搜索；

  __总结：__ 这个搜索函数效率非常低下，不建议这样使用，我们可以通过外界参数的方法来调用；

2. __控制游戏个体的组件:__

  * 增加组件 `T AddComponent<T>()` : <br/>
    通过泛型来增加组件，返回已增加的组件实例化对象；

  * 获取组件 `T GetComponent<T>()` : <br/> 
    通过泛型获取指定类型的组件，获取一个；

  * 获取所有组件 `T[] GetComponents<T>()` : <br/>
    通过泛型获取指定类型的组件，获取所有这个类型的组件；

  * 滞后删除组件 `GameObject.Destroy(Object pComponent, float time)` : <br/>
    删除指定的组件，须要你知道组件 的实例化对象，`time`是表示在规定的秒数之后删除， `time`可以不写，不写下一帧后删除；

  * 立即删除组件 `GameObject.DestroyImmediate(Object pComponent)` : <br/>
    当前语句表示立刻将组件删除，不会产生滞后；

  >__注意：__ <br/>
  >  * 对于增加组件 : 我们只能一个一个的增加，每增加一个组件，组件的`Awake`都会执行一次，所以只能一个个增加。
  >  * 对于删除组件 ：`Update`函数之前执行的函数都需要使用滞后删除，立即删除会造成更新函数失败，程序会报空。更新函数可以直接立即删除；

3. __游戏个体的激活和失活:__

  * 游戏个体不会是和脚本的活性设置一样，他需要通过特定函数来操作
  `void SetActive(bool on)` :<br/>
    `false` ：表示失活，游戏失活后他底下所有的组件全部失活；<br/>
    `true` ： 表示激活游戏个体，表示他底下的所有组件除了组件自己失活外都会再次被激活；

  * 判断游戏个体的活性 
  `activeSelf` : <br/>
    属性获取的，这个属性只能`get`不能`set`；



