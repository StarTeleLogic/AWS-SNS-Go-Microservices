# AWS-SNS-Go-Microservices
Amazon Simple Notification Service

## INstallation
```go
go get https://github.com/StarTeleLogic/AWS-SNS-Go-Microservices
```

# Sending a sms text on mobile number in any country
package main
````go
import (
    "fmt"
    "github.com/aws/aws-sdk-go/aws"
    "github.com/aws/aws-sdk-go/aws/credentials"
    "github.com/aws/aws-sdk-go/aws/session"
    "github.com/aws/aws-sdk-go/service/sns"
    "log"
)
````

# Define a function calling
```go
func main() {
    err := SendSMS("918769640272", "Hi, This is startelelogic")
    if err != nil {
        log.Fatal(err)
    }
}
```

# Define AWS Configuration
```go
const (
    // Replace AccessKeyID with your AccessKeyID key.
    AccessKeyID = ""
    // Replace AccessKeyID with your AccessKeyID key.
    SecretAccessKey = ""
    // Replace us-west-2 with the AWS Region you're using for Amazon SNS.
    AwsRegion = "us-west-2"
)
```

# Define function definition
```go
func SendSMS(phoneNumber string, message string) error {
    // Create Session and assign AccessKeyID and SecretAccessKey
    sess, err := session.NewSession(&aws.Config{
        Region:      aws.String(AwsRegion),
        Credentials: credentials.NewStaticCredentials(AccessKeyID, SecretAccessKey, ""),
    },
    )
    // Create SNS service
    svc := sns.New(sess)
    // Pass the phone number and message.
    params := &sns.PublishInput{
        PhoneNumber: aws.String(phoneNumber),
        Message:     aws.String(message),
    }
    // sends a text message (SMS message) directly to a phone number.
    resp, err := svc.Publish(params)
    if err != nil {
        log.Println(err.Error())
    }
    fmt.Println(resp) // print the response data.
    return "SMS has been sent successfully."
}
```
