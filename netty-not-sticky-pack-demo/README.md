# netty-not-sticky-pack-demo

## ���tcp�������ݣ�ճ������  
�Ƚ������Ľ�����������¼��֣�  
1����Ϣ���������Ĵ�С�̶����ȣ�����ÿ�����ĵĳ��ȹ̶�Ϊ200�ֽڣ����������λ���ո�  
2����β��������ָ���������ÿ�����Ľ��������ӻس����з�������FTPЭ�飩����ָ�������ַ���Ϊ���ķָ��������շ�ͨ������ָ����зֱ������֣�  
3������Ϣ��Ϊ��Ϣͷ����Ϣ�壬��Ϣͷ�а�����ʾ��Ϣ���ܳ��ȣ�������Ϣ�峤�ȣ����ֶΣ�  
4���Զ�������ӵ�Ӧ�ò�Э�顣  

## Nettyճ���Ͳ���������
Netty�ṩ�˶�������������Խ��зְ��Ĳ������ֱ��ǣ�  
LineBasedFrameDecoder  
DelimiterBasedFrameDecoder����������ָ����������ְ���  
FixedLengthFrameDecoder��ʹ�ö����ı������ְ���  
LengthFieldBasedFrameDecoder  

## LengthFieldBasedFrameDecoder
��ʵ��ʹ��LengthFieldBasedFrameDecoder����TCP�ײ�Ĳ����ճ������  
ʹ�ö�����д���  
LengthFieldBasedFrameDecoder�Ĺ��캯����  
``java
public class LengthFieldBasedFrameDecoder extends ByteToMessageDecoder {
    //...
  public LengthFieldBasedFrameDecoder(ByteOrder byteOrder, 
                                    int maxFrameLength, 
                                    int lengthFieldOffset, 
                                    int lengthFieldLength, 
                                    int lengthAdjustment, 
                                    int initialBytesToStrip, 
                                    boolean failFast) {
   }
   //...
}
```
byteOrder����ʾ�ֽ�����ʾ�������Ǵ�˻���С�ˣ���ΪNettyҪ��ȡLength�ֶε�ֵ�����Դ��С��Ҫ���úã�Ĭ��Netty�Ǵ����ByteOrder.BIG_ENDIAN��  
maxFrameLength����ʾ���ǰ�����󳤶ȣ�����������󳤶�netty���ᱨ����  
lengthFieldOffset��ָ���ǳ�����Length����ƫ��������ʾ����ָ�����ȸ��ֽ�֮��Ĳ��ǳ�����Ҳ����lengthǰ����ֽڣ�Ҳ����ͷ����Ϣ��  
lengthFieldLength����¼��֡���ݳ��ȵ��ֶα����ĳ��ȣ�  
lengthAdjustment�����ֶμӳ����ֶε�������֡�ĳ��ȣ����峤�ȵ����Ĵ�С�����������ֵ��ʾ�ĳ��ȼ����������ֵ��ʾ�ľ��Ǵ�header�İ���  
initialBytesToStrip��������֡���������ֽ�������ʾ��ȡ��һ�����������ݰ�֮�󣬺���ǰ���ָ����λ�����ֽڣ�Ӧ�ý������õ��ľ��ǲ�������������ݰ���  
failFast�����Ϊtrue�����ʾ��ȡ��������TA��ֵ�ĳ���maxFrameLength�����׳�һ�� TooLongFrameException����Ϊfalse��ʾֻ�е�������ȡ�곤�����ֵ��ʾ���ֽ�֮�󣬲Ż��׳� TooLongFrameException��Ĭ�����������Ϊtrue�����鲻Ҫ�޸ģ�������ܻ�����ڴ������  


## ʲô��ճ���������
����ʲô��ճ����������⣬�����Ⱦ������򵥵�Ӧ�ó�����  
�ͻ��˺ͷ���������һ�����ӣ��ͻ��˷���һ����Ϣ���ͻ��˹ر������˵����ӡ�  
�ͻ��˺ͷ���������һ�����ӣ��ͻ�����������������Ϣ���ͻ��˹ر������˵����ӡ�  
���ڵ�һ�����������˵Ĵ������̿����������ģ����ͻ��������˵����ӽ����ɹ�֮�󣬷���˲��϶�ȡ�ͻ��˷��͹��������ݣ����ͻ������������ӶϿ�֮�󣬷����֪���Ѿ�������һ����Ϣ��Ȼ����н���ͺ�������...��  
���ڵڶ���������������������ͬ�Ĵ����߼����������Ǿ���������  
�����������ڶ�������¿ͻ��˷��͵�������Ϣ�ݽ���������п��ܳ��ֵ������

��һ�������  
�����һ�������������ݰ�����һ���������ͻ��˷����ĵ�һ����Ϣ��������Ϣ���ڶ����������ͻ��˷����ĵڶ�����Ϣ������������ȽϺô�����������ֻ��Ҫ�򵥵Ĵ����绺����ȥ���ͺ��ˣ���һ�ζ�����һ����Ϣ��������Ϣ���������ٴ����绺�������ڶ���������Ϣ���������ѡ�

![û�з���ճ�������ʾ��ͼ  ](http://blogimg.chenhaoxiang.cn/18-8-14/79484782.jpg)  
û�з���ճ�������ʾ��ͼ  

�ڶ��������  
�����һ���Ͷ���һ�����ݰ���������ݰ������ͻ��˷�����������Ϣ��������Ϣ�����ʱ�����֮ǰ�߼�ʵ�ֵķ���˾����ˣ���Ϊ����˲�֪����һ����Ϣ���Ķ������͵ڶ�����Ϣ���Ķ���ʼ�����������ʵ�Ƿ�����TCPճ����  
![TCPճ��ʾ��ͼ](http://blogimg.chenhaoxiang.cn/18-8-14/66480317.jpg)  
   TCPճ��ʾ��ͼ  

�����������  
�����һ���յ����������ݰ�����һ�����ݰ�ֻ�����˵�һ����Ϣ��һ���֣���һ����Ϣ�ĺ�벿�ֺ͵ڶ�����Ϣ���ڵڶ������ݰ��У������ǵ�һ�����ݰ������˵�һ����Ϣ��������Ϣ�͵ڶ�����Ϣ��һ������Ϣ���ڶ������ݰ������˵ڶ�����Ϣ��ʣ�²��֣����������ʵ�Ƿ�����TCP����Ϊ������һ����Ϣ����������������淢���ˣ�ͬ������ķ������߼�������������ǲ��ô����ġ�  
![TCP���ʾ��ͼ](http://blogimg.chenhaoxiang.cn/18-8-14/58508223.jpg)  
TCP���ʾ��ͼ  
�������ֲο����� [https://my.oschina.net/andylucc/blog/625315](https://my.oschina.net/andylucc/blog/625315)  








