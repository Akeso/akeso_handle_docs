# 对外开放接口

1. 测试服域名:staging.akeso.com.cn
2. 正式服域名:akeso.com.cn


AKESO_NEW OPEN API文档
#### <a href="#create_user">创建用户</a>
#### <a href="#exist_user">根据手机号查询用户是否存在</a>
#### <a href="#add_child">添加儿童</a>
#### <a href="#child_list">根据手机号或user_id获取儿童列表</a>
#### <a href="#users_device">绑定镜腿</a>
#### <a href="#unbind_device">解绑镜腿</a>
#### <a href="#uploads_data">同步数据</a>
#### <a href="#forecasts_options">近视预测条件</a>
#### <a href="#forecasts_search">近视预测查询</a>
#### <a href="#reports_health">眼健康</a>
#### <a href="#reports_daily">日报</a>
#### <a href="#reports_weekly">周报</a>
#### <a href="#reports_monthly">月报</a>

```
```

## <a name="create_user">创建用户</a>
```
POST http://hostname/api/open/users
```
### Request

```
# HEADERS
Content-type: "application/json"

# BODY
{
    "phone": "手机号",
    "name": "用户姓名"
}
```
### Response

#### 正确结果

```
# BODY
{
    "status":200,
    "message":"创建成功",
    "data": {
      user_id: 1
    }
}
```

## <a name="exist_user">根据手机号查询用户是否存在</a>
```
POST http://hostname/api/open/users/exists
```
### Request

```
# HEADERS
Content-type: "application/json"

# BODY
{
    "phone": "手机号"
}
```
### Response

#### 正确结果

```
# BODY
{
    "status":200,
    "message":"请求成功",
    "data": {
      user_id: 1
    }
}
```

## <a name="add_child">添加儿童</a>
```
POST http://hostname/api/open/children/add
```
### Request

```
# HEADERS
Content-type: "application/json"

# BODY
{
    "user_id": "用户id",
    "child_name": "儿童姓名"
}
```
### Response

#### 正确结果

```
# BODY
{
    "status":200,
    "message":"添加成功",
    "data": {
      child_id: 1
    }
}
```

## <a name="child_list">根据手机号或user_id获取儿童列表(先查user_id,没有用户再查phone)</a>
```
POST http://hostname/api/open/users/children
```
### Request

```
# HEADERS
Content-type: "application/json"

# BODY
{
    "user_id": "用户id"，
    "phone": "手机号"
}
```
### Response

#### 正确结果

```
# BODY
{
    "status":200,
    "message":"添加成功",
    "data": {
      children: [
        {id: 1, name: '', age: 1, gender: ''}
      ]
    }
}
```

## <a name="users_device">绑定镜腿</a>
```
POST http://hostname/api/open/users/device
```
### Request

```
# HEADERS
Content-type: "application/json"

# BODY
{
    "child_id": "儿童id",
    "mac_address": "mac地址",
    "device_type": "版本号",
    "uuid": "uuid值"
}
```
### Response

#### 正确结果

```
# BODY
{
    "status":200,
    "message":"绑定成功"
}
```

## <a name="unbind_device">解绑镜腿</a>
```
POST http://hostname/api/open/users/unbind
```
### Request

```
# HEADERS
Content-type: "application/json"

# BODY
{
    "child_id": "儿童id"
}
```
### Response

#### 正确结果

```
# BODY
{
    "status":200,
    "message":"解绑成功"
}
```


## <a name="uploads_data">同步数据</a>
```
POST http://hostname/api/open/uploads
```
### Request

```
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

```
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
```
GET http://hostname/api/v5/forecasts/options
```
### Request

```
# HEADERS
Content-type: "application/json"

# BODY
{}
```
### Response

#### 正确结果

```
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
```
GET http://hostname/api/v5/forecasts
```
### Request

```
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

```
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

## <a name="reports_health">眼健康</a>
```
GET http://hostname/api/open/reports/health
```
### Request

```
# HEADERS
Content-type: "application/json"

# BODY
{
    child_id: '儿童id',
    date: '2019-01-01'
}
```
### Response

#### 正确结果

```
# HTTP CODE
200

