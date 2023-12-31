## Part 1
### Code for StringServer.java
```
import java.util.*;
import java.io.IOException;
import java.net.URI;
import java.net.URLDecoder;
import java.nio.charset.StandardCharsets;

class Handler implements URLHandler {
    //Adds messages the user types in each time and displays them in order
    
    ArrayList<String> message = new ArrayList<String> ();
    int num = 0; //incremented every time a new input is added
    String output = ""; //What's displayed on the screen

    public String handleRequest(URI url) {
        if (url.getPath().equals("/add-message")) {
            String [] parameters = url.getQuery().split("=");
            if (parameters[0].equals("s")){
                String message = URLDecoder.decode(parameters[1], StandardCharsets.UTF_8);
                num++; 
                output += String.format("%d. %s\n", num, message); //Output Concatenated with a previous output
                return output;
            } 
        }
            return "404 not found!";
        
    }
}
class StringServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}
```

### Using `add-message?s=Hello` as a query.
![image](Hello.png)
- For this query, `handleRequest` in the `Handler` class is called, which checks if the path is /add-message, decodes the message, adds it to the list, and returns the updated list of messages.
- The relevant argument in this method is the url (URI object) and its value is `https://0-0-0-0-3009-os6po68qgh84pjj34bob1tlcls.us.edusercontent.com/add-message?s=Hello`. The argument did not exist before `handleRequest` was executed, and it is provided with the url after the request.
- `ArrayList<String> message` was initially empty and later have "Hello".
- The value of `int num` changed from 0 to 1.
- `String output` was empty, and it changes to "1. Hello\n".
- `message` field got "Hello" added, `num` field was incremented by 1, `output` field was updated with "1. Hello\n" after the request.

### Using `/add-message?s=How%20are%20you` as a query.
![image](Howru.png)
- For this query, `handleRequest` in the `Handler` class is called, which checks if the path is /add-message, decodes the message, adds it to the list, and returns the updated list of messages. 
- The relevant argument in this method is the url (URI object) and its value is `https://0-0-0-0-3009-os6po68qgh84pjj34bob1tlcls.us.edusercontent.com/add-message?s=How%20are%20you` The argument did not exist before `handleRequest` was executed, and it is provided with the url after the request.
- `ArrayList<String> message` was initially empty and later have "Hello".
- The value of `int num` changed from 1 to 2.
- `String output` was "1. Hello\n", and it changes to "1. Hello\n 2. How are you\n".
- `message` field got "How are you" added, `num` field was incremented by 1, `output` field was updated with "1. Hello\n 2. How are you\n" after the request.


## Part2
- Both private key (`id_rsa`) and public key (`id_rsa.pub`) is located in */Users/h4ryu/.ssh* directory on my local computer.

![image](privatekey.png)

- As it is shown in the image below, the path to the public key is */Users/h4ryu/.ssh/id_rsa.pub* on my local computer.
![image](publickey.png)

- The path to the public key on `ieng6` is `/home/linux/ieng6/ca15lfa23/cs15lfa23oc/.ssh/authorized_keys`. `id_rsa.pub` on my local computer is copied into the `.ssh` directory in a file called `authorized_keys`.
  
![image](authorizedkeys.png)

- Below is the terminal interaction showing I logged into `ieng6` without password.

![image](loginnopw.png)


## Part 3
Before week 2, I did not even know what a server is. Now I have learned to compile and run servers using terminal commands. Also, being able to manipulate the NumberServer.java to StringServer.java reminded me of how to work with java classes. Most importantly, I learned how servers and clients are connected and I can log into a remote computer using `ssh` command. Being able to remotely sign in and control a computer distant from my location was interesting to learn. Using `ssh-keygen` command will let me save a lot of time from not having to type the password every time, which I think is going to be useful in the future for signing into remote computers. For week 3, I had a little bit of experience with VS code but never run a terminal on it. Now I know I can run the terminal on VS code, which provides me a better visual representation of the commands.

## Disclaimer: When I tried to save this webpage as a PDF file, it did not show the box around the words when used with with ` (backticks). However, when you visit the webpage https://ryanryucode.github.io/cse15l-lab-reports/ it displays the words in boxes when used with backticks.
