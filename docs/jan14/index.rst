
January 14th, 2020
==================

1. I created a javascript folder called "js"

2. I downloaded the JavaScript libraries "amazon-cognito-auth.min", "amazon-cognito-identity.min", "and config.js" into the folder "js"

3. I updated the "config.js" file with my app information from AWS Cognito

4. Typed the code for my sign in page in the file "sign-in.html". This runs 2 input boxes for your email address and password and a sign-in button

5. I signed into my confirmed account and it successfully outputted "You are logged in as: trinity.armstrong@ocsbstudent.ca"

.. code-block:: html
  :linenos:
  :caption: sign-in.html

  <!DOCTYPE html>

  <html lang="en">
    <head>
    <meta charset="utf-8">

      <!-- Javascript SDKs-->
      <script src="https://code.jquery.com/jquery-3.4.1.min.js"></script>
      <script src="js/amazon-cognito-auth.min.js"></script>
      <script src="https://sdk.amazonaws.com/js/aws-sdk-2.596.0.min.js"></script> 
      <script src="js/amazon-cognito-identity.min.js"></script>   
      <script src="js/config.js"></script>
    </head>

    <body>
      <form>
        <h1>Please sign in</h1>

        <input type="text" id="inputUsername"  placeholder="Email address" name="username" required autofocus>
        <input type="password" id="inputPassword"  placeholder="Password" name="password" required>    
        <button type="button" onclick="signInButton()">Sign in</button>
      </form>

      <br>
      <div id='logged-in'>
        <p></p>
      </div>

      <p>
        <a href="./profile.html">Profile</a>
      </p>

      <br>
      <div id='home'>
        <p>
          <a href='./index.html'>Home</a>
        </p>
      </div>

      <script>

        var data = { 
          UserPoolId : _config.cognito.userPoolId,
          ClientId : _config.cognito.clientId
        };
        var userPool = new AmazonCognitoIdentity.CognitoUserPool(data);
        var cognitoUser = userPool.getCurrentUser();

        function signInButton() {
          // sign-in to AWS Cognito

          var authenticationData = {
            Username : document.getElementById("inputUsername").value,
            Password : document.getElementById("inputPassword").value,
          };

          var authenticationDetails = new AmazonCognitoIdentity.AuthenticationDetails(authenticationData);

          var poolData = {
            UserPoolId : _config.cognito.userPoolId, // Your user pool id here
            ClientId : _config.cognito.clientId, // Your client id here
          };

          var userPool = new AmazonCognitoIdentity.CognitoUserPool(poolData);

          var userData = {
            Username : document.getElementById("inputUsername").value,
            Pool : userPool,
          };

          var cognitoUser = new AmazonCognitoIdentity.CognitoUser(userData);

          cognitoUser.authenticateUser(authenticationDetails, {
              onSuccess: function (result) {
                var accessToken = result.getAccessToken().getJwtToken();
                console.log(result);  

                //get user info, to show that you are logged in
                cognitoUser.getUserAttributes(function(err, result) {
                    if (err) {
                      console.log(err);
                      return;
                    }
                    console.log(result);
                    document.getElementById("logged-in").innerHTML = "You are logged in as: " + result[2].getValue();
                });

              },
              onFailure: function(err) {
                alert(err.message || JSON.stringify(err));
              },
          });
        }
      </script>

    </body>
  </html>

.. raw:: html

  <div style="text-align: center; margin-bottom: 2em;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/b72PvMBcVTw" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen>
    </iframe>
  </div>