# BODY
{
    "status": 200,
    "message": "请求成功",
    "data": {
        "id": 157991,
        "device_user_id": 13905,
        "out_time_index": 0,
        "lux_day_index": 0,
        "step_count_index": 0,
        "nearwork_burden_day_index": 29,
        "bad_posture_day_index": 30,
        "nearwork_day_index": 30,
        "health_index": 70,
        "wear_time": 115,
        "bad_posture_times": 30,
        "nearwork_burden_day": 219,
        "nearwork_day": 77,
        "out_time": 5,
        "out_time_lux": 10927,
        "step_count": 1215,
        "nearwork_burden_day_percent": 29,
        "out_time_lux_percent": 4,
        "lux_day_percent": 3,
        "user_ranking": 32,
        "grade": "e",
        "grade_cn": "较差",
        "intro": "今日用眼较差，属于近视中高危人群",
        "suggest": "此分数说明孩子的用眼行为存在较大的问题，如户外时间较短或室内近距用眼时间过长过近等问题持续未得到改善，预计未来近视度数将继续加深到中高度近视。孩子需要达到不少于2小时的户外时间，同时室内需保持“一拳一尺一寸”的标准坐姿。",
        "out_time_data": {
            "out_time": 5,
            "out_time_percent": 4,
            "out_time_grade": "a",
            "out_time_grade_cn": "太少",
            "out_time_suggest": "意味着今天户外活动时间少于1个小时，距离眼科专家规定的每天不少于户外2小时的目标尚远；孩子长时间在室内将会影响身体与视力的健康发育，近视的风险也将大幅提高。建议课外多进行登高望远活动，让孩子在公园和山上凝视远处的田野和群山。"
        },
        "lux_data": {
            "lux_day_percent": 3,
            "lux_day_grade": "a",
            "lux_day_grade_cn": "太少",
            "lux_day_suggest": "意味着今天的阳光摄入量小于15w lux（光照单位），还远远没有达到目标哦！室内的光照要远远小于阳光的光照强度，同时由于空间的限制，孩子眼睛也未能看到足够远的距离，因此建议孩子多去户外接受阳光的照射，将对视力大有好处。"
        },
        "step_count_data": {
            "step_count": 1215,
            "step_count_percent": 12,
            "step_count_grade": "a",
            "step_count_grade_cn": "太少",
            "step_count_suggest": "你今天的运动步数过少哦（少于5000步），距离今天的运动目标还远远不够呢，要多多参加户外活动，增加看远的时间，眼睛才有机会得到放松，身心得到锻炼哦！"
        },
        "bad_posture_data": {
            "bad_posture_day": 61,
            "bad_posture_day_percent": 25,
            "bad_posture_times": 30,
            "bad_posture_times_percent": 33,
            "bad_posture_times_grade": "a",
            "bad_posture_times_grade_cn": "低风险",
            "bad_posture_times_suggest": "你今天出现不良用眼姿态的次数（小于45次）在低风险范畴哦！你的用眼姿态整体很好，你一定是班上的爱眼护眼小标兵，诺小瞳要给你100分，以后也请继续保持满分的用眼好习惯，一双好眼睛将会让你受益一生！"
        },
        "nearwork_burden_data": {
            "nearwork_burden_day": 219,
            "nearwork_burden_percent": 29,
            "nearwork_burden_grade": "a",
            "nearwork_burden_grade_cn": "低风险",
            "nearwork_burden_suggest": "你今天的颈椎与用眼负担在375D以内，说明今天的颈椎与用眼负担在可接受的范围内，没有承受过多的负担，近视眼与颈椎病的发生发展风险都很低，眼睛和颈椎在你的保护下，都在继续健健康康地发育呢！"
        },
        "nearwork_data": {
            "nearwork_total": 77,
            "nearwork_percent": 32,
            "nearwork_grade": "a",
            "nearwork_grade_cn": "低风险",
            "nearwork_suggest": "你今天的近距用眼时间（小于2个小时）在低风险范围内，眼睛得到了充分的休息，度过了轻松的一天，请继续保持哦！"
        }
    }
}
```

## <a name="reports_daily">日报</a>
```
GET http://hostname/api/open/reports/daily
```
### Request

```
# HEADERS
Content-type: "application/json"

# BODY
{
    child_id: '儿童id',
    date: '2019-01-01'
}
```
### Response

#### 正确结果

```
# HTTP CODE
200

