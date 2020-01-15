
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