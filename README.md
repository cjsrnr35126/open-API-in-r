# open-API-in-r

<h1>R을 활용하여 오픈 API자료를 읽어오기</h1>
#install.packages("rvest")
library(rvest)

api='http://apis.data.go.kr/1192000/openapi/service/ManageExpItemService/getExpItemList?ServiceKey=zBvSB3b0iaKU6E%2FCcG9KIhWWbKuNSdtsa9n5NT1Z4r826u4nUxM2B5CUEKrVl83LkKBIkldFK8snLlWXWYa9oQ%3D%3D&pageNo=1&numOfRows=10&type=xml&baseDt=201610'


html_api=read_html(api,encoding = "UTF-8")
###기준 년월
ymd=html_api %>% html_nodes("item") %>% html_node('stdyymm') %>%html_text()
###수산물 수출입품목코드
code1=html_api %>% html_nodes("item") %>% html_node('mprcexipitmcode') %>%html_text()
###수출입 구분코드
code2=html_api %>% html_nodes("item") %>% html_node('imxprtsecode') %>%html_text()
###수산물 수출입품목명
name1=html_api %>% html_nodes("item") %>% html_node('mprcexipitmnm') %>%html_text()
###수출입 구분명
name2=html_api %>% html_nodes("item") %>% html_node('imxprtsenm') %>%html_text()
###수산물 수출입품목 대분류코드
lcls=html_api %>% html_nodes("item") %>% html_node('mprcexipitmlclascode') %>%html_text()   
###수산물 수출입품목 중분류코드
mcls=html_api %>% html_nodes("item") %>% html_node('mprcexipitmmlsfccode') %>%html_text()
###수산물 수출입품목 소분류코드
scls=html_api %>% html_nodes("item") %>% html_node('mprcexipitmsclascode') %>%html_text()   
###수산물 수출입품목 세분류코드
dcls=html_api %>% html_nodes("item") %>% html_node('mprcexipitmdtlclfccode') %>%html_text()   
###수산물 수출입품목 순번
sn=html_api %>% html_nodes("item") %>% html_node('mprcexipitmsn') %>%html_text()
###수출입 중량
wgt=html_api %>% html_nodes("item") %>% html_node('imxprtwt') %>%html_text()
###수출입 미화금액
dollar=html_api %>% html_nodes("item") %>% html_node('imxprtdollaramount') %>%html_text()
db=data.frame(ymd,code1,code2,name1,name2,wgt,dollar)
db
<br>
실행결과
<br>
![캡처](https://user-images.githubusercontent.com/49007889/55308971-3c4d3b00-5497-11e9-97b4-543533dc09d8.PNG)
