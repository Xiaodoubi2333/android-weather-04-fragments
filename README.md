# android-weather-04-fragments v1.0

把底部导航模板（[`android-bottom-navigation`](https://github.com/Xiaodoubi2333/android-bottom-navigation)）与天气功能合并的中间版本：既保留 Home / Dashboard / Notifications / Call 四个页签，又接入了完整的天气模块（地区选择、实时天气、预报、AQI、生活建议、后台刷新）。

包名 `com.example.sadmanbn`，`compileSdk 34 / minSdk 23`。26 个 Java 文件、6 个布局，是本组仓库中第一个「导航 + 天气」双栈工程。

## 文件结构

```text
app/src/main/java/com/example/sadmanbn/
├── MainActivity.java               底部导航宿主
├── WeatherActivity.java            天气详情页
├── ChooseAreaFragment.java         省 - 市 - 县选择
├── db/                             LitPal 三表：Province / City / County
├── gson/                           接口返回体：Basic / Now / Forecast / AQI / Suggestion / Weather
├── service/AutoUpdateService.java  AlarmManager 定时刷新
├── ui/                             四个页签：home / dashboard / notifications / call（含 ViewModel、Entity）
└── util/                           HttpUtil、Utility
app/src/main/res/layout/            6 个布局
```

## 启动

1. Android Studio 打开、同步 Gradle；
2. 运行 `app`：底部导航进入 Home，点选城市 → 跳 `WeatherActivity` 显示天气；
3. 需要网络权限（`INTERNET`）访问 `guolin.tech` 教学接口。

依赖：`appcompat 1.0.2`、`material 1.0.0`、`constraintlayout 1.1.3`、`navigation-fragment/ui 2.0.0`、`lifecycle-extensions 2.0.0`、`litepal 1.3.2`、`okhttp 3.4.1`、`gson 2.7`、`glide 3.7.0`。

## 功能落点表

| # | 功能 | 状态 | 落点 |
|---|---|---|---|
| 1 | 底部四页签 | 完成 | `mobile_navigation.xml` + `MainActivity` |
| 2 | 省 / 市 / 县三级选择 | 完成 | `ChooseAreaFragment` |
| 3 | 选中城市持久化 | 完成 | LitPal `Province` 首选记录 |
| 4 | 实时天气 / 预报 / AQI / 建议 | 完成 | `WeatherActivity` + `gson/` 五个模型 |
| 5 | 后台定时更新（8 小时） | 完成 | `AutoUpdateService` + `AlarmManager` |
| 6 | 列表页视图复用 | 完成 | `ui/notifications` + `ViewHolder` |
| 7 | Home 页直达天气详情 | 完成 | `HomeFragment` → `WeatherActivity` |

## 版本记录

### v0.1 · 工程首推

- `chore: 初始化仓库（LICENSE / .gitignore）`：网页端建库。
- `feat: 导入含 assets 与 layout 的工程骨架`：模板工程入库。

### v0.2 · 三件套补全

- `feat: 补齐 Java 源码、assets 与布局`：补齐后工程可运行（原先两次内容重复的提交已合并为一次）。

### v1.0 · 双栈合并

- 在底部导航骨架上并入 coolweather 天气模块，形成「导航 + 天气」结构；后续功能拆分到 [`android-weather-05-navigation`](https://github.com/Xiaodoubi2333/android-weather-05-navigation) 继续迭代。

## 已知限制

- `applicationId` 与 [`android-bottom-navigation`](https://github.com/Xiaodoubi2333/android-bottom-navigation) 相同（`com.example.sadmanbn`），不能同时安装。
- 天气接口密钥硬编码在源码中，**仅限课程练习**。
- 页签文案仍为英文模板默认值。
