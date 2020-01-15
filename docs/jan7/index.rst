
January 7th 2020
================
1. I created a index.html file in the root of my Cloud9. This contains the code for "Hello, World!" that I will be using to test my new website once I have connected to Amplify.

2. Next, I pushed all the changes I have made to my github repo in my master terminal. This includes my index.html file.

3. Finally, I connected this instance to Amplify. I did this by going to my dashboard and opening AWS amplify through the services tab. From there, I was able to create my Amplify instance connected to GitHub and deploy my hello world program. I was able to confirm through the provided URL that my code is up and running correctly.

4. Created a role in IAM called "AWS_Serverless_Web_App" through AWS Identitiy and Access Management (IAM). After creating my database, I will be able to use this role for AWS Lambda to access it.

5. I created a lambda function in python that returns "Hello, World!" on AWS

6. I was able to test and confirm that this function was running correctly using test cases

7. using considered test event, I passed my name Trinity Armstrong into the function. It outputted "Hello, Trinity Armstrong".