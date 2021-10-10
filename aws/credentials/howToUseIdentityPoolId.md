# how to use identity pool id

when I want to upload file to s3 with public identity pool, how should I do ?

dep: [aws-sdk-go](github.com/aws/aws-sdk-go/)

```go
region := "Region"
identityPoolId := "PublicIdentityPoolId"

sess := session.Must(session.NewSession(&aws.Config{
  Region: aws.String(region),
}))

cisvc := cognitoidentity.New(sess)

idRes, _ := cisvc.GetId(&cognitoidentity.GetIdInput{
  IdentityPoolId: aws.String(identityPoolId),
})

credRes, _ := cisvc.GetCredentialsForIdentity(&cognitoidentity.GetCredentialsForIdentityInput{
  IdentityId: idRes.IdentityId,
})

svc := s3.New(sess, &aws.Config{
Credentials: credentials.NewStaticCredentials(
  *credRes.Credentials.AccessKeyId,
  *credRes.Credentials.SecretKey,
  *credRes.Credentials.SessionToken,
), Region: aws.String(region)})

ctx, cancel := context.WithTimeout(context.Background(), 40*time.Second)
if cancel != nil {
  defer cancel()
}

_, err = svc.PutObjectWithContext(ctx, &s3.PutObjectInput{
  Bucket:          aws.String(bucket),
  Key:             aws.String(fileKey),
  Body:            body,
  ACL:             aws.String(s3.BucketCannedACLPublicRead),
  ContentEncoding: aws.String(fileEncode),
  ContentType:     aws.String(fileType),
})

if err != nil {
if aerr, ok := err.(awserr.Error); ok && aerr.Code() == request.CanceledErrorCode {
  fmt.Fprintf(os.Stderr, "upload canceled due to timeout, %v\n", err)
} else {
  fmt.Fprintf(os.Stderr, "failed to upload object, %v\n", err)
}
} else {
  fmt.Printf("successfully uploaded file to %s/%s\n", fileKey)
}
```
