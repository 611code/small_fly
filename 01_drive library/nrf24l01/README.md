

# NRF24L01使用流程

cubemx配置：

adc1双通道，dma传输，循环半字节，连续转换

![image-20250308171213911](C:\Users\34125\Desktop\github_小四轴\01_drive library\nrf24l01\README.assets\image-20250308171213911.png)



![image-20250308171121791](C:\Users\34125\Desktop\github_小四轴\01_drive library\nrf24l01\README.assets\image-20250308171121791.png)



定义（发送与接收都在这里）

```
extern uint16_t g_iAdcx[2];//缓存ADC采样值
uint8_t Send_Out[33]="本段数据来自NRF24L01发送端 ";//发送端
uint8_t Receive[33];//接收端
```

while前：

NRF24L01_TX_Mode();//设置为发送模式

NRF24L01_RX_Mode();//接收模式

```
while(NRF24L01_Check())
	{
		printf("111\r\n"); 
 		HAL_Delay(1000);
	}
	

	printf("222\r\n");

//	NRF24L01_TX_Mode();//设置为发送模式
//	NRF24L01_RX_Mode();//接收模式

  printf("333\r\n");
```

发送端：

	while (1)
	{	
		if(NRF24L01_TxPacket(Send_Out)==TX_OK)
	    {
	      printf("send_data：%s\r\n",Send_Out);
	    }
	    else
	    {
	      printf("send_error\r\n");
	    } 
	}

接收端：

```
while(1)
{
	if(NRF24L01_RxPacket(Receive)==0)
    {
      Receive[32]=0;//加入字符串结束符      
      printf("RECEIVE：%s\r\n",Receive);
    }
}
```

