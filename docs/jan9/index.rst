
January 9th, 2020
=================

1. Coded a function in the lambda function get_user_info that returns a row from our chocolate_user DynamoDB

2. Tested my code and it correctly outputted the row I had selected in DynamoDB (user: John Smith)
Output: {'Item': {'last_name': 'Smith', 'email': 'john.smith@gmail.com', 'first_name': 'John', 'age': Decimal('35')}

3. Did a second test with a different row, it was a success (user: Jane Smith)
Output:{'Item': {'last_name': 'Smith', 'email': 'jane.smith@gmail.com', 'first_name': 'Jane', 'age': Decimal('25')}

4. Changed code so that an incorrect email will result in a blank row and a existing email will result in the output of the corresponding row
