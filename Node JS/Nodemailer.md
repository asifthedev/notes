## Nodemailer

```js
// Configure transporter
const transporter = nodemailer.createTransport({
  host: "smtp.hostinger.com",
  port: 465,
  secure: true,
  auth: {
    user: "info@asifshahzad.me",
    pass: "Asif@123...mail", // Use environment variable in production
  },
});
```



```js
await transporter.sendMail({
  from: '"Asif Shahzad" <info@asifshahzad.me>',
  to: email,
  subject: "Thank You for Your Interest",
  text: `Plain text version of your email`,
  html: emailTemplate(name, project), 
});


```


