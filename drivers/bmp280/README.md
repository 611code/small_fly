# bmp280使用流程



### cubemx配置：

只需要配置i2c即可



main.c中函数

```
double pow(double X,double Y);
double data_conversion(double air_pressure,double temperature)
{
    double conversion_alt;
    conversion_alt=(pow(101325/air_pressure,1/5.257)-1)*temperature/0.0065f;
    return conversion_alt;
}
```



使用：

定义：

```
double Alt;
bmp280_params_t  params;
BMP280_HandleTypedef bmp280_dev;
float pressure, temperature, humidity;
bmp280_init_default_params(&params); //BMP280模块配置参数。
bmp280_dev.addr = BMP280_I2C_ADDRESS_0;
bmp280_dev.i2c = &hi2c1;
bmp280_init(&bmp280_dev, &params);    
bool bme280p = bmp280_dev.id == BME280_CHIP_ID;
```

使用。打印信息为压力（pa），温度，高度（海拔）

```
while (1)
  {
		bmp280_read_float(&bmp280_dev, &temperature, &pressure, &humidity);
    Alt=data_conversion(pressure,temperature);
        printf("Pressure: %.2f Pa, Temperature: %.2f C, Alt:%.3f m\r\n", pressure, temperature,Alt);
		if (bme280p)
			printf(", Humidity: %.2f\n", humidity);
		else
			printf("\n");
		HAL_GPIO_TogglePin(GPIOC, GPIO_PIN_13);
		HAL_Delay(500);
  }
```

