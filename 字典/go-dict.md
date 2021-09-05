# 字典
## 创建和初始化字典
创建任意类型的字典，有两种方法来创建字典：
- 通过语法糖
- 通过make，并且指定长度： `make(字典数据类型, 长度)`
- 通过make，没有指定长度： `maek(字典数据类型)`
```golang
// 通过语法糖来定义和初始化字典

dict := map[string]interface{}{}

dict["name"] = "js"
dict["age"] = 12

tmp := map[string]interface{}{"info": 12}

dict["info"] = tmp

fmt.Println(dict)
```

## 遍历字典
如何快速的遍历字典
```golang
var dictStr map[string]string = make(map[string]string{"name":"js", "province":"HuBei"})

for index, value := range dictStr {
	fmt.Printf("dictStr[%s] = %s", index, value)
}
```

## 访问指定key的值
如何通过指定的key来获取对应的值
```golang
dictStr := make(map[string]string)
dictStr["name"] = "js"

fmt.Printf("dictStr[\"name\"] = %s", dictStr["name"])

// 如果是需要进行判断是否存在呢？
if value, ok := dictStr["name"]; ok {
	fmt.Printf("dictStr[\"name\"] = %s\n", dictStr["name"])
} else {
	fmt.Printf("name not in the dictStr: %v\n", dictStr)
}
```

## 删除指定key
如何删除字典中的指定key
```golang
dictStr := make(map[string]string)
dictStr["name"] = "js"
dictStr["tmp"] = "tmp value"

fmt.Printf("Before delete operation. dictStr: %v\n", dictStr)
delete(dictStr, "tmp")
fmt.Printf("After delete operation. dictStr: %v\n", dictStr)
```

## 字典转化为json
如何将一个字典转化为json串
```golang
package main

import (
	"encoding/json"
	"fmt"
)

func main() {
	dictTmp := make(map[string]interface{})
	dictTmp["name"] = "js"
	dictTmp["age"] = 18
	dictTmp["score"] = []int{100, 200, 300}
	dictTmp["address"] = "中国"

	slice, err := json.Marshal(dictTmp)
	// slice, err := json.MarshalIndent(dictTmp, "", "\t")
	if err != nil {
		fmt.Println("json转换失败：", err)
	} else {
		fmt.Println(string(slice))
	}
}
```

## json转化为字典
如何将一个json串转化为字典
```golang
package main

import (
	"encoding/json"
	"fmt"
)

func main() {
	var dictTmp map[string]interface{}
	var jsonStr = `{"address":"中国","age":18,"name":"js","score":[100,200,300]}`

	err := json.Unmarshal([]byte(jsonStr), &dictTmp)
	if err != nil {
		fmt.Println("json解析失败：", err)
	} else {
		fmt.Printf("%+v\n", dictTmp)
	}
}

```

## 注意点
- 和切片一样，没有初始化的字典是不能使用的
- 只要能够进行 == 、!= 判断的数据类型，都可以作为字典的key

