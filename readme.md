# Hitokoto to flomo 

基于 Github Action 的 flomo 自动推送脚本，用于从 hitokoto API 获取一言并推送到 flomo 笔记。

## 功能

- 每天推送一条随机的一言到 flomo 笔记
- 对不同类型的一言进行分类，并添加 flomo 标签
- 针对不同类别的一言，设置不同的 flomo 笔记模板

## 实例

![alt text](image-3.png)
![alt text](image-4.png)

## 使用方法

1. **Fork 本项目**
   点击右上角的 Fork 按钮，将本项目 Fork 到自己的 Github 仓库
2. **配置 secrets**
   进入自己的 Github 仓库，点击 `Settings` -> `Security` -> `Secrets and variables` -> `Actions`，添加以下 secrets：
   - `FLOMO_API_URL`：你的 flomo 账户的 API URL，用于推送笔记
   > - 注意：请确保你的 flomo 账户已经开通 PRO 会员，否则无法推送笔记。
   > - API URL 形如 `https://flomoapp.com/iwh/xxxxxxx/xxxxxxx`
3. **配置 Github Action 运行时间**
   在 `.github/workflows/main.yml` 文件中，修改 `cron: '0 10 * * *' ` 字段，设置 Github Action 运行时间，如每天 UTC 10:00(北京时间 18:00) 运行：
   ```yaml
   on:
     schedule:
       - cron: '0 10 * * *'       # 每天 UTC 10:00(北京时间 18:00) 运行
   ```
   > 推送时间的 CRON 表达式，时间要加上 8 小时才为北京时间。推送时间不会完全准确，高峰时期大概会延迟 40-50 分钟推送，可以酌情考虑把设置推送时间比想要推送的时间稍微提前一些
4. **配置一言的类型**
   在 `.github/workflows/main.yml` 文件中，修改 `letter_dict` 字段，设置一言的类型,把不想要的类型删去
