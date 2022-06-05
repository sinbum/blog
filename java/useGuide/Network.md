# NETWORK

## 네트워크 개념
### Intranet / Internet의 구분
- 라우터를 기준으로 안쪽을 intranet, 외부를 Internet이라고 합니다.
- 라우터는 IP의 대역또한 가지고 있습니다.      

```text
      PC ---- NIC ---- HUB ---- HUB ---- ROUTER ---- INTERNET ---- (WEB, FTP, DB)Server
      LAN  UTP                                │
      │
      Intranet    ←│→ Internet
      │
      사설 IP       │
      172.0.0.1     │ 고정 IP 로만 외부와 연결 가능
      192.168.0.1
      10.0.0.1
      127.0.0.1
```
      
### IP and Port의 이해
- IP는 도시와 같은 위치 정보에 해당합니다.
- Port는 항구를 뜻하는 용어로 실제로 네트워크상으로 접속되는 지점을 말합니다.
- 사용 가능한 포트 : 0 ~ 65535
- 사용할 수 없는 포트
  21 : FTP
  23 : Telnet
  25 : SMTP
  80 : HTTP, IIS등 웹서버
  1433 : MS-SQL 기본 포트
  3306 : MySQL 기본 포트
  1521 : Oracle 기본 포트
  8080 : Apache, 기타 웹 서버
- 1500번 이하는 시스템이 사용하는 포트가 많음으로 1500 이상되는 포트를 사용하기바람

### 네트워크를 지원하는 java.net 패키지의 기본클래스
- URL 클래스
  - URL 클래스는 웹상에 존재하는 자원에 접근하거나 네트웍상의 유일한 주소를
  나타내기 위한 방법을 제공합니다.
  또한 위치정보를 관리하기 위한 클래스 입니다.
  해당 위치에 스트림을 개설할 수 있습니다.(openStream() 이용)
- URL 객체 생성후 스트림 개설
  - URL객체를 생성할때는 MalformedURLException 에러처리를 해야 합니다.

```java
      try{
                URL uri = new URL("http", "hostname", 80, "default.htm");
                InputStream is = uri.openStream();
      }catch(MalformedURLException e){
                e.printStackTrace();
      }
```

- URL의 구조
  - 프로토콜://호스트이름: 포트/호스트상의 경로명/파일 의 형태를 지니고 있습니다.

## 네트워크 연습

### URL 클래스를 이용하는 방법
> URLMain.java
```java

import java.net.;
import java.io.;
public class URLMain{
    public static void main(String args[]) throws MalformedURLException, IOException{
        
        URL url  = new  URL("http://www.daum.net:80/index.html");
        
        System.out.println("Port: " + url.getPort());
        System.out.println("Protocol: " + url.getProtocol());
        System.out.println("HostName: " + url.getHost());
        System.out.println("File: " + url.getFile());
        System.out.println("Ref: " + url.getRef());
        
        String temp;
        BufferedReader br;
        
        br = new BufferedReader(new InputStreamReader(url.openStream()));
        
        while ((temp = br.readLine()) != null) {
            System.out.println(temp);
        }
        
        br.close();
        
    } //end of main
} //end of URLMain class
```

> URLMain.java

```java
import java.net.;
import java.io.;
public class URLMain{
    public static void main(String args[]) throws MalformedURLException, IOException{
    
    URL url  = new  URL("http://www.daum.net:80/index.html");
    
    System.out.println("Port: " + url.getPort());
    System.out.println("Protocol: " + url.getProtocol());
    System.out.println("HostName: " + url.getHost());
    System.out.println("File: " + url.getFile());
    System.out.println("Ref: " + url.getRef());
    String temp;
    
    BufferedReader br;    
    //인터넷에서 사용하는 url을 사용하여 데이터를 가지고 옴
    
    url  = new  URL("https://news.v.daum.net/v/20201005204909700");
    br = new BufferedReader(new InputStreamReader(url.openStream()));
    
    while ((temp = br.readLine()) != null) {    
        System.out.println(temp);    
    }    
        br.close();    
    } //end of main
} //end of URLMain class

```



### URLConnection 클래스
URL을 목표지점으로 하는 네트웍 연결을 위한 작업을 수행합니다.

