# Remote-Desktop-Manager 解密

RDM 使用 DES3 加密，加密秘钥仅与连接类型有关，解密函数:

```
def decrypt(data, conn_type):
    known_keys = {
        'ssh': '{D6037472-976A-4EAB-8135-DE779F4EDF29}',
        'rdp': '{9E6D0FD3-AD2B-4fe1-BBAC-F520BF2F1AE1}'
    }

    data = base64.b64decode(data)
    key  = known_keys[conn_type]

    des = DES3.new(md5(key), DES3.MODE_ECB)
    return des.decrypt(data)
```    

