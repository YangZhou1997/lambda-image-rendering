# lambda-image-rendering
Using Amazon Lambda for image processing

## Prerequisites
* Docker
* An existing S3 bucket (e.g., images-bucket-hello-world) containing a demon picture (e.g., lie3.png). 

## How to set up
### Using pure environment provided by lambda. 
```
# don't simply following the original instructions on the following rep -- will produce weird errors. 
git clone https://github.com/andreasonny83/serverless-image-rendering

cd serverless-image-rendering

# details refer to https://github.com/lambci/docker-lambda
docker run -it -v "$PWD":/var/task lambci/lambda:build-nodejs6.10 /bin/bash
```

### Installing packet dependencies (within the container)
```
npm install
npm install -g serverless
```

### Editing config files
```
yum install -y vim
cp serverless.sample.yml serverless.yml

# replace the BUCKET name under the environment section of serverless.yml according to your S3 bucket name previously created (e.g., images-bucket-hello-world).
# you might also need to change the region value in this yml file. 
```

### Setting AWS credentials file
Please following this [blog](https://read.acloud.guru/serverless-image-optimization-and-delivery-510b6c311fe5) or [doc](https://serverless.com/framework/docs/providers/aws/guide/credentials/) to set the AWS credentials file. 
```
export AWS_ACCESS_KEY_ID=<your-key-here>
export AWS_SECRET_ACCESS_KEY=<your-secret-key-here>
```

### Deploying
```
serverless deploy
```
Upon success, you can get an endpoints address from the output, say, https://akcpvzfy99.execute-api.us-east-2.amazonaws.com/dev/resize-image

### Testing
Visiting https://akcpvzfy99.execute-api.us-east-2.amazonaws.com/dev/resize-image?f=lie3.png&w=700&q=60

## Reference
https://read.acloud.guru/serverless-image-optimization-and-delivery-510b6c311fe5
https://github.com/andreasonny83/serverless-image-rendering
https://github.com/lambci/docker-lambda