- URL객체의 스트림 생성과 URLConnection 객체의 스트림 생성
  - URL 객체
  
    ```
             URL uri = new URL("http", "hostname", 80, "default.htm");
             InputStream is = uri.openStream();
    
    ```

  - URLConnection 객체

    ```
             URL uri = URL("http", "hostname", 80, "default.htm");
             URLConnection con = uri.openConnection();
             InputStream is = uri.getInputStream();
    
             또는..
    
             URL uri = URL("http", "hostname", 80, "default.htm");
             URLConnection con = uri.openConnection();
             con.setDoOutput(true); //스트림방향을 출력으로 설정
             OutputStream os  = uri.getOutputStream();
    
    ```


---

### URLConnection을 이용한 입력 스트림 개설

> URLConnectionMain.java

```java

import java.net.;
import java.io.;

public class URLConnectionMain{
    public static void main(String args[])
        throws MalformedURLException, IOException{
        
        URL url  = new  URL("https://www.daum.net");        
        URLConnection con = url.openConnection();
        
        String temp;
        BufferedReader br;
            br = new BufferedReader(new InputStreamReader(con.getInputStream()));
        while ((temp = br.readLine()) != null) {
            System.out.println(temp);
        }
    br.close();
    } //end of main
} //end of URLConnectionMain class

url을 이용하여 문서에 대한 정보를 얻어오는 형태
```
> URLConnection.java

```
import java.io.IOException;
import java.net.MalformedURLException;
import java.net.URL;

public class URLConnection {

    public static void main(String[] args) throws IOException {
        String str = "<https://ssl.pstatic.net/tveta/libs/1306/1306421/c84be064b3aed1368906_20200918171549386.jpg>";
    
        URL url = new URL(str);
    
        java.net.URLConnection conn = url.openConnection();
    
        System.out.println("to String(): " + conn.toString());
        int size = conn.getContentLength();
        System.out.println("문서 사이즈: " + size); // 파일크기를 자꾸 제대로 못읽어옴
        System.out.println("파일 타입" + conn.getContentType());
        System.out.println("접속 날짜 " + conn.getDate()); //접속을 얼마나 오랫동안한지 그 시간 리턴
    }
}
```

---
### url을 이용하여 문서 내용을 가져오기

> URLConnectionMain.java

```java

import java.net.;
import java.io.;

public class URLConnectionMain{
    public static void main(String args[])
    throws MalformedURLException, IOException{
    URL url  = new  URL("https://www.daum.net");
    java.net.URLConnection con = url.openConnection();
    String temp;
    BufferedReader br;
    br = new BufferedReader(new InputStreamReader(con.getInputStream()));
    while ((temp = br.readLine()) != null) {
    System.out.println(temp);
    }
    br.close();
    } //end of main
} //end of Class
```

---

### url이용 파일 다운로드

> URLFileCopy.java

```
import java.io.BufferedInputStream;
import java.io.FileOutputStream;
import java.io.IOException;
import java.net.URL;
import java.net.URLConnection;

public class URLFileCopy {

    public static void main(String[] args) throws IOException { //웹서버에서  사진 데이터를 읽어오자.
    
        String str = "<https://pbs.twimg.com/profile_images/1455185376876826625/s1AjSxph_400x400.jpg>";
        URL url = new URL(str);
        java.io.InputStream in = url.openStream();
        BufferedInputStream bi = new BufferedInputStream(in);
        
        FileOutputStream fo = new FileOutputStream("img.jpg");
    
        byte buff[] = new byte[1024];
        int imgData = 0;
        int cnt = 0;
        
        URLConnection conn = url.openConnection();
        int size = conn.getContentLength();
        
        System.out.println("이미지 크기: " +size);
    
        while( (imgData = bi.read(buff)) != -1 ) {
            fo.write(buff , 0, imgData); // image의 바이트수가 imgData가 들어가 있다.
            fo.flush();
            cnt += imgData;
            System.out.println(((cnt*100)/size)+"%");
        }
        
          in.close(); bi.close(); fo.close();
          
    }
}

```


## 간단 하게 서버접속하기

### 서버 생성

>Server.java - 서버 생성

