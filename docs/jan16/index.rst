
January 16th, 2020
==================

1. I created a ``profile.html`` file in order to add our user's profile to my webpage once signed in

2. I did this by copying my ``sign-out.html`` code

3. removing the sign-out code from my ``profile.html`` file

4. copying getUserAttributes() function from ``sign-in.html`` to add to my file

5. copying  getUser() function from ``temp.html`` to add to my file

6. I confirmed that my code was running correctly by signing in, and checking the profile page that had successfully outputted my profile information

.. code-block:: html
  :linenos:
  :caption: profile.html

  <!doctype html>
  <html lang="en">
    <head>
      <meta charset="utf-8">
      <!--Cognito JavaScript-->
      <script src="js/amazon-cognito-identity.min.js"></script>  
      <script src="js/config.js"></script>
    </head>

    <body>
    <div class="container">
      <div>
        <h1>Profile</h1>
      </div>
      <div id='profile'>
        <p></p>
      </div>
    <div>
        
      <br>
      <div id='home'>
        <p>
          <a href='./index.html'>Home</a>
        </p>
      </div>

    <script>
      
      async function getUser(email_address) {
        // get the user info from API Gate
        
        const api_url = 'https://gonvpjbyuf.execute-api.us-east-1.amazonaws.com/prod/user-profile?user_email=' + email_address;
        const api_response = await fetch(api_url);
        const api_data = await(api_response).json();
        console.log(api_data);
        
        const div_user_info = document.getElementById('profile');
        div_user_info.innerHTML = api_data['body'];
        }
        
      var data = { 
        UserPoolId : _config.cognito.userPoolId,
          ClientId : _config.cognito.clientId
        };
        var userPool = new AmazonCognitoIdentity.CognitoUserPool(data);
        var cognitoUser = userPool.getCurrentUser();
    
        window.onload = function(){
          if (cognitoUser != null) {
            cognitoUser.getSession(function(err, session) {
              if (err) {
                alert(err);
                return;
              }
              //console.log('session validity: ' + session.isValid());
              
              cognitoUser.getUserAttributes(function(err, result) {
                if (err) {
                  console.log(err);
                  return;
                }
                // user email address
                console.log(result[2].getValue());
                getUser(result[2].getValue()) 
              });
    
            });
          } else {
            console.log("Already signed-out")
          }
        }
      </script>
      
    </body>
  </html>
