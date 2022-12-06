## tokenUri 解析

#### token_uri 解析出的 metajson 格式

```python
{
    'version': '0.2',
    'type': 'movie',
    'name': '',
    'description': '',
    'image': 'ipfs://xxxxxxx',
    'playlist': [
        {
            'path': 'movie.m3u8',
            'cid': 'ipfs://QmREXWCuxPrWUB5QfCZxzZ8WXuYfBqhi58ooxe5qfz2VLL',
            'running_time': 7200
        }
    ],
    'expire_date': '2022-08-29T00:00:00'
}
```

- version: 版本
- type: evt类型，目前有 movie/seris 两种
- name: evt 名称
- description: 描述
- image: 封面图 ipfs 地址
- playlist: 播放资源列表
- expire_date: 电影版权到期时间


#### demo

``` python
import requests
import json
from web3 import Web3, HTTPProvider

IPFS_EVT_HOST = f'https://cf-ipfs.wavemall.io/ipfs/'
rpc_url = 'https://rpc1.newchain.newtonproject.org/'
evt_address = ''
with open('contract_abi.json', 'rb') as f:
    contract_abi = json.load(f)

w3 = Web3(HTTPProvider(rpc_url))
evt_contract = w3.eth.contract(address=evt_address, abi=contract_abi)
token_uri = evt_contract.functions.defaultURI().call()
url = IPFS_EVT_HOST.rstrip('/') + '/' + token_uri.split('//')[-1]
token_info = requests.get(url).json()

evt_name = token_info.get('name', '')
evt_description = token_info.get('description', '')
evt_image = token_info.get('image', '')
evt_type = token_info.get('type')
playlist = token_info.get('playlist', [])

```


