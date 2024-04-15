# Onehub Swift Library
```swift
import Foundation

let jsonData = [
    "phoneNumbers": "+2547XXXXXXXX,+2547XXXXXXXX",
    "message": "Hello Api!",
    "senderId": "Onehub"
] as [String : Any]

let data = try! JSONSerialization.data(withJSONObject: jsonData, options: [])

let url = URL(string: "https://api.onehub.co.ke/v1/sms/send")!
let headers = [
    "Content-Type": "application/json",
    "x-api-user": "API_USERNAME_HERE",
    "x-api-key": "API_KEY_HERE"
]

var request = URLRequest(url: url)
request.httpMethod = "POST"
request.allHTTPHeaderFields = headers
request.httpBody = data as Data

let task = URLSession.shared.dataTask(with: request) { (data, response, error) in
    if let error = error {
        print(error)
    } else if let data = data {
        let str = String(data: data, encoding: .utf8)
        print(str ?? "")
    }
}

task.resume()
```
# Username and API Key
You can get your username and API Key [here](https://dashboard.onehub.co.ke/account/0/user/signup).
# Request Body Parameters
`phoneNumbers` - `[Type: String]` `[Required]` - Phone numbers of the recipients in international format with the plus (+) sign. Multiple numbers should be comma-separated.

`Message` - `[Type: String]` `[Required]` - The message you want to send. Each message is counted as 160 characters long. Messages longer than 160 characters will be billed accordingly.

`Sender ID` - `[Type: String]` `[Required]` - A sender ID serves as a branding for outgoing messages, typically representing your company name. Your users will receive messages with your specified sender ID. You can apply for your sender ID on our [website](https://onehub.co.ke/).
