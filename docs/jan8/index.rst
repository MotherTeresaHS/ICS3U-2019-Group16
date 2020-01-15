
January 8th 2020
================
1. Created a DynamoDB table called "choclate_user" with email as my primary key

2. Created rows in the table to ensure that is working correctly. I used the following information: first_name, last_name and age of the user

3. I changed the capacity of my table from 5 to 1 in order to save money, as that is more than enough for the services I will be needing

4. Created a new lambda function called get_user_info

.. code-block:: python
	:linenos:
	:caption: get_user_info.py Lambda function

5. copy pasted my code from the hello_world lambda function into my new function

6. Tested my new lambda function by outputting "Hello, Trinity Armstrong"

