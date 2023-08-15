<h2>🛠️ Deploy Steps:</h2>


<p>1. Go to AWS and Set Lambda Function</p>

```
Run time can be python or language that you want
```

<p>2. Write the code for Lambda Function</p>

```
You can edit Test configuration and test your code
```

<p>3. Use API Gateway to build method connect to Lambda Function</p>

```
When creating Lambda Function method remeber set the correct Lambda Function
```

<p>4. In API Gateway remember to click on Action and enable CORS</p>

<p>5. In Actions Deploy API</p>

```
set New Stage -> set Name
```

<p>6. Copy the URL in Stage Editor</p>

<p>7. Go to DynamoDB and create a table</p>

```
Copy the ARN for your table
```

<p>8. Go back to Lambda Function and go to Configuration</p>

```
Click on Permission
```

<p>19. Create an in line policy and Create the Policy</p>

```
{ "Version": "2012-10-17"
  "Statement": [
      {
         "Sid": "VisualEditor0",
         "Effect": "Allow",
         "Action": [
             "dynamodb:PutItem",
             "dynamodb:DeleteItem",
             "dynamodb:GetItem",
             "dynamodb:Scan",
             "dynamodb:Query",
             "dynamodb:UpdateItem",
         ]
  "Resource": "TABLE-ARN"
}
    ]
 }
```

<p>10. Go to Lambda Function Code paste your DynamoDB ARN</p>

```
import json
import math
import boto3
from time import gmtime, strftime

dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table('PowerOfMathDatabase')

now = strftime("%a %d %b %Y %H:%M:%S +0000", gmtime())

def lambda_handler(event, context):
    mathResult = math.pow(int(event['base']), int(event['exponent']))

    response = table.put_item(
        Item={
            'ID': str(mathResult),
            'LatestGreetingTime': now
        })

    return {
        'statusCode': 200,
        'body': json.dumps('Your result is ' + str(mathResult))
    }

```

<p>11. Now go back to your local File add api to your file and make sure your step 8 url is used</p>

<p>12. Create page file in React Vue Javascript or HTML</p>

<p>13. Deploy the zipped static file into Ampliy Or connect to github and Set Up Build and Deploy Settings in Amplify</p>


<p>14. Now you finished</p>
