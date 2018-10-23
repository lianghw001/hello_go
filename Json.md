
````
import (
	"encoding/json"
	"fmt"
	"io/ioutil"
	"os"

	"github.com/cyulei/agenda/entity"
)

````
- 从user.json文件读取jsonStr（json结构的byte[]）

````
josnStr, err := ioutil.ReadFile("datarw/CurUser.json")
````

- 将jsonStr转化为结构体或切片


````
var user entity.User
err = json.Unmarshal(josnStr, &user)
````


- 将结构体或切片转化为jsonStr
````
josnStr, err := json.Marshal(userToSave)
````

- 清空文件user.json
````
os.Truncate("datarw/CurUser.json", 0)
````
- 将jsonStr写入文件user.json
````
err = ioutil.WriteFile("datarw/CurUser.json", josnStr, os.ModeAppend)
````
