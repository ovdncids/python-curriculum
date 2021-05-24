# Email

settings.py
```py
EMAIL_HOST = 'smtp.gmail.com'
EMAIL_PORT = '587'
EMAIL_HOST_USER = 'user@gmail.com'
EMAIL_HOST_PASSWORD = 'password'
EMAIL_USE_TLS = True
DEFAULT_FROM_EMAIL = EMAIL_HOST_USER
```
```sh
python manage.py shell
```
```py
from django.core.mail import EmailMessage
email = EmailMessage('title', 'content', to=['xxx@gmail.com']) 
email.send()
# 1이 반환 되면 성공
```

## 에러
```py
smtplib.SMTPSenderRefused: (530, b'5.7.0 Authentication Required. Learn more at\n5.7.0  https://support.google.com/mail/?p=WantAuthError m19sm10581502pjq.41 - gsmtp', 'user@gmail.com')
  # Gmail로그인 후 설정 -> 모든 설정 보기 -> 전달 및 POP/IMAP -> IMAP 액세스: IMAP 사용

smtplib.SMTPAuthenticationError: (535, b'5.7.8 Username and Password not accepted. Learn more at\n5.7.8  https://support.google.com/mail/?p=BadCredentials m19sm10581502pjq.41 - gsmtp')
https://myaccount.google.com/lesssecureapps
  # 보안 수준이 낮은 앱 허용: 사용
```
