# JSEasy1


![Pasted image 20210327192020.png](./Pasted%20image%2020210327192020.png)

## View Source

![Pasted image 20210327192747.png](./Pasted%20image%2020210327192747.png)

## Function Login
http://docker.h4x0rbox.com:2010/assests/script.js

```javascript

function login(){

    var username = document.getElementById("inputUser").value;
    var password = document.getElementById("inputPassword").value;

    var Secret = \["admin:SeCRET213#\_T"\];  //username and password
    for (i = 0; i < Secret.length; i++)
    {
        if (Secret\[i\].indexOf(username) == 0)
        {
            var Split = Secret\[i\].split(":"); #spliting secret by ':'
            var TheUsername = Split\[0\]; #username
            var ThePassword = Split\[1\]; #password
            if (username == TheUsername && password == ThePassword)
            {
                alert("You can use this password as a flag Sl7{})"); //successfull login
            }
        }
        else
        {
            alert("NooOOooo.")
        }
    }

}

```

### Flag : `Sl7{SeCRET213#_T}`
