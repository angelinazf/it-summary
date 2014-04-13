### Unity3d调用OC
Unity3d代码,随便找个类,这个没有限制的
##### unity3d代码定义
  在某个cs里面
```
public class FvzIapTest : MonoBehaviour {
    //Unity3d调用OC定义
    [DllImport("__Internal")]
    private static extern void FvzCallFromCSharp(string inStr);
    void OnEnable() {
        //Unity3d代码调用
#if !UNITY_EDITOR && UNITY_IPHONE
        FvzCallFromCSharp("hello ObjectC!");
        Debug.Log("[FvzIapTest] finish");
#else
        Debug.Log("[FvzIapTest] not iphone runtime");
#endif
    }
}
```

##### OC代码定义
在某mm文件里面,必须放在./Assets/Plugin/iOS目录下
```
extern "C" {
  void FvzCallFromCSharp(const char* inStr){
    NSLog(@"FvzCallFromCSharp %@",FvzCharArrayToNSString(inStr));
  }
}
```

### OC调用Unity3d
含义分别是场景中gameobject名,某个对象的方法名,第一个字符串参数
```
    UnitySendMessage("FvzIapTest","onFvzCallFromObjectC","Hello Unity3d");
```