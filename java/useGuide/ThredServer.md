# 다중 접속 서버 (TreadServer 만들기)

## Multi-threading 
Multi-threading 을 이용한 다중 접속 서버, 문자열 전송
    - 동시에 많은 접속자를 처리할 수 있습니다.

### 서버 생성
> ThreadServer.java

```java
import java.io.*;
import java.net.*;

public class ThreadServer {
public static void main(String[] args) {
System.out.println("****************************************");
System.out.println("Thread를 이용한 다중 접속 서버 작동됨...");
System.out.println("****************************************");

        ServerSocket server = null;
        int connectCount=0;
        
        try {
            server = new ServerSocket(2007);

            while(true) {
                Socket client = server.accept();

                InetAddress ia = client.getInetAddress();
                int port = client.getLocalPort();// 접속에 사용된 PORT 
                String ip = ia.getHostAddress(); // 원격 Client IP 
                
                ++connectCount;  //접속자수 카운트
                System.out.print(connectCount);
                System.out.print("클라이언트 접속-Local Port: "+ port);
                System.out.println(" Client IP: " + ip);
                
                //Client와 통신할 스레드 구현 클래스
                Handler handler = new Handler(client);
                handler.start();
            }
        } catch(IOException ioe) {
            System.err.println("Exception generated...");
        } finally {
            try {
                server.close();
            } catch(IOException ignored) {}
        }
    }
}
```

> Handler.java

```java
class Handler extends Thread {
protected Socket socket;

    public Handler(Socket socket) {
     //Client와 통신할 객체를 초기값으로 받아 할당합니다.
        this.socket = socket;  
    }

    public void run() {
        try {
            BufferedWriter writer = new BufferedWriter(new OutputStreamWriter(socket.getOutputStream()));
            //버퍼에 문자열을 기록함
            writer.write("스레드 다중접속 서버 접속");
            writer.newLine();
            writer.write("\n★ 등산했던 산들 ★\n");
            writer.write("----------------------------------------\n");
            writer.write("1. 관악산, 도봉산, 사패산, 수락산, 파평산");
            writer.newLine();
            writer.write("\n★ 기억에남는 영화 ★\n");
            writer.write("----------------------------------------\n");
            writer.write("1. 우주전쟁, 쏘우");
            writer.newLine();
         
            //실제로 Client로 전송함  
            writer.flush();

        } catch(IOException ignored) {
        } finally {
            try {
                socket.close();
            } catch(IOException ignored) {}
        }
    }
}

```

### 클라 생성
> ThreadClient.java

```java
import java.io.*;
import java.net.*;

public class ThreadClient {
public static void main(String[] args) {
System.out.println("클라이언트 프로그램 작동.....");

        Socket socket = null;
        String line;   //서버로부터 읽어온 문자열 저장
        int cnt=0;
        
        try {
            socket = new Socket(args[0], 2007);  

            InetAddress ia = socket.getInetAddress();
            int port = socket.getLocalPort();// 접속에 사용된 PORT 
            String ip = ia.getHostAddress(); // 원격 Client IP 
            
            System.out.print("클라이언트 접속-Local Port: "+ port);
            System.out.println(" Server IP: " + ip);
            
            //서버로부터 데이터를 입력받아 버퍼에 저장합니다.
            BufferedReader reader = new BufferedReader(new InputStreamReader(socket.getInputStream()));
            
            //버퍼로부터 한 라인씩 읽어 출력합니다.
            while(true){
                try{
                    //cnt++;
                    //System.out.println("순환중입니다.:" + cnt);
                
                    //서버로부터 출력되는 내용을 읽어오기위해 
                    //순환하면서 기다립니다.
                    line = reader.readLine();

                    if (line == null){ 
                        break;
                    }
                    
                    //불규칙적으로 입력되는 데이터를 입력 받을시 지정 
                    //Thread.sleep(10);
                    
                    System.out.println(line);
                }catch(Exception e){
                    System.out.println(e.toString());
                }
            }
        } catch(IOException ioe) {
            System.err.println("Exception generated...");
        } finally {
            try {
                socket.close();
                System.out.println("서버와의 접속을 종료합니다.");
            } catch(Exception ignored) {}
        }

        //아무키나 누를 때까지 대기합니다.
        InputStream is = System.in;
        try{
            is.read();
        }catch(Exception e){
            
        }   
        System.out.println("서버 프로그램 실행을 종료합니다.");        
    }
}
```


### 실행 하기

```text
C:
cd C:서버 경로
start java ThreadServer
start java ThreadClient {고정ip호스팅주소}
```

## 다중 접속 동시 처리

Multi-threading을 이용한 다중 접속 서버, 난수 발생을 이용한 실시간 주가 전송
    - 동시에 많은 접속자를 처리할 수 있습니다.

