# Nationality-App Deployment to LocalStack S3

## Prerequisites
```bash
docker --version
bash
Copy
node --version
Deployment Steps
1. Navigate to project directory
bash
Copy
cd nationality-app
2. Install dependencies
bash
Copy
npm install
3. Build production files
bash
Copy
npm run build
4. Start LocalStack container
bash
Copy
docker-compose up -d
5. Enter container shell
bash
Copy
docker exec -it stacky bash
6. Create S3 bucket
bash
Copy
awslocal s3api create-bucket --bucket nationality-app-bucket
7. Upload built files
bash
Copy
awslocal s3 sync ./dist s3://nationality-app-bucket
8. Configure website hosting
bash
Copy
awslocal s3 website s3://nationality-app-bucket --index-document index.html
9. Set bucket permissions
bash
Copy
awslocal s3api put-bucket-policy --bucket nationality-app-bucket --policy file://policy.json
10. Verify deployment
bash
Copy
awslocal s3api list-buckets
Access Your Application
Copy
http://nationality-app-bucket.s3.localhost.localstack.cloud:4566/index.html
