# Json
## JsonUtility
<img width="374" height="70" alt="Image" src="https://github.com/user-attachments/assets/01ee836f-44ba-4364-9e24-405d1d052036" />

### 序列化
**`JsonUtility.ToJson(data)`**
把内存中的数据存储到硬盘上

把一串类对象的数据序列化为Json字符串
这个Json字符串可以写入硬盘中

<img width="556" height="353" alt="Image" src="https://github.com/user-attachments/assets/604c9d0e-1209-4514-bff1-edaef08cb80c" />


<img width="432" height="117" alt="Image" src="https://github.com/user-attachments/assets/27a830e0-ad4d-4f96-836e-2f9266871001" />

### 反序列化
**`JsonUtility.FromJson<FireInfo>(字符串);`**
把硬盘的数据读取到内存中

读取文件中的Json字符串
```c#
string readFileInfo  = File.ReadAllText(Application.streamingAssetsPath + "/FireData2.json");
print(readFileInfo);//正常读取
```
使用Json字符串内容 反序列化转换成类对象
`FireInfo fireData = JsonUtility.FromJson<FireInfo>(readFileInfo);`

注意必须是对象，如果想直接反序列数据结构得把这个数组再包裹一层对象
注意json文件必须是UTF-8

## LitJson
### 序列化
```c#
string strJson = JsonMapper.ToJson(p);
File.WriteAllText(Application.persistentDataPath + "/" + fileName + ".json", strJson);//写进json文件
```

### 反序列化
```c#
string strJson = File.ReadAllText(Application.persistentDataPath + "/" + fileName + ".json");
JsonMapper.ToObject<PlayerInfo2>(strJson);
```
LitJson虽然支持字典但是
注意键如果是int类型，会出问题，因为json里面默认转成字符串，再次读取数据之后反序列化会出问题因为无法创建int类型的键

<img width="373" height="92" alt="Image" src="https://github.com/user-attachments/assets/33181a4f-c354-4cf7-9bd3-62f9ecf0d18f" />

<img width="592" height="171" alt="Image" src="https://github.com/user-attachments/assets/9de68222-5854-4c17-8d8b-cae22ce102db" />