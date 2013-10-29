发GET请求
```
	void OnGUI () {	
    StartCoroutine(clickButton());
  }
	IEnumerator clickButton(){
		output.text+="start network\n";
		WWW net=new WWW("http://127.0.0.1:15600");
		output.text+="finish new\n";
		yield return net;
		output.text+="net.isDone="+net.isDone.ToString()+"\n";
		output.text+="finish LoadUnityWeb\n";
		output.text+=net.text;
	}
```