```
import java.io.IOException;
import java.net.ServerSocket;
import java.net.Socket;
public class Server {
public static void main(String[] args) throws IOException {
    int port = 5050;
    
        //서버 소켓을 생성
        ServerSocket serverSocket= new ServerSocket(port); //서버 자신의 포트를 설정해준다.
    
        System.out.println("접속 대기중~ ");
    
        while(true) {
        Socket sock = serverSocket.accept(); // 새로운 소켓을 생성 클라이언트가 들어왔을때 , 접속했을때  실행되는 구문
        System.out.println("사용자 접속 했습니다");
        System.out.println("Client ip :"+ sock.getInetAddress());
        } //while    
    }
}
```

### 클라이언트 생성

>Client.java - 클라이언트 생성

```
import java.io.IOException;
import java.net.Socket;
import java.net.UnknownHostException;
public class Client {
    public static void main(String[] args) throws Exception {    
        // 연길시에 소켓이 생성된다. 연결이 안될경우에는 예외발생한다.
        Socket socket= new Socket("127.0.0.1" , 5050) ;
        System.out.println("서버와 접속이 되었습니다.");    
    }
}
```


## 소켓을이용한 데이터 전송

### 서버
소켓을 이용해 데이터를 전달받을 서버를 생성.

> server1.java 

```
import java.io.DataOutputStream;
import java.io.IOException;
import java.io.OutputStream;
import java.net.BindException;
import java.net.ServerSocket;
import java.net.Socket;

public class Server1 {
    public static void main(String[] args) throws IOException,BindException {
    int port = 5050;
    OutputStream out;
    DataOutputStream dataOut;
    Socket sock;
    
        ServerSocket serverSocket = new ServerSocket(port);         //서버 소켓을 생성
    
        System.out.println("접속 대기중~ "); // C 소켓에서는 listen상태이나 자바에서는 없음
    
        while(true) {
        sock = serverSocket.accept();  //실제로 송신을 하는것은 바로 저 sock 객체, 서버 소켓은 대기중에 있다가 외부로 부터 접속이 들어오면 accept()활성하여 클라이언트와 연결 통로인 새로운 소켓 생성
        System.out.println("사용자 접속 했습니다");
        System.out.println("Client ip :"+ sock.getInetAddress());
    
        //클라이언트와 연결을 하기위한 스트림을 생성한다.  //recv, send함수를 통해 데이터를 보내고 받지만 java에서는 소켓을 통해 나가는 스트림, 들어오는 스트림을 만들어 통신하게 됨
        out = sock.getOutputStream();
        dataOut = new DataOutputStream(out);
    
        dataOut.writeUTF("math:");
        dataOut.writeInt(10);
        dataOut.flush();
        dataOut.close();
        sock.close();
    
        }  
    }
}
```

### 클라이언트

> Clinet1.java
> 
소켓을 이용해 데이터를 전달할 클라이언트를 생성.

```
import java.io.DataInputStream;
import java.io.InputStream;
import java.net.Socket;
public class Client1 {
    
    public static void main(String[] args) throws Exception {
    
        // 연길시에 소켓이 생성된다. 연결이 안될경우에는 예외발생한다.
        Socket socket = new Socket("127.0.0.1" , 5050) ;
        System.out.println("서버와 접속이 되었습니다.");
    
        InputStream in = socket.getInputStream(); //inputstream 과 연결되었
    
        DataInputStream dataIn = new DataInputStream(in);
    
        String str= dataIn.readUTF();
        int number = dataIn.readInt(); // 정수형형태로 데이터를 읽어오기 위한 메소드
        System.out.println("서버에서 전송된 값 : " + number  );
        System.out.println("서버에서 전송된 문자 : " + str  );
    
        dataIn.close(); in.close(); socket.close();
    
    
    }
}
```

## 정리

### 컴퓨터-socket-stream-network

