# open-API-in-r

<html>
<body>
<h1>R을 활용하여 오픈 API자료를 읽어오기</h1>
  <p>어제 TV를 보다가 후쿠시마산 수산물이 수입될 수도 있다는 뉴스를 접했습니다. 정말 걱정이됩니다.
    그래서 많고 많은 자료들중에 '수산물 수출입 현황'한번 읽어와 보겠습니다.</p>


<p>
#install.packages("rvest")
library(rvest)

api='http://apis.data.go.kr/1192000/openapi/service/ManageExpItemService/getExpItemList?ServiceKey=zBvSB3b0iaKU6E%2FCcG9KIhWWbKuNSdtsa9n5NT1Z4r826u4nUxM2B5CUEKrVl83LkKBIkldFK8snLlWXWYa9oQ%3D%3D&pageNo=1&numOfRows=10&type=xml&baseDt=201610'</p>

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
