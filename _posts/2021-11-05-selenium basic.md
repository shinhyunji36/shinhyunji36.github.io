---
title: '[python] Web scraping_02 (Selenium)'
description: selenium, beautifulsoup을 이용한 web scraping 실습과 수많은 🔨
categories: 
  - Data Engineering
tags: [selenium, web scraping]
toc : true
# author_profile: false
---


# Selenium

## Selenium 기초 
- beautifulsoup보다 직관적
- web driver (주로 chromedriver) 사용
- 클릭하거나 스크롤을 내리는 등 웹페이지 원격 조정 가능
  - 웹 어플리케이션 테스트를 위해 고안된 도구이기 때문

- requests 활용의 한계 보완
  - 로그인이 필요한 사이트는 웹 스크래핑이 힘들다.
  - 동적으로 html을 만드는 경우
    - 동적으로? : 전체 페이지가 리로딩 되는 것이 아니라, 부분만 정보가 업데이트 되는 html. 
    - 스크롤하거나, 클릭하면 데이터가 생성되나, url주소가 변경되지 않고 데이터가 변하는 특징.
    - 주로 표, 테이블 형태의 데이터



### 설치

```python
!pip install Selenium
!apt-get update
!apt install chromium-chromedriver
# user bin에 copy
!cp /usr/lib/chromium-browser/chromedriver /usr/bin

# 이렇게 해주어야 지금 설치된 chromedriver의 위치를 system path(환경 path)로 등록 가능
import sys
sys.path.insert(0, 'usr/lib/chromium-browser/chromedriver')
```



### 웹 드라이버 설정 (colab 기준)

```python
# 셀레니움 로컬에서 하면 브라우저 뜨는 것 볼 수 있지만, 코랩이라 안 뜨고 내부적으로 도는 것으로 설정할 것!
from selenium import webdriver

chrome_options = webdriver.ChromeOptions()
chrome_options.add_argument('--headless')
chrome_options.add_argument('--no-sandbox')
chrome_options.add_argument('--disable-dev-shm-usage')
```
```python
# 웹 드라이버 객체 생성
driver = webdriver.Chrome('chromedriver', options=chrome_options)
```



### 실행

```python
# get() :  url 로드
driver.get("http://suanlab.com/")
```

```python
# 웹페이지 스크린샷 떠서 저장 가능
wd.get_screenshot_as_file("suanlab.png")

# colab 상에 저장된 스크린샷 로컬로 다운받아 확인
from google.colab import files
files.download("suanlab.png")
```



- 요소 하나 가져오기 vs 요소 여러개 가져오기

  - 하나 가져올 때
    ```python
    driver.find_element_by
    ```
  - 여러개 가져올 때
    ```python
    driver.find_elements_by
    ```
    - find_elements로 복수의 요소들 가져올 수 있다.
    - 이땐 for 반복문 사용해서 하나씩 리스트에 넣어주거나 프린트 할 수 있다.

  

- css selector

  - select 활용 : 확실한 경로로 지정해주기 때문에 가져오고 싶은 요소 정확히 가져올 수 있음. 
  - copy selector : `웹페이지 > 마우스 오른쪽 클릭 > 검사 > copy > copy selector` > 붙여넣기
  - ex) 
     ```python
     labels = driver.select('#wrapper > section > div > div > div:nth-child(1) > div > div:nth-child(1) > label')
     ```

  

 - 위의 예시에서 `div:nth-child(1)` : div의 자식(소속) 중 첫번째 가져오기

 - 따라서 모든 자식(label)들을 한꺼번에 가져오고 싶다면, `div`뒤의 `:nth-child(1)`을 빼고 아래처럼 써주면 된다.
    ```python
    labels = driver.find_elements_by_css_selector('#wrapper > section > div > div > div > div > div > label')
    ```




- xpath

  - copy xpath 활용
  - Xpath 구문 의미 및 연습 : [w3schools](https://www.w3schools.com/xml/xpath_syntax.asp)
  - ex)
    ```python
    labels = driver.find_elements_by_xpath('//*[@id="wrapper"]/section/div/div/div/div/div/label')
    ```




- `find_elements(By.~, '찾는 것')`

  - find_elements_by~ 접근법 대신 사용 가능

    ```python
    find_elements(By.TAG_NAME,'찾는 것 이름')
    find_elements(By.CSS_SELECTOR,'찾는 것 위치')
    ```
    
  - ex)
    ```python
    from selenium.webdriver.common.by import By
    
    for label in driver.find_elements(By.TAG_NAME, 'label'):
      print(label.text)
    ```
    
    - 해당 코드랑 동일함 (find_elements_by_tag_name)
    ```python
    for label in driver.find_elements_by_tag_name('label'):
      print(label.text)
    ```

  

- 기타 이용법

  - 태그의 속성 가져오기 (ex. a 태그의 속성인 href 가져오기)
    ```python
    driver.find_element_by_tag_name('a').get_attribute('href')
    ```
    
  - find_elements로 찾은 elements가 담긴 리스트 안에서 마지막꺼 가져오고 싶을 때 ==> 인덱스로 찾기
    ```python
    driver.find_elements_by_tag_name('li')[-1]
    ```
    




## Reference

- selenium : [이수안컴퓨터연구소 youtube](https://www.youtube.com/watch?v=dDEESB4Iw8g&list=PL7ZVZgsnLwEFbtQ9LkKkzTBRDkEz3YHsQ&index=14)





