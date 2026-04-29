# AudioSource音频相关
## 音频切片
```c#
AudioSource audioSource;
public GameObject obj;
public AudioClip clips;
void Start()
{
   audioSource = GetComponent<AudioSource>();
   //Instantiate(obj);
   AudioSource aus = this.AddComponent<AudioSource>();
   aus.clip = clips;
   aus.Play();
}
```

## 音频的播放与暂停
```c#
if(Input.GetKeyDown(KeyCode.P))
{
    //播放音频
    audioSource.Play();
    //延迟五秒播放
    //audioSource.PlayDelayed(5);
}
if(Input.GetKeyDown(KeyCode.S))
{
    //停止音频
    audioSource.Stop();
}
if(Input.GetKeyDown (KeyCode.Space))
{
    //暂停
    audioSource.Pause();
}
if (Input.GetKeyDown(KeyCode.X))
{
    //停止暂停
    audioSource.UnPause();
}

//检测是否播放中
if (audioSource.isPlaying)
{
    print("正在播放");
}
else
{
    print("播放结束");
}
```