# BODY
{
	"status": 200,
	"message": "请求成功",
	"data": {
		"bad_posture_data": {
			"bad_posture_day": 0.0,
			"bad_posture_day_percent": 0,
			"bad_posture_times": 0,
			"bad_posture_times_percent": 0,
			"bad_posture_times_grade": "a",
			"bad_posture_times_grade_cn": "低风险",
			"bad_posture_times_suggest": "你今天出现不良用眼姿态的次数（小于45次）在低风险范畴哦！你的用眼姿态整体很好，你一定是班上的爱眼护眼小标兵，诺小瞳要给你100分，以后也请继续保持满分的用眼好习惯，一双好眼睛将会让你受益一生！",
			"bad_posture_hour": [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
			"description": "儿童正确的用眼读写姿势是：坐姿端正，做到一拳一尺一寸，一拳指胸离书桌一拳远（8cm），眼睛离书本一尺远（33cm），手离笔尖一寸远（3cm）。坐姿不正、歪头阅读、握笔方法错误等不良用眼读写姿势会引起眼睛调节滞后，颈部疼痛，从而引起近视的发生或加深。我们的APP将记录儿童近距离不良用眼时间及次数，当超过一定指标，智能眼镜会提醒干预，同时该项显示为红色，反之则显示为绿色。"
		},
		"nearwork_data": {
			"nearwork_total": 0,
			"nearwork_percent": 0,
			"nearwork_grade": "a",
			"nearwork_grade_cn": "低风险",
			"nearwork_suggest": "你今天的近距用眼时间（小于2个小时）在低风险范围内，眼睛得到了充分的休息，度过了轻松的一天，请继续保持哦！",
			"nearwork_hour": [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
			"description": "近距离用眼时间过长，是目前公认的近视发生发展的重要因素之一。世界视光学会对青少年近距离用眼提出了“20-20-20原则”，即近距离用眼20分钟之后，尽量眺望20英尺（6米）远处20秒以上，有助于近视防控。我们建议儿童一天的近距用眼时间不要超过6个小时（360分钟）。"
		},
		"nearwork_burden_data": {
			"nearwork_burden_day": 0,
			"nearwork_burden_percent": 0,
			"nearwork_burden_grade": "a",
			"nearwork_burden_grade_cn": "低风险",
			"nearwork_burden_suggest": "你今天的颈椎与用眼负担在375D以内，说明今天的颈椎与用眼负担在可接受的范围内，没有承受过多的负担，近视眼与颈椎病的发生发展风险都很低，眼睛和颈椎在你的保护下，都在继续健健康康地发育呢！",
			"nearwork_burden_list": [{
				"name": "放松",
				"percent": 0,
				"colour": "#2FC14A",
				"duration": 0,
				"tip": "低头0~15度或抬头时阅读距离50~200厘米颈椎承受重量约5公斤"
			}, {
				"name": "低负荷",
				"percent": 0,
				"colour": "#27ADFF",
				"duration": 0,
				"tip": "低头15~30度或抬头时阅读距离30~50厘米颈椎承受重量约12公斤"
			}, {
				"name": "中负荷",
				"percent": 0,
				"colour": "#E5D40C",
				"duration": 0,
				"tip": "低头30~45度或抬头时阅读距离20~30厘米颈椎承受重量约18公斤"
			}, {
				"name": "高负荷",
				"percent": 0,
				"colour": "#F5A623",
				"duration": 0,
				"tip": "低头45~60度或抬头时阅读距离10~20厘米颈椎承受重量约22公斤"
			}, {
				"name": "超高负荷",
				"percent": 0,
				"colour": "#CC4455",
				"duration": 0,
				"tip": "低头大于60度或抬头时阅读距离小于100厘米颈椎承受重量约27公斤"
			}],
			"nearwork_burden_1D_duration": 0,
			"nearwork_burden_2D_duration": 0,
			"nearwork_burden_3D_duration": 0,
			"nearwork_burden_4D_duration": 0,
			"nearwork_burden_5D_duration": 0,
			"description": "当阅读距离越近，眼睛负荷也会增加，相应近视发生率就会增加。例如，当看书时眼睛距离书本33cm，眼睛会产生约3个D的调节负荷。若距离是10cm，眼睛将会产生约9个D的调节负荷，若该负荷持续30分钟，那么近视发生或加深的概率增加1.5~2.5倍。诺瞳眼健康将根据每日用眼负荷情况，进行轻中重分类，并精准计算。当负荷过大时，会显示红色预警状态，反之则显示为绿色。"
		},
		"step_count_data": {
			"step_count": 0,
			"step_count_percent": 0,
			"step_count_grade": "a",
			"step_count_grade_cn": "太少",
			"step_count_suggest": "你今天的运动步数过少哦（少于5000步），距离今天的运动目标还远远不够呢，要多多参加户外活动，增加看远的时间，眼睛才有机会得到放松，身心得到锻炼哦！",
			"step_count_hour": [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
			"calorie": 0.0,
			"step_distance": 0,
			"description": "多参加户外运动不仅减少近距离用眼的时间，增加看远的时间，有助于保护眼睛。专家建议学龄期孩每天走10000步左右，最佳时间是早上8点~10点。羽毛球、乒乓球、网球、足球、放风筝运动对放松眼睛，降低近视风险都很有帮助，同时请注意安全。"
		},
		"out_time_data": {
			"out_time": 0,
			"out_time_percent": 0,
			"out_time_grade": "a",
			"out_time_grade_cn": "太少",
			"out_time_suggest": "意味着今天户外活动时间少于1个小时，距离眼科专家规定的每天不少于户外2小时的目标尚远；孩子长时间在室内将会影响身体与视力的健康发育，近视的风险也将大幅提高。建议课外多进行登高望远活动，让孩子在公园和山上凝视远处的田野和群山。",
			"out_time_hour": [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
			"in_time_hour": [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
			"description": "科学研究发现：户外运动是公认的最自然，最有效的控制度数增长方式之一。青少年儿童每天户外时间累积超过2小时，针对近视的防控作用将达到最大，可使近视发生率降低30%。家长可指导孩子在课间、上学、放学路上有意识增加户外活动时间，即可轻松达到2小时。"
		},
		"protect_lux_time_data": {
			"protect_lux_time": 0,
			"protect_lux_time_percent": 0,
			"protect_lux_time_grade": "a",
			"protect_lux_time_grade_cn": "太少",
			"protect_lux_time_suggest": "意味着今天受到的护眼光照时间短于15分钟，距离目标尚远，请继续努力哦！一般即使是室内灯火通明，仍然比不上室外阴天的光照强度，因此是没有预防近视的效果的，所以不要总是在屋内当小宅男/女啦！",
			"description": "专家建议学生们在上午十点左右及下午四点左右两个时间段进行户外活动半小时，这时光照强度≥15000lux，可抑制50%左右的近视发病率，若光照过强，可配戴太阳镜、帽子等保护措施。相比于户外，室内光照对近视无保护作用。"
		},
		"lux_data": {
			"lux_day_percent": 0,
			"lux_day_grade": "a",
			"lux_day_grade_cn": "太少",
			"lux_day_suggest": "意味着今天的阳光摄入量小于15w lux（光照单位），还远远没有达到目标哦！室内的光照要远远小于阳光的光照强度，同时由于空间的限制，孩子眼睛也未能看到足够远的距离，因此建议孩子多去户外接受阳光的照射，将对视力大有好处。",
			"lux_hour": [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
			"lux_day": 0,
			"out_time_lux": 0,
			"lux_daytime": 0,
			"lux_daytime_avg": 0,
			"lux_nighttime": 0,
			"lux_nighttime_avg": 0,
			"uv_day": 0,
			"uv_max": 0,
			"description": "科学研究表明：太阳的光照强度比室内光照强度高数百倍，高强度光照一方面可使瞳孔缩小、景深加深，达到抑制近视的发生；另一方面是光照越强，多巴胺释放量越多，而多巴胺也能抑制近视的发生发展。建议可在阳光晴好的时候多出去沐浴阳光，同时做好防晒措施。"
		}
	}
}
```

## <a name="reports_weekly">周报</a>
```
GET http://hostname/api/open/reports/weekly
```
### Request

```
# HEADERS
Content-type: "application/json"

# BODY
{
    child_id: '儿童id',
    date: '2019-01-01'
}
```
### Response

#### 正确结果

```
# HTTP CODE
200

# BODY
{
	"status": 200,
	"message": "请求成功",
	"data": {
		"id": 1,
		"child_id": 2,
		"health_index": 0,
		"health_index_array": [0, 0, 0, 0, 0, 0, 0],
		"effective_days": 0,
		"out_time": 0,
		"out_time_array": [0, 0, 0, 0, 0, 0, 0],
		"protect_lux_time": 0,
		"protect_lux_time_array": [0, 0, 0, 0, 0, 0, 0],
		"lux_day": 0,
		"lux_day_array": [0, 0, 0, 0, 0, 0, 0],
		"lux_daytime": 0,
		"lux_daytime_array": [0, 0, 0, 0, 0, 0, 0],
		"lux_nighttime": 0,
		"lux_nighttime_array": [0, 0, 0, 0, 0, 0, 0],
		"out_time_lux_avg": 0,
		"out_time_lux_array": [0, 0, 0, 0, 0, 0, 0],
		"step_count": 0,
		"step_count_array": [0, 0, 0, 0, 0, 0, 0],
		"nearwork_burden_day": 0,
		"nearwork_burden_day_array": [0, 0, 0, 0, 0, 0, 0],
		"bad_posture_times": 0,
		"bad_posture_times_array": [0, 0, 0, 0, 0, 0, 0],
		"nearwork_day": 0,
		"nearwork_day_array": [0, 0, 0, 0, 0, 0, 0],
		"wear_time_array": [0, 0, 0, 0, 0, 0, 0],
		"merchant_id": null,
		"suggest": "经过本周测评，戴镜时间少及数据不完整，该测评报告不能很好的反映真实用眼情况。建议一周至少8小时/天的戴镜时间，以更好的完成数据测评，找出近视的危险因素以助于孩子更好的防控近视。",
		"time_array": ["2019-04-08", "2019-04-09", "2019-04-10", "2019-04-11", "2019-04-12", "2019-04-13", "2019-04-14"],
		"up_element": 0,
		"down_element": 0,
		"wear_time": 0,
		"health_index_total": 0,
		"user_ranking": 0,
		"grade": "e",
		"grade_cn": "无",
		"health_standard": [120, 30, 300000, 10000, 240, 750, 90],
		"weekend_score": 0,
		"week_score": 0,
		"weekend_score_avg": 0,
		"week_score_avg": 0,
		"doctor_name": "",
		"doctor_id": null
	}
}
```

## <a name="reports_monthly">月报</a>
```
GET http://hostname/api/open/reports/monthly
```
### Request

```
# HEADERS
Content-type: "application/json"

# BODY
{
    child_id: '儿童id',
    date: '2019-01-01'
}
```
### Response

#### 正确结果

```
# HTTP CODE
200

# BODY
{
	"status": 200,
	"message": "请求成功",
	"data": {
		"id": 2,
		"child_id": 3,
		"health_index": 0,
		"health_index_array": [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
		"effective_days": 0,
		"out_time": 0,
		"out_time_array": [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
		"protect_lux_time": 0,
		"protect_lux_time_array": [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
		"lux_day": 0,
		"lux_day_array": [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
		"lux_daytime": 0,
		"lux_daytime_array": [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
		"lux_nighttime": 0,
		"lux_nighttime_array": [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
		"out_time_lux_avg": 0,
		"out_time_lux_array": [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
		"step_count": 0,
		"step_count_array": [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
		"nearwork_burden_day": 0,
		"nearwork_burden_day_array": [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
		"bad_posture_times": 0,
		"bad_posture_times_array": [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
		"nearwork_day": 0,
		"nearwork_day_array": [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
		"wear_time_array": [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
		"merchant_id": null,
		"suggest": "经过本月测评，戴镜时间少及数据不完整，该测评报告不能很好的反映真实用眼情况。建议每天至少8小时的戴镜时间，以更好的完成数据测评，找出近视的危险因素以助于孩子更好的防控近视。",
		"time_array": ["2019-04-01", "2019-04-02", "2019-04-03", "2019-04-04", "2019-04-05", "2019-04-06", "2019-04-07", "2019-04-08", "2019-04-09", "2019-04-10", "2019-04-11", "2019-04-12", "2019-04-13", "2019-04-14", "2019-04-15", "2019-04-16", "2019-04-17", "2019-04-18", "2019-04-19", "2019-04-20", "2019-04-21", "2019-04-22", "2019-04-23", "2019-04-24", "2019-04-25", "2019-04-26", "2019-04-27", "2019-04-28", "2019-04-29", "2019-04-30"],
		"up_element": 0,
		"down_element": 0,
		"wear_time": 0,
		"health_index_total": 0,
		"user_ranking": 5,
		"grade": "e",
		"grade_cn": "无",
		"health_standard": [120, 30, 300000, 10000, 240, 750, 90],
		"doctor_name": "",
		"doctor_id": null
	}
}
```
