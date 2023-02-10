# mailJS操作流程

## 一.建立MailJS帳戶
[傳送門](https://dashboard.emailjs.com/admin)

## 二.創建Email Services
**為接收信件的客戶or廠商建立，客戶or廠商須提供mail**

![email_services](https://github.com/jingruei/repo-images/blob/master/images_for_blogs/email_services.png?raw=true)
![email_services_Config](https://github.com/jingruei/repo-images/blob/master/images_for_blogs/email_services_Config.png?raw=true)
## 三.創建Email Templates
#### 信件的預設模板，可自行修改，也可添加變數直接生成html來應用，相當便利。
![email_templates](https://github.com/jingruei/repo-images/blob/master/images_for_blogs/email_templates.png?raw=true)
![email_templates_model](https://github.com/jingruei/repo-images/blob/master/images_for_blogs/email_templates_model.png?raw=true)


## 四.安裝套件 or 使用CDN引入

**`npm install emailjs-com --save`**
```js
<script type="text/javascript" src="https://cdn.jsdelivr.net/npm/@emailjs/browser@3/dist/email.min.js"></script>
```

## 五.開始寫JS
```js
 <script type="text/javascript">
        emailjs.init('USER ID');  

        const btn = document.getElementById('button');

        document.getElementById('form').addEventListener('submit', function (event) {
            event.preventDefault();

            btn.value = 'Sending...';

            const serviceID = 'service ID';
            const templateID = 'template ID';

            emailjs.sendForm(serviceID, templateID, this)
                .then(() => {
                    btn.value = 'Send Email';
                    alert('Sent!');
                }, (err) => {
                    btn.value = 'Send Email';
                    alert(JSON.stringify(err));
                });
        });
</script>
```
- ##### USER ID放自己的，可以在Account -> API Keys 裡面看到。
- ##### serviceID、templateID 也是自己的，創建的地方皆可以找到。

#### 補充: 可以在建立email templates時，透過`playground`直接產生程式碼來使用
![email_templates_playground](https://github.com/jingruei/repo-images/blob/master/images_for_blogs/email_templates_playground.png?raw=true)
![email_templates_playground_code](https://github.com/jingruei/repo-images/blob/master/images_for_blogs/email_templates_playground_code.png?raw=true)

## 六. 測試
---
#### **缺點:**
1.**安全性**: 原因是因為畢竟是依賴第三方協助才能達成寄信這個功能~ 多多少少也要犧牲一些安全性 (雖然EmailJS部會直接暴露帳密在前端，也可以定期在後台改新的 TemplateID)

2. **額度限制**: 每個月只會讓你免費寄兩百封信~ 所以如果你是個人project當然沒問題，但在大型一點的就要好好考慮意下預算了~