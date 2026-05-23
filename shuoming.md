1.先登录github账号
    954560590@qq.com
    密码：2023212028lyc
或者直接搜索YaoHengWang/20041208这个仓库

2.把auth.json传到~/.codex/auth.json

3.改本地SSH的config: .ssh/config：
    Host xxx
    HostName xxx
    Port xxx
    User xxx
    RemoteForward 17897 127.0.0.1:7897



https://blog.csdn.net/s404610154/article/details/159011279?fromshare=blogdetail&sharetype=blogdetail&sharerId=159011279&sharerefer=PC&sharesource=qq_69149270&sharefrom=from_link


https://blog.csdn.net/lxx309707872/article/details/160280985?ops_request_misc=elastic_search_misc&request_id=7cb7fe83e2fbc20c3e3ce5640383f964&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-2-160280985-null-null.142^v102^pc_search_result_base8&utm_term=claude%20code%20CC&spm=1018.2226.3001.4187


https://aimonkey.plus/




好的，整理如下：

---

## 明天 Linux 配置 Claude Code 完整流程

### 第一步：开启代理
打开 FlClash，确认 System proxy 已开启，代理端口 **7890**。

验证代理是否通：
```bash
curl -I --proxy http://127.0.0.1:7890 https://api.anthropic.com
```
返回非 403 就说明通了。

---

### 第二步：安装 Node.js（无需 sudo）
```bash
# 安装 nvm
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash

# 重新加载环境
source ~/.bashrc

# 安装 Node.js
nvm install 20
nvm use 20

# 验证
node -v
npm -v
```

---

### 第三步：安装 Claude Code
```bash
export HTTPS_PROXY=http://127.0.0.1:7890
export HTTP_PROXY=http://127.0.0.1:7890

npm install -g @anthropic-ai/claude-code

# 验证
claude --version
```

---

### 第四步：设置代理永久生效
```bash
echo 'export HTTPS_PROXY=http://127.0.0.1:7890' >> ~/.bashrc
echo 'export HTTP_PROXY=http://127.0.0.1:7890' >> ~/.bashrc
source ~/.bashrc
```

---

### 第五步：登录 Claude Code
```bash
claude
```
浏览器打开后选 **Claude.ai Subscription**，登录你的 Claude Pro 账号。

---

### 第六步：VS Code 插件配置
扩展商店搜 **Claude Code**（Anthropic 官方），安装。

按 `Ctrl+Shift+P` → 输入 `Open User Settings JSON` → 添加：

```json
{
    "http.proxy": "http://127.0.0.1:7890",
    "http.proxySupport": "override",
    "http.proxyStrictSSL": false,
    "claudeCode.environmentVariables": [
        {
            "name": "HTTP_PROXY",
            "value": "http://127.0.0.1:7890"
        },
        {
            "name": "HTTPS_PROXY",
            "value": "http://127.0.0.1:7890"
        }
    ]
}
```

**完全关闭 VS Code 再重新打开**，然后登录插件。

---

### 注意事项
- 全程不需要 sudo
- 每次新开终端如果代理失效，手动运行 `source ~/.bashrc`
- 登录选 **Claude.ai Subscription**