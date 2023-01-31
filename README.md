# RealWorld docker app

1. Create s3 bucket

2. Add bucket policy:
```bash
{
    "Version": "2012-10-17",
    "Id": "ExamplePolicy01",
    "Statement": [
        {
            "Sid": "ExampleStatement01",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::123456789:user/user_name"
            },
            "Action": [
                "s3:*Object",
                "s3:ListBucket"
            ],
            "Resource": [
                "arn:aws:s3:::conduit-fe/*",
                "arn:aws:s3:::conduit-fe"
            ]
        }
    ]
}
```

3. Genegate access key and secret access key

4. Go to frontend:
```bash
cd project-frontend
```

5. Build docker image:
```bash
docker build -t fe-builder -f Dockerfile.s3 .
```

6. Deploy

```bash
docker run -it -v "ts-redux-react-realworld-example-app":"/app" -e AWS_ACCESS_KEY_ID='access_key' -e AWS_SECRET_ACCESS_KEY='secret_access_key' -e AWS_DEFAULT_REGION='us-east-1' -w "/app" fe-builder /bin/bash -c 'npm clean-install && npm run build && aws s3 sync ./build/ s3://backet_name'
```