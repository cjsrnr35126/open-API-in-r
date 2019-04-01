# open-API-in-r

<html>
<body>
<h1>R을 활용하여 오픈 API자료를 읽어오기(연습)</h1>
  많고 많은 자료들중에 '수산물 수출입 현황' 한번 읽어와 보겠습니다.<br>
  
  ![1](https://user-images.githubusercontent.com/49007889/55310216-debaed80-549a-11e9-9c04-4cad500d5a5c.PNG)
  
  ![2](https://user-images.githubusercontent.com/49007889/55310227-e5e1fb80-549a-11e9-9d61-24c9b0417c04.PNG)
  
  open API활용 가이드를 다운로드합니다.<br>
  가이드 파일을 보면 요청/응답 메세지 예제가 존재합니다. 예제대로 실행해 봅시다.<br>
  
  ![3](https://user-images.githubusercontent.com/49007889/55310523-93550f00-549b-11e9-8ca3-ff6341d2acb1.PNG)
  
  ![4](https://user-images.githubusercontent.com/49007889/55310836-66edc280-549c-11e9-92f8-813dd57fb99e.PNG)
  
  무엇이 문제일까요. 다시 가이드파일을 살펴보고 난 후 2016년10월 자료를 요청하는 &baseDt=201610을 url에 추가했습니다.<br>
  
  ![5](https://user-images.githubusercontent.com/49007889/55310842-69501c80-549c-11e9-9562-8720e0ce0377.PNG)
  
  이제 이 정보를 R을 이용해 읽어오겠습니다.<br>


<h3>R-code</h3>
<p>
#install.packages("rvest")
library(rvest)

api='http://apis.data.go.kr/1192000/openapi/service/ManageExpItemService/getExpItemList?ServiceKey=인증키&pageNo=1&numOfRows=10&type=xml&baseDt=201610'</p>

<p>
html_api=read_html(api,encoding = "UTF-8")<br>
###기준 년월<br>
ymd=html_api %>% html_nodes("item") %>% html_node('stdyymm') %>%html_text()<br>
###수산물 수출입품목코드<br>
code1=html_api %>% html_nodes("item") %>% html_node('mprcexipitmcode') %>%html_text()<br>
###수출입 구분코드<br>
code2=html_api %>% html_nodes("item") %>% html_node('imxprtsecode') %>%html_text()<br>
###수산물 수출입품목명<br>
name1=html_api %>% html_nodes("item") %>% html_node('mprcexipitmnm') %>%html_text()<br>
###수출입 구분명<br>
name2=html_api %>% html_nodes("item") %>% html_node('imxprtsenm') %>%html_text()<br>
###수산물 수출입품목 대분류코드<br>
lcls=html_api %>% html_nodes("item") %>% html_node('mprcexipitmlclascode') %>%html_text()<br>   
###수산물 수출입품목 중분류코드<br>
mcls=html_api %>% html_nodes("item") %>% html_node('mprcexipitmmlsfccode') %>%html_text()<br>
###수산물 수출입품목 소분류코드<br>
scls=html_api %>% html_nodes("item") %>% html_node('mprcexipitmsclascode') %>%html_text()<br>   
###수산물 수출입품목 세분류코드<br>
dcls=html_api %>% html_nodes("item") %>% html_node('mprcexipitmdtlclfccode') %>%html_text()<br>   
###수산물 수출입품목 순번<br>
sn=html_api %>% html_nodes("item") %>% html_node('mprcexipitmsn') %>%html_text()<br>
###수출입 중량<br>
wgt=html_api %>% html_nodes("item") %>% html_node('imxprtwt') %>%html_text()<br>
###수출입 미화금액<br>
dollar=html_api %>% html_nodes("item") %>% html_node('imxprtdollaramount') %>%html_text()<br>
db=data.frame(ymd,code1,code2,name1,name2,wgt,dollar)<br>
  </p>
</body>
<br>
실행결과입니다.

![캡처](https://user-images.githubusercontent.com/49007889/55308971-3c4d3b00-5497-11e9-97b4-543533dc09d8.PNG)

</html>
