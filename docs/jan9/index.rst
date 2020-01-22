
January 9th, 2020
=================

1. Coded a function in the lambda function get_user_info that returns a row from our chocolate_user DynamoDB

2. Tested my code and it correctly outputted the row I had selected in DynamoDB (user: John Smith)
Output: {'Item': {'last_name': 'Smith', 'email': 'john.smith@gmail.com', 'first_name': 'John', 'age': Decimal('35')}

3. Did a second test with a different row, it was a success (user: Jane Smith)
Output:{'Item': {'last_name': 'Smith', 'email': 'jane.smith@gmail.com', 'first_name': 'Jane', 'age': Decimal('25')}

4. Changed code so that an incorrect email will result in a blank row and a existing email will result in the output of the corresponding row

5. Next, I created a new API gateway, that is fully funtioning. When you enter a parameter, it outputs the corresponding information and when you enter NO parameter, there is a nice response. It is now published on the internet and later I will be able to use this URL while coding in HTML. 
URL:https://y8s2gy3mi8.execute-api.us-east-1.amazonaws.com/prod/user-profile?user_email=mr.coxall@mths.ca

6. I altered my lambda code to trap errors with a try catch statement

7. Used Javascript "Fetch" through index.html to call my API and present the data for "jane.smith@gmail.com" on my website

.. code-block:: python
	:linenos:
	:caption: get_user_info.py Lambda function

	#!/usr/bin/env python3

	# Created by: Trinity Armstrong
	# Created on: Jan 2020
	# This function returns a row from our chocolate_user DynamoDB

	import json
	import boto3
	import decimal


	def replace_decimals(obj):
		# Helper class to Decimals in an arbitrary object
		#   from: https://github.com/boto/boto3/issues/369
	    
	    if isinstance(obj, list):
	        for i in range(len(obj)):
	            obj[i] = replace_decimals(obj[i])
	        return obj
	    elif isinstance(obj, dict):
	        for k, v in obj.items():
	            obj[k] = replace_decimals(v)
	        return obj
	    elif isinstance(obj, set):
	        return set(replace_decimals(i) for i in obj)
	    elif isinstance(obj, decimal.Decimal):
	        if obj % 1 == 0:
	            return int(obj)
	        else:
	            return float(obj)
	    else:
	        return obj


	def lambda_handler(event, context):
	    # get a row from our chocolates_user table
	    
	    dynamodb = boto3.resource('dynamodb')
	    table = dynamodb.Table('chocolate_users')
	    response = table.get_item(
	        Key = {
	            'email':event['email_address']
	        }
	    )
	    
	    try:
	        results = response["Item"]
	        results = replace_decimals(results)
	    except:
	        results = {}
	    
	    return {
	        'statusCode': 200,
	        'body': json.dumps(results)
	    }
