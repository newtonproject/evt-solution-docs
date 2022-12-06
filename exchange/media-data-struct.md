## 媒体资源数据结构

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
- type: evt类型，目前有 movie/series 两种
- name: evt 名称
- description: 描述
- image: 封面图 ipfs 地址
- playlist: 播放资源列表
- expire_date: 电影版权到期时间

