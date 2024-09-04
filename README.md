# ETE-amplify-lambda-apiGateway-dynamodb-IAM

![image](https://github.com/user-attachments/assets/99594905-3255-4513-955e-ac6552c7b9c5)

![image](https://github.com/user-attachments/assets/8856933f-7f0b-46be-9b0a-323192bfd183)

# 0- create and zip and index.html

![image](https://github.com/user-attachments/assets/f258c636-abdf-49a2-9e32-1905101549d2)

# 1-go to amplify
![image](https://github.com/user-attachments/assets/ed1fbc2c-27ed-4e4d-8739-5893bb8b3e79)

![image](https://github.com/user-attachments/assets/acf3cc08-18b5-4f7d-8c8b-9e8ad34aa729)

![image](https://github.com/user-attachments/assets/0385b11e-1fd4-46db-ab27-e7389558e8ff)

![image](https://github.com/user-attachments/assets/2ec35b9c-8265-430d-9ffa-f39d180c6ddd)

![image](https://github.com/user-attachments/assets/33c1e2d8-8566-485c-8233-33ee29349b5a)

![image](https://github.com/user-attachments/assets/b07d171b-3ec8-4304-91a0-07f538808061)

# 2- Lambda function

import json

import math

def lambda_handler(event, context):

    mathResult = math.pow(int(event['base']),int(event['exponent']))
    
    return {
    
        'statusCode': 200,
        
        'body': json.dumps('You result is '+ str(mathResult))
        
    }


![image](https://github.com/user-attachments/assets/953c0ff5-3e9a-4633-ae83-89243d2e3cb6)

![image](https://github.com/user-attachments/assets/ef370f7d-4bbe-4342-b404-725591346d05)

![image](https://github.com/user-attachments/assets/4e5970b7-e690-44ed-b35d-d0052ca04102)

![image](https://github.com/user-attachments/assets/fa9ea766-2ade-4e7e-b29f-00417046036c)

![image](https://github.com/user-attachments/assets/317bb6a7-4c7e-432a-a190-1088a527c364)

![image](https://github.com/user-attachments/assets/8ccf7f44-c824-45af-9495-35f80cda846c)

![image](https://github.com/user-attachments/assets/232366d8-18cd-4219-abdb-4e73f227fd5a)

# 3 - API Gateway

![image](https://github.com/user-attachments/assets/ea452904-e855-41fa-8ebc-0f0506415aad)

![image](https://github.com/user-attachments/assets/c6e5e94b-2dd9-4711-a5a2-69382ba2af3a)

![image](https://github.com/user-attachments/assets/a690c141-a535-493b-bfe6-25cf271fe65f)

![image](https://github.com/user-attachments/assets/879de339-bd42-4eaf-9c2d-059c8d4da6e7)

![image](https://github.com/user-attachments/assets/c0dcb594-a0fa-4495-a2f1-31c39d8a0dcc)

![image](https://github.com/user-attachments/assets/392e2633-077f-4d0b-825a-8082fc8ccc81)

![image](https://github.com/user-attachments/assets/78ffb096-da09-4c2f-a401-edb0d840feb1)

![image](https://github.com/user-attachments/assets/ea408f95-f06e-4af5-a966-e3ce4ce396dc)

![image](https://github.com/user-attachments/assets/97309df9-d721-4101-aa95-d77e3b5fb791)

### copy and save the URL

![image](https://github.com/user-attachments/assets/78265e9c-d935-4c66-8bc0-6de1b1f95686)

![image](https://github.com/user-attachments/assets/88136f16-b135-4809-8802-efd54c1b7ccf)

![image](https://github.com/user-attachments/assets/3b36ea6b-395d-4f7d-b1c4-9a759f4f8649)

![image](https://github.com/user-attachments/assets/bd3eee26-de14-422f-b600-4e579e0031f2)

![image](https://github.com/user-attachments/assets/1e9d8823-8c2d-4fdd-97f3-28ce82df3d7c)

# 4-Dynamodb

![image](https://github.com/user-attachments/assets/d9398864-cc21-4550-b131-c2df690bfc3e)

![image](https://github.com/user-attachments/assets/accc593d-c328-41bc-a397-53179aee8d8b)

![image](https://github.com/user-attachments/assets/4106a123-43c0-4c43-afbd-ea73cc87a3f1)

![image](https://github.com/user-attachments/assets/1b78fe71-17c0-48b3-b29b-55f694b2f2bb)

## copy and save the arn of the database and give lambda permission to write in the table

![image](https://github.com/user-attachments/assets/1d3c3abd-ec93-410b-83cd-19c3182b96ed)

![image](https://github.com/user-attachments/assets/c319a702-37cb-477a-879b-97de8dde85f1)

![image](https://github.com/user-attachments/assets/d73dc31e-0491-4470-a115-ab642f8ef354)

## create inline policy , choose JSON

![image](https://github.com/user-attachments/assets/5ca445bb-6182-4121-b185-e4f992e71333)

![image](https://github.com/user-attachments/assets/7285ed41-74e6-4a2d-b8b5-3f66ba25cd21)

![image](https://github.com/user-attachments/assets/bedeb543-1bd8-424f-97d8-dfad0cda55fc)




import json

import math

import boto3

from time import gmtime, strftime

dynamodb = boto3.resource('dynamodb')

table = dynamodb.Table('PowerOfMathDatabase')

now = strftime("%a, %d %b %Y %H:%M:%S +0000", gmtime())

def lambda_handler(event, context):

    mathResult = math.pow(int(event['base']), int(event['exponent']))
    
    response = table.put_item(
    
        Item={
        
            'ID': str(mathResult),
            'LatestGreetingTime':now
            })

    return {
    'statusCode': 200,
    'body': json.dumps('Your result is ' + str(mathResult))
    }

![image](https://github.com/user-attachments/assets/4b2367ec-6083-47f1-945a-ea43f455a517)

![image](https://github.com/user-attachments/assets/b777ac1c-3a61-46ec-b2e4-0ee60db50e0b)

![image](https://github.com/user-attachments/assets/9f2ab369-05e7-4df3-8afd-3d8941733628)

![image](https://github.com/user-attachments/assets/cf864230-7ccd-4337-afe2-16f23e91c6d9)

![image](https://github.com/user-attachments/assets/3b390abf-6e37-4c60-bc55-dcc9e0e3359f)