### 서버 생성
> ThreadServer2.java

```java
import java.io.*;
import java.net.*;
import java.text.*;

public class ThreadServer2 {
public static void main(String[] args) {
System.out.println("****************************************");
System.out.println("Thread를 이용한 다중 접속 서버 작동됨 2..");
System.out.println("****************************************");


        ServerSocket server = null;
        int connectCount=0;
        try {
            server = new ServerSocket(2007);

            while(true) {
                Socket client = server.accept();

                InetAddress ia = client.getInetAddress();
                int port = client.getLocalPort();// 접속에 사용된 PORT 
                String ip = ia.getHostAddress(); // 원격 Client IP 
                
                ++connectCount;  //접속자수 카운트
                System.out.print(connectCount);
                System.out.print("클라이언트 접속-Local Port: "+ port);
                System.out.println(" Client IP: " + ip);
                
                //Client와 통신할 스레드 구현 클래스
                StockHandler handler = new StockHandler(client);
                handler.start();
            }
        } catch(IOException ioe) {
            System.err.println("Exception generated...");
        } finally {
            try {
                server.close();
            } catch(IOException ignored) {}
        }
    }
}
```
> StockHandler.java

```java
class StockHandler extends Thread {
protected Socket socket;

    public StockHandler(Socket socket) {
        //Client와 통신할 객체를 초기값으로 받아 할당합니다.
        this.socket = socket;  
    }

    public void run() {
        try {
            BufferedWriter writer = new BufferedWriter(new OutputStreamWriter(socket.getOutputStream()));
            double d;
            int min=1000;
            int max=1000000;
            int rnd=0;
            int count=0;
            DecimalFormat comma = new DecimalFormat("###,##0");
            
            writer.write("개발자A 스레드 다중접속 서버에 접속 하신것을 환영 합니다.");
            writer.newLine();
            
            while(true){
                count++;
                //1000 ~ 1000000 사이의 난수 발생
                //----------------------------------
                d = Math.random(); 
                rnd = ((int)(d*((max-min)+1))+min); 
                //----------------------------------                
                String s = comma.format(rnd);
                writer.write("종목:" + count + "  주가:" + s);
                writer.newLine();
            
                //Client로 전송함  
                writer.flush();
                sleep(2000);  //2초 sleep
            }
        }catch(InterruptedException e){
            System.out.println(e.toString());
        }
        catch(IOException e) {
            System.out.println(e.toString());
        }finally {
            try {
                socket.close();
            } catch(IOException ignored) {}
        }
    }
}
```

### 클라 생성

> ThreadClient2.java

```java
import java.io.*;
import java.net.*;

public class ThreadClient2 {
public static void main(String[] args) {
System.out.println("클라이언트 프로그램 작동.....");

        Socket socket = null;
        String line;   //서버로부터 읽어온 문자열 저장
        int cnt=0;
        
        try {
            socket = new Socket(args[0], 2022);  

            InetAddress ia = socket.getInetAddress();
            int local_port = socket.getLocalPort();// 접속에 사용된 PORT
            int server_port = socket.getPort();// 접속에 사용된 PORT
            String ip = ia.getHostAddress(); // 원격 Client IP 
            
            System.out.print("클라이언트 접속-Local Port: "+ local_port);
            System.out.print(" Server IP: " + ip);
            System.out.println(" Server PORT: " + server_port);
                        
            //서버로부터 데이터를 입력받아 버퍼에 저장합니다.
            BufferedReader reader = new BufferedReader(new InputStreamReader(socket.getInputStream()));
            
            //버퍼로부터 한 라인씩 읽어 출력합니다.
            while(true){
               System.out.println("순환중입니다.:" + cnt++);
                
               //서버로부터 출력되는 내용을 읽어오기위해 
               //순환하면서 기다립니다.
               line = reader.readLine();

               if (line == null){ 
                   break;
               }
                    
               //불규칙적으로 입력되는 데이터를 입력 받을시 지정 
               Thread.sleep(10);
                    
               System.out.println(line);
            }
        } catch(Exception e) {
            System.err.println(e.toString());
        } finally {
            try {
                socket.close();
                System.out.println("서버와의 접속을 종료합니다.");
            } catch(Exception ignored) {}
        }

        //아무키나 누를 때까지 대기합니다.
        InputStream is = System.in;
        try{
            is.read();
        }catch(Exception e){
            
        }   
        System.out.println("서버 프로그램 실행을 종료합니다.");        
    }
}

```
### 실행

- 서버 실행
   ```text
    C:
    cd C:\서버경로
    start java ThreadServer2
   ```
- 클라이언트 살행 - 추가 CMD 실행
   
  ```text
   start java ThreadClient2 클라ip 1번
   start java ThreadClient2 클라ip 2번
   start java ThreadClient2 클라ip 3번   
   ```





