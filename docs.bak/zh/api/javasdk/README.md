---
sidebarDepth: 4
---
# 快速开始

## github

[Vitej](https://github.com/vitelabs/vitej)

## 开始

### 添加依赖

#### maven

```xml
<dependency>
  <groupId>org.vite</groupId>
  <artifactId>vitej</artifactId>
  <version>1.1.0</version>
</dependency>
<dependency>
  <groupId>org.vite</groupId>
  <artifactId>vitej-dependencies</artifactId>
  <version>1.1.0</version>
  <type>pom</type>
</dependency>
```

#### gradle

```
implementation 'org.vite:vitej:1.1.0'
implementation 'org.vite:vitej-dependencies:1.1.0'
```

### 使用示例

```java
import com.alibaba.fastjson.JSON;
import org.vitej.core.protocol.HttpService;
import org.vitej.core.protocol.Vitej;
import org.vitej.core.protocol.methods.response.SnapshotChainHeightResponse;

import java.io.IOException;

public class QuickStart {
    public static void main(String[] args) {
        try {
            // 实例化Vitej client
            Vitej vitej = new Vitej(new HttpService());
            // 查询最新的快照块高度
            SnapshotChainHeightResponse response = vitej.getSnapshotChainHeight().send();
            System.out.println(JSON.toJSONString(response));
            Long latestSnapshotHeight = response.getHeight();
            System.out.println(latestSnapshotHeight);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

更多示例见[Vitej demo](https://github.com/vitelabs/vitej-demo)

