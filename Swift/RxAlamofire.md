# RxAlamofire 메모
<br>

## pod 'RxAlamofire'
## 앱 내에 ATS설정. info.plist 에 아래 내용 추가
```
<key>NSAllowsArbitraryLoads</key>
<false/>
<key>NSExceptionDomains</key>
<dict>
    <key>friendservice.herokuapp.com</key>
    <dict>
        <key>NSExceptionAllowsInsecureHTTPLoads</key>
        <true/>
        <key>NSIncludesSubdomains</key>
        <true/>
    </dict>
</dict>
```
<br>

## request

```
let disposeBag = DisposeBag() // 전역변수에 추가
let urlString = "http://friendservice.herokuapp.com/listFriends"

data
string
json(.get, urlString)
    .debug()
    .subscribe(onNext: { print($0) })
    .disposed(by: disposeBag)
```
<br>

## response
 
 ```
requestData()
requestJSON(.get, urlString)
    .debug()
    .subscribe(onNext: {(res, json) in
        print(res)
        print(json)
    })

request(.get, urlString)
    .validate(statusCode: 200 ..< 299)
    .json()
    .subscribe(onNext: { print($0) } )
.validate(contentType: ["txet/json"])
 

requestJSON(.get, urlString)
.subscribe(
    onNext: {res, json in        
        guard let josnArray = json as? NSArray else { return }

        for item in josnArray {            
            guard let dic = item as? [String: Any] else { return }
            guard let firstName = dic["firstname"] as? String else { return }
            
            print(firstName)            
        }
})
.disposed(by: disposeBag)
```
