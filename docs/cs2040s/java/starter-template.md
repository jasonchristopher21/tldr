---
sidebar_position: 1
---

# Kattis Starter Template

As this module would require faster input-output methods, the following shows a quick template I use normally. The template is equipped with the following

- Imports all libraries in `java.util`
- Imports all libraries in `java.io`
- Uses `BufferedReader` and `PrintWriter` for reading inputs and displaying outputs

You need to, however, change the name of the class. `public` identifier is optional. 

```java title="YourClassName.java"
import java.util.*;
import java.io.*;

public class YourClassName {
    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        PrintWriter pw = new PrintWriter(System.out);

        // YOUR CODE HERE

        pw.flush();
    }
}
```