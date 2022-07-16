# Cloud-Resume-Challenge-Part-II- Developing a Hello, World application via CloudFormation


In the second part of this series we will start with IAC. Before defining and deploying our resources as infrastructure as code let's start by downloading sam cli. 
You can download here:
https://aws.amazon.com/serverless/sam/#:~:text=The%20AWS%20Serverless%20Application%20Model,and%20model%20it%20using%20YAML.

![image](https://user-images.githubusercontent.com/96833570/179353126-4cd0cd23-6827-471f-b5e2-f79623c7ad05.png)

After it is finished, verify the installation by running the following command:

`sam --version`

Your output will be similar to this:

`SAM CLI, version 1.53.0`

Let's start building our static website utilizing S3 bucket.

## Getting started with SAM- SAM init

First of all change directory to your repo and then type the following:

`sam init`

![image](https://user-images.githubusercontent.com/96833570/179353287-6c863b3b-8f6d-4446-b065-806970a87e33.png)

![image](https://user-images.githubusercontent.com/96833570/179353323-a34ec2bb-f662-46ea-97da-9b1cb3ee0982.png)


![image](https://user-images.githubusercontent.com/96833570/179353477-1086a040-cce5-459d-bb8d-c9423dfca967.png)

Let's verify the process. Change directory and simply type `ls -la`
![image](https://user-images.githubusercontent.com/96833570/179354357-fe94e6bc-b6f0-4e43-abf9-feb0bbb92c33.png)


### SAM build

Let's run the following command to deploy our simple hello-world application

`sam build`

![image](https://user-images.githubusercontent.com/96833570/179354842-c394e50e-d269-4229-887d-f36e5fa0550f.png)


### Adjusting permissions

We need to set the IAM permissions for SAM. We need to attach the following permission to the group of our IAM user account. 


**IAMFullAccess**: 

![image](https://user-images.githubusercontent.com/96833570/179354538-2d870628-f804-44a2-9a29-910c863f45e6.png)

![image](https://user-images.githubusercontent.com/96833570/179354607-9d907e33-7f4b-4767-83fd-5545c7a473d3.png)

**AWSCloudFormationFullAccess**

![image](https://user-images.githubusercontent.com/96833570/179354648-20c9966e-0b53-43f8-8da0-6dee7de22fcf.png)

**AWSLambda_FullAccess**

![image](https://user-images.githubusercontent.com/96833570/179354679-1118fce3-bf66-45a5-b345-347814e38e5f.png)

**AmazonAPIGatewayAdministrator**

![image](https://user-images.githubusercontent.com/96833570/179354713-4a245e6c-315c-40e5-8227-0370d5570734.png)

![image](https://user-images.githubusercontent.com/96833570/179354738-fcf0f7c2-87ff-4f5e-8005-7ada46924f5b.png)

## SAM deploy

`aws-vault exec robin --no-session -- sam deploy --guided`  

Change robin with your IAM user.

Then go to cloud formation to see the deployment process.


![image](https://user-images.githubusercontent.com/96833570/179354958-5b4da937-e45b-4cac-99da-8f48f9501d36.png)


What is happening in Cloud formation?

Cloud formation tool is deploying the resources (the serverless function) we defined in our template.



![image](https://user-images.githubusercontent.com/96833570/179355073-70c6a7ca-4fbe-4ff4-b9db-69f19d477a84.png) ![image](https://user-images.githubusercontent.com/96833570/179355092-dfc2ab3a-ea8b-4466-b319-fa5d31174505.png)

## Defining an S3 bucket resource in `template.yaml` file

Go ahead into your template.yaml file and copy and paste the following under your resources section.


![image](https://user-images.githubusercontent.com/96833570/179355216-604f46ef-77e4-4136-bd4a-29e04568d8eb.png)

As you can see we have only one resource which is lambda. 

![image](https://user-images.githubusercontent.com/96833570/179355326-33ac7fc0-7731-46bc-9885-4c72d2c98d97.png)

```
Resources:


  Website:
    Type: AWS::S3::Bucket
    Properties:
      BucketName: cloud-res-bucket
```

![image](https://user-images.githubusercontent.com/96833570/179355370-294b15cf-2c90-4801-9c6b-d474737b279c.png)

Run `sam build` again.

![image](https://user-images.githubusercontent.com/96833570/179356189-9bbe2a54-2b63-4783-bbbc-60d6eab8a943.png)


Let's create our S3 bucket by running `aws-vault exec robin --no-session -- sam deploy`.

![image](https://user-images.githubusercontent.com/96833570/179356262-954627be-4e44-4af7-a99b-e97f628f1bbd.png)

### Displaying your bucket

`aws-vault exec robin aws s3 ls`

![image](https://user-images.githubusercontent.com/96833570/179356361-55584f32-a1ef-402e-8d44-307a71a16dcc.png)


### Summary

In the second part, we have simply deployed an S3 bucket via CloudFormation. 














