# 크롤링(Crawling)

## 간단한 크롤링 만들기
crawling.py
```py
import requests
from bs4 import BeautifulSoup

res = requests.get('https://ovdncids.github.io/html-css-curriculum/facebook/index.html')
soup = BeautifulSoup(res.content, 'html.parser')

# print(soup.prettify())
  # .prettify() = html을 이쁘게 보여줌
# print(soup.header)
  # <header> 태그를 보여줌
# print(soup.find_all('div', {'class': 'post-shortcut'})[1].text.strip())
  # .find_all = 조건이 맞는 태그를 배열로 반환 한다
  # .strip() = 문자의 양쪽의 공백 제거
```

https://www.crummy.com/software/BeautifulSoup/bs4/doc.ko/