- ServerSocket 클래스는 외부로 들어오는 접속 정보의 통로 역할을 하는 구멍으로서 정보를 제공하는 역할을 하므로 서버 1개, 클라이언트 여럿을 상대하게 됨
- c에서는 소켓을 만들 때 IP 주소가 필요없지만, java 에서는 IP주소가 클래스 내에 포함되어 있어 서버소켓 생성시 ip주소를 입력하는 형태로 되어 있음, 이주소 함께 포트번호를 내부적으로 바인딩시켜줌
- 서버에는 서버소켓은 들어오는 역할을 하는 통로이고 클라이언트는 다수를 취급하므로 클라이언트와 통신하는 소켓은 별도로 만들어줘야함.
- 클라이언트가 서버에 접속해오면 별도의 소켓을 하나 더 생성하며 이를 일반적인 Socket클래스에서 다루게 됨
---
- 소켓을 통해 스트림이 오고가며 소켓에 스트림을 연결해줘야 합니다.
- 스트림 생성은 socket.getInputStream()을 InputStream 인스턴스를 생성하게 되며 추가적으로 데이터를 읽기 쉽도록 DataInputStream 추가적으로 연결하게 됩니다.(들어오는 데이터)
- 반대로 출력스트림은 socket.getOutputStream()을 이용해 OutputStream 인스턴스를 생성하게 됩니다.(외부로 나가는 데이터)
- 서버에 접속하기 위해서 클라이언트는 인터넷 정보를 수집하게 되는데 이때 이용하는 클래스가 InetAddress이다. 이클래스는 인터넷 주소 정보를 얻어오거나 저장해 두는 역할을 하는 클래스이다.

---

### InetAddress Class
- IP주소와 관련된 여러 정보 제공
  - InetAddress의 객체를 생성하기 위해 스태틱의 getByName()메소들
    이용합니다.

> AddressTest.java

```java
import java.net.*;

class AddressTest{
    public static void main(String args[]) throws UnknownHostException {
    //객체 선언
    InetAddress address=null;
    
    //현재의 나의 인터넷 주소 정보를 얻어오기 위함
    address = InetAddress.getLocalHost();
    // getLocalHost() 메소드는 static으로 선언된 클래스 메소드임
    System.out.println("로컬 컴퓨터의 이름 : "+address.getHostName());
    System.out.println("로컬 컴퓨터의 IP 주소 : "+address.getHostAddress());
    
    //특정 사이트의 IP 정보를 얻어오기 위한 정보인
    address = InetAddress.getByName("naver.com");
    System.out.println("naver.com 도메인 이름과 IP 주소 : "+address);
    
    //특정 사이트의 여러 IP 정보를 얻어오기 위함
    InetAddress SW[] = InetAddress.getAllByName("naver.com");
    
    for (int i=0; i<SW.length; i++){
        System.out.println(SW[i]);
    }
    
    }
}
```

##  Socket, ServerSocket

- ServerSocket: 클라이언트보다 먼저 실행되어 클라이언트의 접속 요청을 기다리며,
  클라이언트가 접속하면 양방향 통신을 할 수 있는 Socket 객체를 생성합니다.
- Socket: 다른 Socket과 데이터를 송수신 합니다.
- Network 프로그램의 운영순서
  1. Server: ServerSocket 생성
  2. Server: 포트감시 시작, Client의 접속을 기다림
  3. Client: Socket 생성시에 인자 값으로 서버의 IP, PORT를 지정, 서버에 접속 요구
  4. Server: Client의 요구를 받아 Socket 객체 생성
  5. Server: 생성된 Socket 객체를 이용해 Client에게 데이터를 보냄
  6. Client: Socket객체로 데이터를 받고 필요한 데이터를 다시 서버로 전송함


### Socket의 처리방식.  
ServerSocket에 의해 Client의 접속요청후 생성된 Socket PORT 나, Clinet쪽 Socket PORT는 무작위로 발생 합니다.  

다음설명은 아래와 같습니다.

```text
                                 2022
    

  ⓐ 서버                   ⓑ             접속요청     ⓒ

- ServerSocket -----> PORT감시 <--------- Socket 클라이언트
  │ ↑
  │생성 │
  ↓ |
  Socket1 ←────────┘
  ⓓ ⓔ 통신

```

### Queue(FIFO:First In First Out, 선입선출)

```text
- Server ---> Socket 1 4307 <--- User1 Socket 3001
  Socket 2 4506 <--- User2 Socket 3002
  Socket 3 4308 <--- User3 Socket 3003

                                    Server Buffer         Client Buffer
                                   -------------        -------------
    

1. Java <---> Socket -┬-- Output Queue ----> Input Queue --┬ Socket <---> Java
   │ │
   └-- Input Queue <---- Output Queue -┘

```


