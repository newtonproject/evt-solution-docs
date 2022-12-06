# NewKeeper Api 



**请求地址**: `https://newkeeper.testnet.newtonproject.org/api/v1/evt/check/`

**请求参数**:

> 生成随机字符串作为  `message`,  使用 newton 钱包进行签名  ``



**header** 

| 名称          | 类型   | 说明                     |
| ------------- | ------ | ------------------------ |
| content-type  | string | application/json         |
| Authorization | string | 对 post 参数进行排序签名 |

#### params

| 参数             | 类型   | 说明                                             |
| ---------------- | ------ | ------------------------------------------------ |
| contract_address | string | EVT 合约地址                                     |
| sign_r           | string | 签名结果 r                                       |
| sign_s           | string | 签名结果 s                                       |
| sign_v           | string | 签名结果 v                                       |
| sign_message     | string | 使用`app_secret` 对 `message` 进行`aes` 加密结果 |
| app_key          | string | 申请访问 `newkeeper` 的 app_key                  |
| timestamp        | int    | 请求时间戳，单位秒                               |

#### response

| 参数        | 类型   | 说明                            |
| ----------- | ------ | ------------------------------- |
| csm_version | string | CSM 版本号                      |
| private_key | string | 用app_secret aes加密后的加密key |



Python 版代码示例

```python
import urllib
import base64
import datetime
from Crypto.Cipher import AES
from eth_account.messages import encode_defunct
from utils import newton_web3


# LIBS

'''
AES ENCRYPT
'''
# 
def add_to_16(value):
    while len(value) % 16 != 0:
        value += '\0'
    return str.encode(value)  # 返回bytes
# AES ENCRYPT
def aes_encrypt(key, text):
    aes = AES.new(add_to_16(key), AES.MODE_ECB)  # 初始化加密器
    encrypt_aes = aes.encrypt(add_to_16(text))  # 先进行aes加密
    encrypted_text = str(base64.encodebytes(encrypt_aes), encoding='utf-8')  # 执行加密并转码返回bytes
    return encrypted_text
# AES DECRYPT
def aes_decrypt(key, text):
    aes = AES.new(add_to_16(key), AES.MODE_ECB)  # 初始化加密器
    base64_decrypted = base64.decodebytes(text.encode(encoding='utf-8'))  # 优先逆向解密base64成bytes
    decrypted_text = str(aes.decrypt(base64_decrypted), encoding='utf-8').replace('\0', '')  # 执行解密密并转码返回str
    return decrypted_text

def sign_hmac(data, secret, prefix='', use_urlencode=False, joint='&'):
    data = collections.OrderedDict(sorted(data.items()))
    sign_string = prefix
    n = 0
    for k, v in data.items():
        if n != 0 and k != 'sign':
            sign_string += joint
        n += 1
        if k != 'sign':
            sign_string += u'%s=%s' % (k, v)
    sign_string += secret
    if use_urlencode:
        sign_string = urllib.quote_plus(sign_string)
    signed_string = generate_digest(sign_string)
    return signed_string
  
  


wallet_private_key = '0x...'
message = 'abcdefgjkqwerrttyuio' # 随机生成，不要纯数字，也不要十六进制字符串

w3 = newton_web3.get_web3()
signable_message = encode_defunct(text=message)
signed_message = w3.eth.account.sign_message(signable_message, private_key=wallet_private_key)

app_key = '...'
app_secret = '...'

data = {
    'contract_address': '0x...',
    'token_id': '111',
    'sign_r': hex(signed_message.r),
    'sign_s': hex(signed_message.s),
    'sign_v': signed_message.v,
    'sign_message': aes_encrypt(app_secret, message),
    'app_key': app_key,
    'timestamp': time.time(),
}

generate_sign = sign_hmac(data, app_secret)
headers = {
    'content-type': 'application/json',
    'Authorization': generate_sign,
}
api_url = 'https://newkeeper.testnet.newtonproject.org/api/v1/evt/check/'
response = requests.post(api_url, data=json.dumps(data), headers=headers)
result = json.loads(response.text)
if result['error_code'] == 1:
    csm_version = result['result']['csm_version']
    private_key = result['result']['private_key']
    private_key = aes_decrypt(app_secret, private_key)

```

