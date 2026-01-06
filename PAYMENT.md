# 收费方案与支付设置指南

## 收费方案概述

### 免费版（¥0）
- 前 10 个闪卡
- 前 5 个核心概念
- 预览重点文档

### 完整版（¥9.9/永久）
- 全部 67 个闪卡
- 全部 15 个核心概念
- 重点文档完整版下载
- 思维导图高清版
- 永久免费更新
- 优先客服支持

## 支付方式选择

### 方案一：个人收款码（推荐新手）

#### 优点
- 设置简单，无需审核
- 资金直接到个人账户
- 无手续费（或手续费很低）

#### 缺点
- 需要手动发放验证码
- 无法自动验证支付
- 用户体验稍差

#### 设置步骤

1. **获取收款码**
   - 微信：打开微信 → 我 → 服务 → 钱包 → 收付款 → 收款码
   - 支付宝：打开支付宝 → 首页 → 收款

2. **保存收款码**
   - 截图保存收款码
   - 将图片保存到 `assets/` 目录
   - 命名为 `wechat-qr.png` 和 `alipay-qr.png`

3. **修改网站代码**
   
   在 `unlock.html` 中找到支付二维码部分，替换为：
   ```html
   <div class="bg-white p-4 rounded-lg flex justify-center">
       <img src="assets/wechat-qr.png" alt="微信支付" class="w-48 h-48">
   </div>
   ```

4. **设置验证码**
   
   在 `js/data.js` 中修改验证码：
   ```javascript
   function unlock(code) {
       if (code === 'YOUR_CUSTOM_CODE') {
           localStorage.setItem('unlocked', 'true');
           return true;
       }
       return false;
   }
   ```

5. **发放验证码流程**
   - 用户支付后截图
   - 用户通过微信/支付宝/邮箱联系你
   - 你验证支付后，手动发放验证码
   - 用户在网站输入验证码解锁

### 方案二：第三方支付平台（推荐进阶）

#### 可选平台
- **PayPal**：国际支付，适合海外用户
- **Stripe**：功能强大，需要企业资质
- **支付宝开放平台**：适合国内，需要企业认证
- **微信支付商户平台**：适合国内，需要企业认证

#### 优点
- 自动验证支付
- 用户体验好
- 支持多种支付方式

#### 缺点
- 需要企业资质
- 有手续费
- 设置复杂

#### 设置步骤（以支付宝为例）

1. **注册支付宝开放平台账号**
   - 访问 [支付宝开放平台](https://open.alipay.com)
   - 注册并完成企业认证

2. **创建应用**
   - 创建网页/移动应用
   - 配置回调地址
   - 获取 AppID 和密钥

3. **集成支付 SDK**
   - 下载支付宝 SDK
   - 修改 `unlock.html` 集成支付功能
   - 实现支付回调验证

4. **修改验证逻辑**
   ```javascript
   function unlock(code) {
       // 调用后端验证支付状态
       fetch('/api/verify-payment', {
           method: 'POST',
           body: JSON.stringify({ code: code })
       })
       .then(response => response.json())
       .then(data => {
           if (data.valid) {
               localStorage.setItem('unlocked', 'true');
               return true;
           }
       });
       return false;
   }
   ```

### 方案三：知识付费平台（推荐快速上线）

#### 可选平台
- **知识星球**：适合社群运营
- **小鹅通**：功能完善，适合课程
- **得到**：适合高质量内容
- **CSDN/知乎付费专栏**：适合技术内容

#### 优点
- 平台自带支付
- 无需技术设置
- 有流量扶持

#### 缺点
- 平台抽成高（20-30%）
- 内容受平台限制
- 用户数据不在自己手中

## 验证码管理

### 生成验证码

使用以下方式生成唯一验证码：

```javascript
function generateCode() {
    const timestamp = Date.now().toString(36);
    const random = Math.random().toString(36).substr(2, 5);
    return timestamp + random.toUpperCase();
}
```

### 存储验证码

可以创建一个简单的验证码管理系统：

```javascript
// 验证码数据库
const codes = {
    'ABC123': { used: false, createdAt: '2024-01-06' },
    'DEF456': { used: false, createdAt: '2024-01-06' }
};

// 验证验证码
function verifyCode(code) {
    if (codes[code] && !codes[code].used) {
        codes[code].used = true;
        return true;
    }
    return false;
}
```

### 批量生成验证码

```javascript
function batchGenerate(count) {
    const codes = [];
    for (let i = 0; i < count; i++) {
        codes.push(generateCode());
    }
    return codes;
}

// 生成 100 个验证码
const codes = batchGenerate(100);
console.log(codes.join('\n'));
```

## 营销策略

### 定价建议

- **低价策略**：¥9.9（吸引更多用户）
- **中等定价**：¥19.9（平衡收入和销量）
- **高价策略**：¥29.9（强调内容质量）

### 促销活动

1. **限时优惠**
   - 考试前 3 天 5 折
   - 早鸟价（前 50 名）
   - 团购优惠（3 人成团 7 折）

2. **增值服务**
   - 附赠其他学科资料
   - 提供答疑服务
   - 定期更新内容

3. **社交传播**
   - 分享返现（推荐好友购买返 ¥2）
   - 朋友圈集赞优惠
   - 群内拼团

### 客服支持

设置联系方式：
- 微信：在网站底部添加微信号
- QQ：添加 QQ 群号
- 邮箱：提供客服邮箱

## 数据统计

### 简单统计

在 `unlock.html` 中添加统计代码：

```javascript
function trackUnlock() {
    const data = {
        timestamp: new Date().toISOString(),
        userAgent: navigator.userAgent
    };
    
    // 发送到统计服务
    fetch('https://your-analytics.com/track', {
        method: 'POST',
        body: JSON.stringify(data)
    });
}
```

### 使用第三方统计

- **百度统计**：免费，国内常用
- **Google Analytics**：免费，功能强大
- **友盟+**：免费，适合移动端

## 法律合规

### 注意事项

1. **税务申报**
   - 个人收款需要申报个人所得税
   - 建议咨询税务专业人士

2. **内容版权**
   - 确保内容原创或有授权
   - 避免侵犯他人版权

3. **用户协议**
   - 添加用户服务协议
   - 明确退款政策

4. **隐私保护**
   - 不收集不必要的用户信息
   - 遵守相关法律法规

## 常见问题

### Q: 如何防止验证码泄露？
A: 
- 使用一次性验证码
- 设置验证码有效期
- 记录验证码使用情况

### Q: 用户要求退款怎么办？
A: 
- 明确退款政策（如：7 天无理由退款）
- 退款后禁用验证码
- 保留退款记录

### Q: 如何提高转化率？
A: 
- 优化免费内容，展示价值
- 添加用户评价
- 提供限时优惠
- 优化支付流程

### Q: 可以支持其他支付方式吗？
A: 
- 可以集成更多支付方式
- 考虑用户习惯选择支付方式
- 注意支付手续费

## 下一步

1. 选择适合你的支付方案
2. 设置收款码或集成支付平台
3. 生成验证码管理系统
4. 测试支付流程
5. 上线并推广

## 需要帮助？

如果遇到问题，可以：
- 查看各支付平台的官方文档
- 在技术社区寻求帮助
- 联系支付平台客服