## 기본적인 소켓통신 연습
- 네트웍으로 출력하는 경우
  BufferedWriter writer = new BufferedWriter(new OutputStreamWriter(client.getOutputStream()));
  writer.write("왕눈이 서버에 접속 하신것을 환영 합니다.");
  writer.flush();
- 네트웍에서 읽어오는 경우
  BufferedReader reader = new BufferedReader(new InputStreamReader(socket.getInputStream()));
  String line = reader.readLine();

### 서버측 소켓 생성

> TestServer.java(서버측)

```java
import java.io.;
import java.net.;

public class TestServer {
    public static void main(String[] args) {
    System.out.println("***** 개발자_1 서버 프로그램 작동됨 *****");
    
        ServerSocket server = null;
        try {
            //2022 포트로 ServerSocket 생성
            server = new ServerSocket(2022);
            while(true) {   // 데몬이 되기 위한 무한 루프
                System.out.println("클라이언트 접속을 대기중입니다.");
                Socket client = server.accept(); //Lock
    
                InetAddress ia = client.getInetAddress();
                int port = client.getLocalPort();// 접속에 사용된 PORT
                String ip = ia.getHostAddress(); // 원격 Client IP
    
                System.out.println("클라이언트 접속:" + " Local Port: "+ port + " IP: " + ip);
    
                //한글을 출력할 수 있습니다.
                //Client로 출력할 객체 생성
                BufferedWriter writer = new BufferedWriter(new OutputStreamWriter(client.getOutputStream()));
    
                //버퍼에 문자열을 기록함
                writer.write("개발자_1 서버에 접속 하신것을 환영 합니다.");
    
                //실제로 Client로 전송함
                writer.flush();
    
                try {
                    client.close();  //소켓 닫음
                } catch(IOException e) {
                    System.out.println("Socket을 닫는중 에러 났습니다." + e.toString());
                }
            }
        }catch(IOException ioe) {
            System.err.println("Exception generated...");
        } finally {
            try {
                 server.close();
                 System.out.println("서버 작동을 종료합니다.");
    
            } catch(IOException e) {
                System.out.println("ServerSocket을 닫는중 에러 났습니다." + e.toString());
            }
        }
    
        //아무키나 누를 때까지 대기합니다.
        try{
            InputStream is = System.in;
            is.read();
        }catch(Exception e){
    
        }
        System.out.println("서버 프로그램 실행을 종료합니다.");
    }
}
```
### 클라이언트 측 소켓 생성

> TestClient.java(클라이언트 측)

```
import java.io.;
import java.net.;

public class TestClient {
    public static void main(String[] args) {
    System.out.println("클라이언트 프로그램 작동.....");
    
        Socket socket = null;
        try {
            //args[0]: 접속할 지역의 IP
            //2022: 접속할 Server Port
            socket = new Socket(args[0], 2022);
    
            System.out.println("서버에 연결 되었습니다....");
    
            InetAddress ia = socket.getInetAddress();
            int port = socket.getLocalPort();// 접속에 사용된 PORT
            String ip = ia.getHostAddress(); // 원격 Client IP
    
            System.out.println("접속한 서버 정보:" + " Local Port: "+ port + " IP: " + ip);
    
            //서버로부터 데이터를 입력받아 버퍼에 저장합니다.
            BufferedReader reader = new BufferedReader(new InputStreamReader(socket.getInputStream()));
    
            //버퍼로부터 한 라인씩 읽어 출력합니다.
            //Blocking상태에서 기다립니다.
            String line = reader.readLine();
    
            System.out.println(line);
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
        System.out.println("Client 프로그램 실행을 종료합니다.");
    }
}
```



### 실행하기
- 포트보안 문제시 예외 처리
   - **[시작 -- 설정 -- 제어판 -- Windows 방화벽]**에서 2022 포트를 **[예외]**로 등록합니다.

- 서버 실행
```text
    C:
    cd C:\서버폴더 경로
    java TestServer
```
- Client 실행
```text
    C:
    cd C:\클라이언트 폴더 경로
    java TestClient 127.0.0.1 2022
```

```text
C:
cd C:\클라 경로
java TestClient {고정ip주소} 2022
```

