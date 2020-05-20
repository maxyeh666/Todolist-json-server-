# Todolist-json-server-

## 程式目的
javascript練習，使用vscode的外掛json-server搭配原生javascript的ajax(XMLHttprequest)進行C(create)R(read)U(update)D(delete)的存取

## 使用筆記
### 啟用json-server  

Terminal中輸入:
  - json-server json位置  
    可以啟動指定的json
  - json-server --watch json位置  
    可以切換使用的json

### 使用AJAX
#### 啟用XMLHttprequest
let Variable = new XMLHttpRequest()  

每次使用ajax都視作一個新的請求,使用建構式初始化,Variable為自己命名的變數

#### 設定要送出的請求
.open(method,url,async,user,password)  

.open()是把AJAX請求發送到指定位置的函式
- mothod的類型:
  - GET: 取得資料(read) 
  - POST: 增加資料(create)  
  - PUT: 更新資料(update),更新資料,但是沒輸入的部分會變成空字串  
  - PATCH: 更新資料(update),更新資料,只更新指定的資料,若沒有輸入的資料則維持原狀  
  - DELETE: 刪除資料(delete)
- url:接受請求的頁面(注意跨域請求的問題)  
- async: 非同步請求,預設為false
- user: 使用者帳號,預設為null
- password: 密碼,預設為null

詳細請看MDN:https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/open  

#### 設定標頭(head)的協議資訊
.setRequestHeader(header,value)  

 設定傳送到標頭的協議,本次在POST跟PATCH中設定.setRequestHeader('Content-type', 'application/json'),  
 即為設定傳送的為JSON格式,在需要修改時建議加上避免產生問題

#### 送出請求
.send(data)  

.send()是將請求送出到指定的頁面,data則是要傳送過去的資料

#### XMLHttprequest的屬性
這裡只寫一些本次使用的屬性  

- readyState:目前的處理狀態  
  - 0:	UNSENT 請求已建立,但尚未啟用.open()  
  - 1:  OPENED .open()已調用  
  - 2:  HEADERS_RECEIVED .send()已調用,header已接收  
  - 3:  LOADING 正在下載responseText的資料  
  - 4:  DONE  資料已下載完成
  
  詳細請看MDN:https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/readyState
  
- responseText:收到的回應文字(字串型態)
- status: 伺服器回傳的狀態碼

#### 監聽XMLHttprequest的狀態
.onreadystatechange = function()

當XMLHttprequest的readystate狀態改變時就執行對應的function
