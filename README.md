特点

接受客户端文件上传、下载文件。
动态Http API，就像Java的Servlet一样写接口。
部署静态网站，例如纯Html，支持JS、CSS、Image分离。
部署动态网站，例如Html表单，当然可以结合上面的Android Http接口。

## AssetsWebsite的使用

如果你的网站在assets下，那么你就用AssetsWebsite来部署你的网站。

使用方法是：

```
//AssetManager不能被关闭。
AssetManager mAssetManager = getAssets();
Wesite wesite = new AssetsWebsite(mAssetManager, youPath);
```

上面我们看到new AssetsWebsite时需要传一个AssetManager和一个path，path支持assets根目录和子目录，下面是这两种情况的举例。

如果你的网站在assets根目录下, 你的path就填""，比如：
```
Wesite wesite = new AssetsWebsite(mAssetManager, "");
```


# AndServer

![Logo](./images/logo.svg)

Web server and Web framework of Android platform. It provides annotations like SpringMVC, and if you are familiar with SpringMVC, you can master it very quickly.

- Static html website deployment
- Dynamic http api deployment

```java
@RestController
@RequestMapping(path = "/user")
public class UserController {

    @PostMapping("/login")
    public String login(
        @RequestParam("account") String account,
        @RequestParam("password") String password) {

        ...
        return "Successful.";
    }

    @GetMapping(path = "/{userId}")
    public User info(
        @PathVariable("userId") String userId,
        @QueryParam("fields", required = false) String fields) {

        User user = findUserById(userId, fields);
        ...

        return user;
    }

    @PutMapping(path = "/{userId}")
    public void modify(
        @PathVariable("userId") String userId
        @RequestParam("age") int age) {
        ...
    }
}
```

The above code will generate the following two http apis:

```text
POST http://.../user/login
GET http://.../user/uid_001?fields=id,name,age
PUT http://.../user/uid_001
```

For documentation and additional information see [the website](https://www.yanzhenjie.com/AndServer).

## Download

```groovy
dependencies {
    implementation 'com.yanzhenjie.andserver:api:2.0.5'
    annotationProcessor 'com.yanzhenjie.andserver:processor:2.0.5'
}
```

If you are using Kotlin, replace `annotationProcessor` with `kapt`.

AndServer requires at minimum Android 2.3(Api level 9).

## Contributing

Before submitting pull requests, contributors must abide by the [agreement](./CONTRIBUTING.md) .

## License

```text
Copyright 2019 Zhenjie Yan

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
