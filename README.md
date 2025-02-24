11. Program for Remote Command Execution using sockets.
SERVER:
import java.io.*;
import java.net.*;

class RemoteServer
{
	public static void main(String args[])
	{
		try
		{
			int port;
			BufferedReader buf = new BufferedReader(new InputStreamReader(System.in));
			
			System.out.println("Enter the Port Address : ");
			port = Integer.parseInt(buf.readLine());
			ServerSocket ss = new ServerSocket(port);
			System.out.println("Waiting ....");
			Socket s = ss.accept();
			
			if(s.isConnected() == true)
			{
				System.out.println("Client Socket is Connected Successfully. ");
			}
			
			InputStream in = s.getInputStream();
			OutputStream ou = s.getOutputStream();
			
			//BufferedReader buf = new BufferedReader(new InputStreamReader(System.in));
			String cmd = buf.readLine();
			PrintWriter pr = new PrintWriter(ou);
			pr.println(cmd);
			
			Runtime H = Runtime.getRuntime();
			//Process p = H.excel(cmd);
			System.out.println("The "+cmd+"Command is executed successfully");
			pr.flush();
			pr.close();
			ou.close();
			in.close();
		}
		
		catch(Exception e)
		{
			System.out.println("Error : "+e.getMessage());
		}
	}
}



CLIENT:
import java.io.*;
import java.net.*;

class RemoteClient
{
	public static void main(String args[])
	{
		try
		{
			int port;
			BufferedReader buf = new BufferedReader(new InputStreamReader(System.in));
			System.out.println("Enter the port Address : ");
			port = Integer.parseInt(buf.readLine());
			Socket s = new Socket("localhost",port);
			
			if(s.isConnected() == true)
			{
				System.out.println("Server Socket is connected Successfully. ");
			}
			
			InputStream in = s.getInputStream();
			OutputStream ou = s.getOutputStream();
			
			//BufferedReader buf = new BufferedReader(new InputStreamReader(System.in));
			//BufferedReader buf = new BufferedReader(new InputStreamReader(in));
			
			PrintWriter pr = new PrintWriter(ou);
			System.out.println("Enter the command to be Executed : ");
			pr.println(buf.readLine());
			pr.flush();
			
			String str = buf.readLine();
			System.out.println(" "+str+" Command is Executed Successfully. ");
			pr.close();
			ou.close();
			in.close();
		}
		
		catch(Exception e)
		{
			System.out.println("Error : "+e.getMessage());
		}
	}
}
OUTPUTS:





7. Program for connection-oriented Iterative service in which server reverses the string send by client and sends it back.
SERVER:
import java.io.*;
import java.net.*;
class OrderReverseTCPServer  {
  public static void main(String args[]) throws Exception
{
String clientSentence;
String capitalizedSentence=null;
ServerSocket welcomeSocket=new ServerSocket(6333);
while(true){
Socket connectionSocket=welcomeSocket.accept();
BufferedReader inFromClient=new  BufferedReader(new InputStreamReader(connectionSocket.getInputStream()));
DataOutputStream outToClient=new DataOutputStream(connectionSocket.getOutputStream());
clientSentence=inFromClient.readLine();
String sendToClient=new StringBuilder(clientSentence).reverse().toString()+'\n';
outToClient.writeBytes(sendToClient);
}
}
}

CLIENT:
import java.io.*;
import java.net.*;
class OrderReverseTCPClient   {
  public static void main(String args[]) throws Exception
{
String sentence;
String modifiedSentence;
BufferedReader inFromUser=new  BufferedReader(new InputStreamReader(System.in));
Socket clientSocket;
clientSocket=new Socket("localhost",6333);
DataOutputStream outToServer=new DataOutputStream(clientSocket.getOutputStream());
BufferedReader inFromServer=new BufferedReader(new InputStreamReader(clientSocket.getInputStream()));
sentence=inFromUser.readLine();
outToServer.writeBytes(sentence + '\n');
modifiedSentence=inFromServer.readLine();
System.out.println("FROM SERVER:" +modifiedSentence);
clientSocket.close();
}
}
OUTPUTS:
