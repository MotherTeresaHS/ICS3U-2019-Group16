
January 8th 2020
================
1. Created a DynamoDB table called "choclate_user" with email as my primary key

2. Created rows in the table to ensure that is working correctly. I used the following information: first_name, last_name and age of the user

3. I changed the capacity of my table from 5 to 1 in order to save money, as that is more than enough for the services I will be needing

4. Created a new lambda function called get_user_info

.. code-block:: python
	:linenos:
	:caption: hello_world.py Lambda function

	#!/usr/bin/env python3

	# Created by: Trinity Armstrong
	# Created on: Jan 2020
	# This function is the Hello, World! Lambda function

	import json

	def lambda_handler(event, context):
	    # TODO implement
	    
	    return_var = {
	        'statusCode': 200,
	        'body': json.dumps('Hello, ' + event['name'])
	    }
	    
	    return return_var

5. copy pasted my code from the hello_world lambda function into my new function

6. Tested my new lambda function by outputting "Hello, Trinity Armstrong"

