# ses-react-deploy-instructions

Instructions on how to deploy a react app
- React provides this [link](https://cra.link/deployment) that leads you to a lot of resources
- Using AWS. Recommended especially if you already have an account. See instructions [here](https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html)


Add this Bucket policy. Make sure you're only uploading files that you want to make public to your bucket. **Also replace `<YOUR_BUCKET_NAME>` with the name of your bucket.**
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": [
                "s3:GetObject"
            ],
            "Resource": [
                "arn:aws:s3:::<YOUR_BUCKET_NAME>/*"
            ]
        }
    ]
}
```

