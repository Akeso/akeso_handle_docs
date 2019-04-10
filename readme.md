# 对外开放接口

1. 测试服域名:staging.akeso.com.cn
2. 正式服域名:akeso.com.cn


AKESO_NEW OPEN API文档
#### <a href="#users_device">绑定镜腿</a>
#### <a href="#uploads_data">同步数据</a>
#### <a href="#forecasts_options">近视预测条件</a>
#### <a href="#forecasts_search">近视预测查询</a>

## <a name="users_device">绑定镜腿</a>
```ruby
POST http://hostname/api/open/users/device
```
### Request

```ruby
# HEADERS
Content-type: "application/json"

# BODY
{
    "phone": "电话",
    "mac_address": "mac地址",
    "device_type": "版本号",
    "uuid": "uuid值"
}
```
### Response

#### 正确结果

```ruby
# BODY
{
    "status":200,
    "message":"绑定成功",
    "data":{
        "child_id”: 1
    }
}
```

## <a name="uploads_data">同步数据</a>
```ruby
POST http://hostname/api/open/uploads
```
### Request

```ruby
# HEADERS
Content-type: "application/json"

# BODY
{
    "child_id": "儿童id",
    "records": "采集到的数据",
    "electricity": "电量"
}
```
### Response

#### 正确结果

```ruby
# HTTP CODE
200

# BODY
{
    "status": 200,
    "message": "请求成功",
    "data": {
        "count":3
    }
}
```

## <a name="forecasts_options">近视预测条件</a>
```ruby
GET http://hostname/api/v5/forecasts/options
```
### Request

```ruby
# HEADERS
Content-type: "application/json"

# BODY
{}
```
### Response

#### 正确结果

```ruby
# HTTP CODE
200

# BODY
{
    "status": 200,
    "message": "请求成功",
    "data": {
        "age_start_options": [6, 7, 8...],
        "re_options": [
            {
                "key": "50度",
                "value": -0.5
            },
            {
                "key": "100度",
                "value": -1
            }...
        ],
        "ctrl_type_options": [
            {
                "key": "普通框架眼镜",
                "value": 9
            },
            {
                "key": "多焦点软性隐形眼镜",
                "value": 0
            }...
        ],
        "health_data_options": [
            {
                "key": "优（120以上）",
                "value": 40
            },
            {
                "key": "良（80~120分）",
                "value": 30
            }...
        ]
    }
}
```

## <a name="forecasts_search">近视预测查询</a>
```ruby
GET http://hostname/api/v5/forecasts
```
### Request

```ruby
# HEADERS
Content-type: "application/json"

# BODY
{
    age_start: '年龄 6,7,8',
    re: '近视度数 -0.5, -1',
    ctrl_type: '防控方式 9, 0',
    health_data: '健康评分 40, 30'
}
```
### Response

#### 正确结果

```ruby
# HTTP CODE
200

# BODY
{
    "status": 200,
    "message": "请求成功",
    "data": {
        "no_ctrl_data": [50, 205,315,415,500,575,645,705,760,815,875,930],
        "ctrl_data_default": [50,85,125,165,195,215,235,245,250,250,245,235],
        "ctrl_data_section": [0,40,55,70,85,100,115,135,155,185,225,260],
        "ctrl_data_default_top": [50,125,180,235,280,315,350,380,405,435,470,495],
        "ctrl_akeso_data": [50,125,185,235,280,320,350,380,410,440,470,500],
        "ctrl_rate": 49
    }
}
```

