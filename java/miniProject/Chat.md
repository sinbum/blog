# 채팅 프로그램 앱 개발

## Thread 기반의 채팅 서버/클라이언트 만들기

### 채팅 서버 생성

> ChatServerThread.java

```java
package chatting;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.net.InetAddress;
import java.net.ServerSocket;
import java.net.Socket;

public class ChatServerThread {

    private Socket socket=null;
    private ServerSocket server = null;
    int connectCount=0;

    public void serverStart(){
        System.out.println("접속자를 기다리는 중입니다.");
        try {
            server = new ServerSocket(2022);
            socket = server.accept();
            
            InetAddress ia = socket.getInetAddress();
            int port = socket.getLocalPort();// 접속에 사용된 PORT 
            String ip = ia.getHostAddress(); // 원격 Client IP 
            
            ++connectCount;  //접속자수 카운트
            System.out.print(connectCount);
            System.out.print("클라이언트 접속-Local Port: "+ port);
            System.out.println(" Client IP: " + ip);
            
            //데이터를 읽어오는 스레드
            ChatServerReadHandler read = new ChatServerReadHandler(socket);
            read.start();
            //데이터를 보내는 스레드
            ChatServerSendHandlersend = new ChatServerSendHandler(socket);
            send.start();
        } catch(IOException ioe) {
            System.err.println("연결이 되어 있지 않습니다.");
        } finally {
            try {
                server.close();
            } catch(IOException ignored) {}
        }
        
    }

    public static void main(String[] args) {
        ChatServerThread cs = new ChatServerThread();
        cs.serverStart();
    }
}

```

> ChatServerReadHandler.java

- 데이터를 읽어오는 ReadHandler 생성

```java

class ChatServerReadHandler extends Thread{
private Socket socket;
private String line;   //서버로부터 읽어온 문자열 저장

    public ChatServerReadHandler() {
        System.out.println("프로그램이 초기화 되지 않았습니다.");
    }
    
    public ChatServerReadHandler(Socket socket) {
        this.socket = socket;  
    }

    public void run() {
        try {
            BufferedReader reader = new BufferedReader(new InputStreamReader(socket.getInputStream()));
            while(true){
                line = reader.readLine();
                
                if (line == null){ 
                    break;
                }
                System.out.println("받은글: " + line);
                System.out.print("☞ ");
            }

        } catch(IOException ignored) {
        } finally {
            try {
                socket.close();
            } catch(IOException ignored) {}
        }
    }

}
```
- 데이터를 보내는 SendHandler 생성

> ChatServerSendHandler.java
```java
class ChatServerSendHandler extends Thread{
private Socket socket;
private BufferedWriter writer;
private BufferedReader in;           
private String s="";

    public ChatServerSendHandler() {
        System.out.println("프로그램이 초기화 되지 않았습니다.");
    }
    
    public ChatServerSendHandler(Socket socket) {
        this.socket = socket;
        try{
            writer = new BufferedWriter(new OutputStreamWriter(socket.getOutputStream()));
            in = new BufferedReader(new InputStreamReader(System.in));
        } catch (Exception e) {
            System.err.println("연결이 되어 있지 않습니다.");
        }   
    }

    public void run() {
        try {
            while(true) {
                System.out.print("☞ ");
                s = in.readLine(); //키보드로부터 입력
                if(s.equals("999")){
                    break; //종료코드
                }
                writer.write(s);
                writer.newLine();  //줄바뀜 기호가 있어야 BufferedReader의 readLine()이 인식함
                writer.flush();    //client로 전송 

                //System.out.println("보낸 글:" + s);//입력받은 내용 출력
            }
        } catch(Exception ignored) {

        } finally {
            try {
                socket.close();
            } catch(IOException ignored) {}
        }
    }

}

```


### 채팅 클라 생성

> ChatClientThread.java

```java
package chatting;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.net.InetAddress;
import java.net.Socket;

public class ChatClientThread {
private Socket socket = null;

    public void clientStart(String ip){
        System.out.println("클라이언트 프로그램 작동.....");
        try {
            socket = new Socket(ip, 2022);
            
            InetAddress ia = socket.getInetAddress();
            int local_port = socket.getLocalPort();// 접속에 사용된 PORT
            int server_port = socket.getPort();// 접속에 사용된 PORT
            String server_ip = ia.getHostAddress(); // 원격 Client IP 
            
            System.out.print("클라이언트 접속-Local Port: "+ local_port);
            System.out.print(" Server IP: " + server_ip);
            System.out.println(" Server PORT: " + server_port);            
            
            //데이터를 읽어오는 스레드
            ChatClientReadHandler read = new ChatClientReadHandler(socket);
            read.start();
            //데이터를 보내는 스레드
            ChatClientSendHandler send = new ChatClientSendHandler(socket);
            send.start();
            
        } catch(IOException ioe) {
            System.err.println("연결이 되어 있지 않습니다.");
        } finally {
            try {
                if(socket == null){
                    socket.close();                    
                }
            } catch(IOException ignored) {}
        }
       
    }

    public static void main(String[] args) {
        ChatClientThread cc = new ChatClientThread();
        cc.clientStart(args[0]);
    }
}
```

