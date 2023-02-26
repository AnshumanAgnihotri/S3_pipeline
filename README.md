# S3_pipeline
deploy on aws s3 using github action:
step1. create new github repo.
step2. create new s3 bucket.
step3. set iam rule for se full access.
step4. do public your bucket if you want to give public access.
step5. configure access key and secret key with github action.
step6. create main.yml.
step7. push code to github from local machine.
if you are facing issue during create .yml file.
you can use as refernce .yml file in below.

name: Deploy to AWS S3

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v2

      - name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@v1
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-s3-bukcet: ${{secrets.AWS_S3_BUCKET}}
          aws-region: us-east-1

      - name: Deploy code to S3
        run: |
          aws s3 sync . s3://your_bucket_name/
