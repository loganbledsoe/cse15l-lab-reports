# Lab 1

## Part 1

**With No Arguments**
```
import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;
import java.util.List;

class Handler implements URLHandler {
    List<String> messages = new ArrayList<>();
    private static final String ERROR_MESSAGE = "404 Not Found!";

    public String handleRequest(URI url) {
        //check for /add-message path
        if (!url.getPath().equals("/add-message")) {
            return ERROR_MESSAGE;
        }

        String parameters = url.getQuery();
        int index = parameters.indexOf("&user=");

        //check that both parameters exist
        if (!parameters.startsWith("s=") || index == -1) {
            return ERROR_MESSAGE;
        }

        //extract parameters
        String message = parameters.substring(2, index);
        String user = parameters.substring(index + 6);

        //format <user>: <message>
        String formattedMessage = user + ": " + message;

        //add to messages
        messages.add(formattedMessage);

        return getDisplay();

    
    }

    //returns string that is a concatenation all
    //strings in messages with newlines inbetween
    private String getDisplay() {
        String result = "";
        for (String str : messages) {
            result += str + "\n";
        }
        return result;
    }
}

class ChatServer {

    private static final String PORT_ERROR_MESSAGE =
            "Missing port number! Try any number between 1024 to 49151";

    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println(PORT_ERROR_MESSAGE);
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}

```