- 데이터를 읽어오는 클라이언트 ReadHandler 생성

```java
class ChatClientReadHandler extends Thread{
private Socket socket;
private String line;   //서버로부터 읽어온 문자열 저장

    public ChatClientReadHandler() {
        System.out.println("프로그램이 초기화 되지 않았습니다.");
    }
    
    public ChatClientReadHandler(Socket socket) {
        this.socket = socket;  
    }

    public void run() {
        try {
            BufferedReader reader = new BufferedReader(new InputStreamReader(socket.getInputStream()));
            while(true){
                line = reader.readLine();
                
                if (line == null){ 
                    break;
                }
                
                System.out.println("받은글: " + line);
                System.out.print("☞ ");
            }
        } catch(IOException ignored) {
            System.err.println("연결이 되어 있지 않습니다.");
        } finally {
            try {
                socket.close();
            } catch(IOException ignored) {}
        }
    }

}
```

- 데이터를 보내는 클라이언트 SendHandler 생성

```java
class ChatClientSendHandler extends Thread{
private Socket socket;
private BufferedWriter writer;
private BufferedReader in;           
private String s="";

    public ChatClientSendHandler() {
        System.out.println("프로그램이 초기화 되지 않았습니다.");
    }
    
    public ChatClientSendHandler(Socket socket) {
        this.socket = socket;
        try{
            writer = new BufferedWriter(new OutputStreamWriter(socket.getOutputStream()));
            in = new BufferedReader(new InputStreamReader(System.in));
        } catch (Exception e) {
            System.err.println("연결이 되어 있지 않습니다.");
        }   
    }

    public void run() {
        try {
            while(true) {
                System.out.print("☞ ");
                s = in.readLine(); //키보드로부터 입력
                if(s.equals("999")){
                    break; //종료코드
                }
                writer.write(s);
                writer.newLine();  //줄바뀜 기호가 있어야 BufferedReader의 readLine()이 인식함
                writer.flush();
                //System.out.println("보낸 글:" + s);//입력받은 내용 출력
            }
        } catch(Exception ignored) {

        } finally {
            try {
                socket.close();
            } catch(IOException ignored) {}
        }
    }

}

```



### 실행 하기

- CMD 를 실행합니다.

```text
C:
cd F:\ChatServerThread 클래스가 있는 폴더경로.
start java chatting.ChatServerThread

start java chatting.ChatClientThread 172.16.3.1
```



## 멀티 채팅 앱 구현하기.

### 멀티 채팅 서버 생성

> ChatServerThreadMulti.java

```java
package multichatting;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.net.InetAddress;
import java.net.ServerSocket;
import java.net.Socket;
import java.util.Vector;

public class ChatServerThreadMulti {

    private Socket socket=null;
    private ServerSocket server = null;
    private Vector user=null;
    int connectCount=0;

    public ChatServerThreadMulti(){
        user = new Vector(20);
    }
    
    public void serverStart(){
        System.out.println("**************************************");
        System.out.println("***** 접속자를 기다리는 중입니다. *****");
        System.out.println("**************************************");
        try {
            server = new ServerSocket(2022);
            while(true){
                socket = server.accept(); //Lock
                
                InetAddress ia = socket.getInetAddress();
                int port = socket.getLocalPort();// 접속에 사용된 PORT 
                String client_ip = ia.getHostAddress(); // 원격 Client IP
                int client_port = socket.getPort();// 원격 Client PORT
                
                ++connectCount;  //접속자수 카운트
                System.out.print(connectCount);
                System.out.print("클라이언트 접속-Local Port: "+ port);
                System.out.print(" Client IP: " + client_ip);
                System.out.println(" Client PORT: " + client_port);
                
                
                //null인 Socket 객체를 Vector에서 제거합니다.
                try{
                    for(int i=0; i< user.size(); i++){
                        Socket s = (Socket)user.get(i);
                        if (s==null){
                            user.remove(i);
                            user.trimToSize();
                        }
                    }
                }catch(Exception e){
                    System.out.println(e.toString());
                }
                user.add(socket);
            
                //데이터를 읽어오는 스레드
                ChatServerReadHandler read = new ChatServerReadHandler(user, socket);
                read.start();
                //데이터를 보내는 스레드
                //ChatServerSendHandler send = new ChatServerSendHandler(user);
                //send.start();
            }
        } catch(Exception e) {
            System.err.println(e.toString());
        } finally {
            try {
                server.close();
            } catch(IOException ignored) {}
        }
        
    }

    public static void main(String[] args) {
        ChatServerThreadMulti cs = new ChatServerThreadMulti();
        cs.serverStart();
    }
}
```

- ReadHandler 생성
> ChatServerReadHandler.java 

