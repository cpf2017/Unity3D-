# UI框架的作用
1. 加载，显示，隐藏，关闭页面，根据标示获得相应界面实例 
2. 提供界面显示隐藏动画接口 
3. 单独界面层级，Collider，背景管理 
4. 根据存储的导航信息完成界面导航 
5. 界面通用对话框管理(多类型Message Box)
6. 便于进行需求和功能扩展(比如，在跳出页面之前添加逻辑处理等)

# UI框架的搭建方法

1. 创建一个叫**UIGame**的类用来封装UI物体对象（此类不用继承MonoBehaviour类）：
* （1）声明一个UI物体对象；
* （2）用属性封装UI物体对象的名字；
* （3）用bool属性来判断UI是否激活；
* （4）用构造函数构件UI；
```c
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
/*
*****************************
创建时间：2017-6-30 10:5:25
创建人：夏洛克丶
邮箱：396070677@qq.com
微信：18500467616
网址：www.newbieol.com
公司名称：菜鸟在线
*****************************
*/
public class UIGame  {

    //UI物体对象
    public GameObject UIObj;

    //UI名字
    public string Name
    {
        get {return UIObj.name; }
    }
    //UI是否显示
    public bool Visible
    {
        get { return UIObj.activeInHierarchy; }
        set { UIObj.SetActive(value); }
    }
    //构建UI
    public UIGame(string name)
    {
        UIObj = GameObject.Instantiate(Resources.Load("UI/" + name)) as GameObject;
        if (UIObj != null)
        {
            UIObj.name = name;
            UIObj.AddComponent(System.Type.GetType(name + "Handler"));
            UIObj.SetActive(false);

        }
    }
}
```

2. 创建一个叫**UIName**的类用来封装UI物体对象的名字（此类不用继承MonoBehaviour类）
```c
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
/*
*****************************
创建时间：2017-6-30 10:23:0
创建人：夏洛克丶
邮箱：396070677@qq.com
微信：18500467616
网址：www.newbieol.com
公司名称：菜鸟在线
*****************************
*/
public class UIName  {


    public const string UIHome = "UIHome";
    public const string UIMap = "UIMap";
    public const string UIStage = "UIStage";

    public const string UILevel = "UILevel";
}
```

3. 创建一个叫**UIGameManager**的类用来封装操作UI流程的代码（此类不用继承MonoBehaviour类）
* （1）创建UIGame这个类的对象；
* （2）写一个将UI添加到列表里的方法；
* （3）写一个UIGame类型的方法用来寻找列表里的方法；
* （4）写一个显示UI的方法；
* （5）写一个隐藏UI的方法；
* （6）用单例模式让这个类的对象唯一；
```c
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
/*
*****************************
创建时间：2017-6-30 10:13:2
创建人：夏洛克丶
邮箱：396070677@qq.com
微信：18500467616
网址：www.newbieol.com
公司名称：菜鸟在线
*****************************
*/
public class UIGameManager
{

    //单例模式
    private UIGameManager()
    {
    }
    private static UIGameManager _instance;
    public static UIGameManager instance
    {
        get {
            if (_instance == null)
            {
                _instance = new UIGameManager();
            }
            return _instance;
        }
    }



    List<UIGame> UIGameList = new List<UIGame>();
    //添加UI到列表
    public void AddUI(string name,bool visible = false)
    {
        UIGame gui = new UIGame(name);
        if (gui != null)
        {
            gui.Visible = visible;
            UIGameList.Add(gui);
        }
    }
    //通过名字寻找列表里的UI
    UIGame GetByUIGame(string name)
    {
        for (int i = 0; i < UIGameList.Count; i++)
        {
            if (UIGameList[i].Name == name)
            {
                return UIGameList[i];
            }
        }
        return null;
    }
    // 显示UI
    public void ShowUI(string name)
    {
        UIGame gui = GetByUIGame(name);
        if (gui != null)
        {
            gui.Visible = true;
        }
    }
    // 隐藏UI
    public void HideUI(string name)
    {
        UIGame gui = GetByUIGame(name);
        if (gui != null)
        {
            gui.Visible = false;
        }
    }


}
```

4. 创建一个叫**StartUIGameManager**的类用来执行代码（此类需要继承MonoBehaviour类）
* （1）声明一个UIGameManager类类型的变量

```c
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
/*
*****************************
创建时间：2017-6-30 10:24:39
创建人：夏洛克丶
邮箱：396070677@qq.com
微信：18500467616
网址：www.newbieol.com
公司名称：菜鸟在线
*****************************
*/
public class StartUIGameManager : MonoBehaviour {

    public UIGameManager uimgr;
	void Awake ()
    {
        uimgr = UIGameManager.instance;
	}
    void Start()
    {
        uimgr.AddUI(UIName.UIHome, true);
        uimgr.AddUI(UIName.UIMap);
        uimgr.AddUI(UIName.UIStage);

        uimgr.AddUI(UIName.UILevel);
    }
	// Update is called once per frame
	void Update () {
		
	}
  ```
  * 本章纯属新人胡乱总结，如有错误，望请指出。