```java
class ChatServerReadHandler extends Thread{
private Vector user;
private Socket socket;
private String line;   //서버로부터 읽어온 문자열 저장
private BufferedWriter writer; // 네트워크 전송

    public ChatServerReadHandler() {
        System.out.println("프로그램이 초기화 되지 않았습니다.");
    }
    
    public ChatServerReadHandler(Vector user, Socket socket) {
        this.user = user;
        this.socket = socket;
    }

    public void run() {
        try {
            BufferedReader reader = new BufferedReader(new InputStreamReader(socket.getInputStream()));
            while(true){
                line = reader.readLine();
                
                for(int i=0; i< user.size(); i++){
                    Socket s = (Socket)user.get(i);
                    if(s.isClosed()){
                        user.remove(i);
                        user.trimToSize();
                    }else{
                        writer = new BufferedWriter(new OutputStreamWriter(s.getOutputStream()));
                        writer.write(line);
                        writer.newLine();  //줄바뀜 기호가 있어야 BufferedReader의 readLine()이 인식함
                        writer.flush();
                    }
                }                
                System.out.println(line);
                System.out.println("현재 접속자수: " + user.size());
                //System.out.print("☞ ");
                if (line == null) {
                    break;
                }
            }

        } catch(IOException ignored) {
        } finally {
            try {
                socket.close();
            } catch(IOException ignored) {}
        }
    }

}

```

### 멀티 채팅 클라 생성
> ChatClientThreadMulti.java

```java
package multichatting;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.net.InetAddress;
import java.net.Socket;

public class ChatClientThreadMulti {
private Socket socket = null;

    public void clientStart(String ip, String id){
        System.out.println("클라이언트 프로그램 작동.....");
        try {
            socket = new Socket(ip, 2022);
            
            InetAddress ia = socket.getInetAddress();
            int local_port = socket.getLocalPort();// 접속에 사용된 PORT
            int server_port = socket.getPort();// 접속에 사용된 PORT
            String server_ip = ia.getHostAddress(); // 원격 Client IP 
            
            System.out.print("클라이언트 접속-Local Port: "+ local_port);
            System.out.print(" Server IP: " + server_ip);
            System.out.println(" Server PORT: " + server_port);            
            
            //Server와 통신할 스레드 구현 클래스
            ChatClientReadHandler read = new ChatClientReadHandler(socket, id);
            read.start();
            ChatClientSendHandler send = new ChatClientSendHandler(socket, id);
            send.start();
            
        } catch(IOException e) {
            System.err.println(e.toString());
        } finally {
            try {
                if(socket == null){
                    socket.close();                    
                }
            } catch(IOException ignored) {}
        }
       
    }

    public static void main(String[] args) {
        ChatClientThreadMulti cc = new ChatClientThreadMulti();
        cc.clientStart(args[0], args[1]);
    }
}
```

- 클라이언트 ReadHandler 생성
> ChatClientReadHandler.java

```java
class ChatClientReadHandler extends Thread{
private Socket socket;
private String line;   //서버로부터 읽어온 문자열 저장
private String id;     //대화명

    public ChatClientReadHandler() {
        System.out.println("프로그램이 초기화 되지 않았습니다.");
    }
    
    public ChatClientReadHandler(Socket socket, String id) {
        this.socket = socket;  
        this.id = id;
    }

    public void run() {
        try {
            BufferedReader reader = new BufferedReader(new InputStreamReader(socket.getInputStream()));
            while(true){
                line = reader.readLine();
                if (line == null) {
                    break;
                }
                System.out.println(line);
            }
        } catch(Exception e) {
            System.err.println(e.toString());
        } finally {
            try {
                socket.close();
            } catch(IOException ignored) {}
        }
    }

}
```
- 클라이언트 SendHandler 생성
> ChatClientSendHandler.java

```java
class ChatClientSendHandler extends Thread{
private Socket socket;
private BufferedWriter writer;
private BufferedReader in;           
private String s;
private String id;

    public ChatClientSendHandler() {
        System.out.println("프로그램이 초기화 되지 않았습니다.");
    }
    
    public ChatClientSendHandler(Socket socket, String id) {
        this.socket = socket;
        this.id = id;
        try{
            writer = new BufferedWriter(new OutputStreamWriter(socket.getOutputStream()));
            in = new BufferedReader(new InputStreamReader(System.in));
        } catch (Exception e) {
            System.err.println(e.toString());
        }   
    }

    public void run() {
        try {
            while(true) {
                try {
                  //System.out.print(id + ": ");
                  s = in.readLine(); //키보드로부터 입력
                  if(s.equals("999")){
                      break; //종료코드
                  }
                  writer.write(id + ": " + s);
                  writer.newLine();  //줄바뀜 기호가 있어야 BufferedReader의 readLine()이 인식함
                  writer.flush();
                } catch (Exception e) {
                }    
            }
        } catch(Exception ignored) {

        } finally {
            try {
                socket.close();
            } catch(IOException ignored) {}
        }
    }

}
```
### 실행 하기

```text
실행:
C:
cd C:\ChatServerThreadMulti 자바 파일 경로
start java multichatting.ChatServerThreadMulti
start java multichatting.ChatClientThreadMulti {ip 주소} {아이디}
```




