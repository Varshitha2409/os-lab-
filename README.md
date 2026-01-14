CN

CN  

Program 1:  

#include<stdio.h>   
int main() {  
int data[10];  
int dataatrec[10], c, c1, c2, c3, i;  
printf("Enter 4 bits of data one by one\n");  
scanf("%d",&data[0]);  
scanf("%d",&data[1]);  
scanf("%d",&data[2]);  
scanf("%d",&data[4]);  
 // calculate even parity  
data[6]=data[0]^data[2]^data[4];  
data[5]=data[0]^data[1]^data[4];  
data[3]=data[0]^data[1]^data[2];  
 printf("\nEncoded data is\n");  
for(i=0;i<7;i++)  
        printf("%d",data[i]);  
 printf("\n\nEnter received data bits one by one\n");  
 for(i=0;i<7;i++)  
        scanf("%d",&dataatrec[i]);    
c1=dataatrec[6]^dataatrec[4]^dataatrec[2]^dataatrec[0];  
c2=dataatrec[5]^dataatrec[4]^dataatrec[1]^dataatrec[0];  
c3=dataatrec[3]^dataatrec[2]^dataatrec[1]^dataatrec[0];  
c=c3*4+c2*2+c1 ;    
    if(c==0) {  
printf("\nNo error while transmission of data\n");  
    }  
else {  
printf("\nError on position %d",c);       
printf("\nData sent : ");  
        for(i=0;i<7;i++)   
            printf("%d",data[i]);           
printf("\nData received : ");  
        for(i=0;i<7;i++)  
            printf("%d",dataatrec[i]);   
printf("\nCorrect message is\n");  
  //if errorneous bit is 0 we complement it else vice versa  
if(dataatrec[7-c]==0)  
dataatrec[7-c]=1;  
 else  
dataatrec[7-c]=0;  
for (i=0;i<7;i++) {  
printf("%d",dataatrec[i]);  
}  
}  
return 0;  
}  
  
Output:  
 
Case 1 without error 

 Enter 4 bits of data one by one 
1 1 0 1
Encoded data is 
1100110
Enter receive data bits one by one 
1 1 0 0 1 1 0
No error while transmission of data
 
Case 2: with error 

 Enter 4 bits of data one by one 
1 1 0 1
Encoded data is 
1100110
Enter receive data bits one by one 
1 1 0 0 1 0 0
Error on Position :2
Data sent: 1100110
Data received : 1100100
correct message is  
1100110

Program 2:  

#include <iostream> 
#include <unistd.h> 
using namespace std; 
int main() 
{ 
    int frames[] = {1, 2, 3, 4}; 
    int delaysPerFrame[] = {1, 2, 2, 1}; 
    cout << "Sender has to send frames : "; 
    for (int i = 0; i < 4; i++) 
        cout << frames[i] << " "; 
    cout << endl << endl; 
    cout << "Sender\t\t\t\t\tReceiver" << endl; 
    const useconds_t shortDelay = 350000; 
    for (int i = 0; i < 4; i++) { 
        int frame = frames[i]; 
        int delayCount = delaysPerFrame[i]; 
        cout << "Sending Frame : " << frame << "\t\t"; 
        usleep(shortDelay); 
        cout << "Received Frame : " << frame << endl; 
        for (int d = 0; d < delayCount; d++) { 
            usleep(shortDelay); 
            cout << "Delayed Ack" << endl; 
            usleep(shortDelay); 
            cout << "Sending Frame : " << frame << "\t\t"; 
            usleep(shortDelay); 
            cout << "Received Frame : " << frame << " Duplicate" << endl; 
        } 
        usleep(shortDelay); 
        cout << "Acknowledgement : " << frame << endl; 
    } 
    return 0; 
} 
 
Output:
Sender has to send frames : 1 2 3 4

Sender                            Receiver

Sending Frame : 1        Received Frame : 1
Delayed Ack
Sending Frame : 1        Received Frame : 1 Duplicate
Acknowledgement : 1

Sending Frame : 2        Received Frame : 2
Delayed Ack
Sending Frame : 2        Received Frame : 2 Duplicate
Delayed Ack
Sending Frame : 2        Received Frame : 2 Duplicate
Acknowledgement : 2

Sending Frame : 3        Received Frame : 3
Delayed Ack
Sending Frame : 3        Received Frame : 3 Duplicate
Delayed Ack
Sending Frame : 3        Received Frame : 3 Duplicate
Acknowledgement : 3

Sending Frame : 4        Received Frame : 4
Delayed Ack
Sending Frame : 4        Received Frame : 4 Duplicate
Acknowledgement : 4


Program 3:  

#include <iostream> 
#include <cstdlib>
#include <ctime>  
class Station {  
public: 
Station(std::string name) : name(name) {}  
void send() { 
if (carrierBusy()) { 
std::cout << name << " detects carrier busy, deferring transmission." << std::endl; 
return; 
} 
std::cout << name << " is sending a message." << std::endl;  
if (collisionDetected()) { 
std::cout << name << " detects a collision, stopping transmission." << std::endl; 
} else { 
std::cout << name << " successfully transmitted the message." << std::endl; 
} 
} 
bool carrierBusy() { 
return rand() % 2 == 1; 
} 
bool collisionDetected() { 
return rand()% 2 == 1; 
} 
private: 
std::string name; 
}; 
int main() { 
Station stationA("Station A"); 
 Station stationB("Station B"); int i=1; 
while(i<=10){ 
std::cout<<"Scenario"<<i<<std::endl;  
stationA.send(); 
stationB.send(); i++; 
} 
return 0; 
} 
  
Output:  

Scenario1
Station A detects carrier busy, deferring transmission.
Station B is sending a message.
Station B detects a collision, stopping transmission.

etc

Program 4: 

#include<stdio.h>  
#include<iostream>  
using namespace std;                                              
struct node  {
    unsigned dist[6];  
    unsigned from[6];  
}DVR[10];  
int main()  
{  
    cout<<"\n\n-------------------- Distance Vector Routing Algorithm----------- ";  
    int costmat[6][6];  
    int nodes, i, j, k;  
    cout<<"\n\n Enter the number of nodes : ";  
    cin>>nodes; 
    cout<<"\n Enter the cost matrix : \n" ;  
    for(i = 0; i < nodes; i++)  
     {  
        for(j = 0; j < nodes; j++)  
        {  
            cin>>costmat[i][j];  
            costmat[i][i] = 0;  
            DVR[i].dist[j] = costmat[i][j];  
            DVR[i].from[j] = j;  
        }  
    }  
            for(i = 0; i < nodes; i++)   
            for(j = i+1; j < nodes; j++)  
            for(k = 0; k < nodes; k++)  
                if(DVR[i].dist[j] > costmat[i][k] + DVR[k].dist[j])  
                {   //We calculate the minimum distance  
                    DVR[i].dist[j] = DVR[i].dist[k] + DVR[k].dist[j];  
                    DVR[j].dist[i] = DVR[i].dist[j];  
                    DVR[i].from[j] = k;  
                    DVR[j].from[i] = k;  
                }  
        for(i = 0; i < nodes; i++)  
        {  
            cout<<"\n\n For router: "<<i+1;  
            for(j = 0; j < nodes; j++)  
                cout<<"\t\n node "<<j+1<<" via "<<DVR[i].from[j]+1<<" Distance 
"<<DVR[i].dist[j];  
        }  
    cout<<" \n\n ";  
    return 0;  
}  

Output:
---------------- Distance Vector Routing Algorithm ----------------

Enter the number of nodes : 4

Enter the cost matrix :
0 2 999 1
2 0 3 7
999 3 0 11
1 7 11 0


For router : 1
node 1 via 1 Distance 0
node 2 via 2 Distance 2
node 3 via 2 Distance 5
node 4 via 4 Distance 1


For router : 2
node 1 via 1 Distance 2
node 2 via 2 Distance 0
node 3 via 3 Distance 3
node 4 via 1 Distance 3


For router : 3
node 1 via 2 Distance 5
node 2 via 2 Distance 3
node 3 via 3 Distance 0
node 4 via 2 Distance 6


For router : 4
node 1 via 1 Distance 1
node 2 via 1 Distance 3
node 3 via 2 Distance 6
node 4 via 4 Distance 0

Program 5: 

#include <iostream> 
#include <vector> 
#include <climits> 
using namespace std; 
const int INF = INT_MAX; 
class Network { 
public: 
    int numNodes; 
    vector<vector<int>> costMatrix; 
    Network(int nodes) : numNodes(nodes) { 
        costMatrix.resize(nodes, vector<int>(nodes, INF)); 
    } 
    void addLink(int node1, int node2, int cost) { 
        costMatrix[node1][node2] = cost; 
        costMatrix[node2][node1] = cost; 
    } 
    void printLeastCostTree(int source, const vector<int>& parent) { 
        cout << "Least Cost Tree:" << endl; 
        for (int i = 0; i < numNodes; ++i) { 
            if (i != source) { 
                cout << "Node " << i << " -> Node " << parent[i] 
                     << " (Cost: " << costMatrix[i][parent[i]] << ")" 
                     << endl; 
            } 
        } 
    } 
    void linkStateRouting(int source) { 
        vector<int> distance(numNodes, INF); 
        vector<bool> inTree(numNodes, false); 
        vector<int> parent(numNodes, -1); 
        distance[source] = 0; 
        for (int i = 0; i < numNodes - 1; ++i) { 
            int u = getMinDistanceVertex(distance, inTree); 
            inTree[u] = true; 
            for (int v = 0; v < numNodes; ++v) { 
                if (!inTree[v] && 
                    costMatrix[u][v] != INF && 
                    distance[u] + costMatrix[u][v] < distance[v]) { 
                    parent[v] = u; 
                    distance[v] = distance[u] + costMatrix[u][v]; 
                } 
            } 
        } 
        printLeastCostTree(source, parent); 
    } 

    int getMinDistanceVertex(const vector<int>& distance, 
                             const vector<bool>& inTree) { 
        int minDistance = INF; 
        int minVertex = -1; 
        for (int v = 0; v < numNodes; ++v) { 
            if (!inTree[v] && distance[v] < minDistance) { 
                minDistance = distance[v]; 
                minVertex = v; 
            } 
        } 
        return minVertex; 
    } 
}; 
 
int main() { 
    int numNodes = 4; 
    Network network(numNodes); 
    network.addLink(0, 1, 4); 
    network.addLink(0, 2, 2); 
    network.addLink(1, 2, 5); 
    network.addLink(1, 3, 10); 
    network.addLink(2, 3, 1); 
    int sourceNode = 0; 
    network.linkStateRouting(sourceNode); 
    return 0; 
} 
Output:
Least Cost Tree :
Node 1-> Node 0 (Cost :4)
Node 2-> Node 0 (Cost :2)
Node 3-> Node 2 (Cost :1)

Program 6:  

// TCP server side  
#include<stdio.h>  
#include<netinet/in.h>  
#include<netdb.h>  
#include<arpa/inet.h>  
#include<unistd.h>     
#define SERV_TCP_PORT 5035  
int main(int argc,char**argv)  
{   
       int sockfd,newsockfd;  
       socklen_t clength;  
       struct sockaddr_in serv_addr,cli_addr;  
       char buffer[4096];   
       sockfd=socket(AF_INET,SOCK_STREAM,0);     
       serv_addr.sin_family=AF_INET;  
       serv_addr.sin_addr.s_addr=INADDR_ANY;  
       serv_addr.sin_port=htons(SERV_TCP_PORT);   
       printf("\nStart");  
       bind(sockfd,(struct sockaddr*)&serv_addr,sizeof(serv_addr));  
       printf("\nListening...");  
       printf("\n");  
       listen(sockfd,5);    
       clength=sizeof(cli_addr);  
       newsockfd=accept(sockfd,(struct sockaddr*)&cli_addr,&clength);  
       printf("\nConnection Accepted");  
       printf("\n");  
       read(newsockfd,buffer,4096);  
       printf("\nClient message:%s",buffer);  
       write(newsockfd,buffer,4096);  
       printf("\n");   
       close(sockfd);  
       close(newsockfd);  
       return 0;  
} 
 
//TCP client side  
#include<stdio.h>  
#include<sys/types.h>  
#include<sys/socket.h>  
#include<netinet/in.h>  
#include<netdb.h>  
#include<unistd.h>  
#include<arpa/inet.h>  
#define SERV_TCP_PORT 5035  
int main(int argc,char*argv[])  
{  
       int sockfd;  
       struct sockaddr_in serv_addr;  
       struct hostent *server;  
       char buffer[4096];   
       sockfd=socket(AF_INET,SOCK_STREAM,0);  
       serv_addr.sin_family=AF_INET;  
       serv_addr.sin_addr.s_addr=inet_addr("127.0.0.1");  
       serv_addr.sin_port=htons(SERV_TCP_PORT);  
       printf("\nReady for sending...");  
       connect(sockfd,(struct sockaddr*)&serv_addr,sizeof(serv_addr));  
       printf("\nEnter the message to send\n");  
       printf("\nClient: ");  
       fgets(buffer,4096,stdin);   
       write(sockfd,buffer,4096);  
       printf("Serverecho:%s",buffer);  
       printf("\n");  
       close(sockfd);  
       return 0;  
} 
 
Output:

At Server Terminal  :

Start
Listening...

Accepted

Client message: hello

At Client Terminal:

Ready for sending...
Enter the message to send

Client: hello
Server echo: hello



 Compressed prg

prg 3:

#include <iostream> 
#include <cstdlib> 
#include <ctime> 
using namespace std; 
 
int main() { 
    srand(time(0)); 
    for (int i = 1; i <= 5; i++) { 
        cout << "\nScenario" << i << endl; 
        int a = rand() % 3; 
        int b = rand() % 3; 
 
        if (a == 0) cout << "Station A detects carrier busy, deferring transmission." << endl; 
        else cout << "Station A is sending a message." << endl; 
 
        if (b == 0) cout << "Station B detects carrier busy, deferring transmission." << endl; 
        else if (b == 1) cout << "Station B detects a collision, stopping transmission." << endl; 
        else cout << "Station B successfully transmitted the message." << endl; 
    } 
    return 0; 
} 

prg 4:


#include <iostream> 
using namespace std; 
 
struct node { 
    int dist[10]; 
    int from[10]; 
} DVR[10]; 
 
int main() { 
    int cost[10][10], nodes; 
    cout << "---------------- Distance Vector Routing Algorithm----------------\n\n"; 
    cout << "Enter the number of nodes : "; 
    cin >> nodes; 
    cout << "\nEnter the cost matrix :\n"; 
    for (int i = 0; i < nodes; i++) { 
        for (int j = 0; j < nodes; j++) { 
            cin >> cost[i][j]; 
            DVR[i].dist[j] = cost[i][j]; 
            DVR[i].from[j] = j; 
        } 
    } 
    for (int i = 0; i < nodes; i++) { 
        for (int j = 0; j < nodes; j++) { 
            for (int k = 0; k < nodes; k++) { 
                if (DVR[i].dist[j] > cost[i][k] + DVR[k].dist[j]) { 
                    DVR[i].dist[j] = cost[i][k] + DVR[k].dist[j]; 
                    DVR[i].from[j] = k; 
                } 
            } 
        } 
    } 
    for (int i = 0; i < nodes; i++) { 
        cout << "\nFor router: " << i + 1 << endl; 
        for (int j = 0; j < nodes; j++) { 
            cout << "node " << j + 1 << " via " << DVR[i].from[j] + 1 << " Distance " << DVR[i].dist[j] << 
endl; 
        } 
    } 
    return 0; 
}

prg 5:

#include <iostream> 
#include <climits> 
using namespace std; 
#define N 4 
#define INF 999 
 
int main() { 
    int cost[N][N] = { {0, 4, 2, INF}, {4, 0, 5, 10}, {2, 5, 0, 1}, {INF, 10, 1, 0} }; 
    int dist[N], parent[N]; 
    bool visited[N]; 
 
    for (int i = 0; i < N; i++) { dist[i] = INF; visited[i] = false; parent[i] = -1; } 
    dist[0] = 0; 
 
    for (int i = 0; i < N - 1; i++) { 
        int u = -1, min = INF; 
        for (int j = 0; j < N; j++) if (!visited[j] && dist[j] < min) { min = dist[j]; u = j; } 
        visited[u] = true; 
        for (int v = 0; v < N; v++) { 
            if (!visited[v] && cost[u][v] != INF && dist[u] + cost[u][v] < dist[v]) { 
                dist[v] = dist[u] + cost[u][v]; 
                parent[v] = u; 
            } 
        } 
    } 
    cout << "Least Cost Tree:" << endl; 
    for (int i = 1; i < N; i++) cout << "Node " << i << " -> Node " << parent[i] << " (Cost: " << 
cost[i][parent[i]] << ")" << endl; 
    return 0; 
} 

prg 6.

// server.c
#include <stdio.h>
#include <unistd.h>
#include <arpa/inet.h>

int main() {
    int s, ns;
    char buf[4096];
    struct sockaddr_in a = {AF_INET, htons(5035), INADDR_ANY};

    printf("\nStart");
    s = socket(AF_INET, SOCK_STREAM, 0);
    bind(s, (struct sockaddr*)&a, sizeof(a));

    printf("\nListening...\n");
    listen(s, 5);

    ns = accept(s, NULL, NULL);
    printf("\nConnection Accepted\n");

    read(ns, buf, sizeof(buf));
    printf("\nClient message:%s", buf);

    write(ns, buf, sizeof(buf));
    printf("\n");

    close(ns);
    close(s);
}


// client.c
#include <stdio.h>
#include <unistd.h>
#include <arpa/inet.h>

int main() {
    int s;
    char buf[4096];
    struct sockaddr_in a = {AF_INET, htons(5035), inet_addr("127.0.0.1")};

    printf("\nReady for sending...");
    s = socket(AF_INET, SOCK_STREAM, 0);
    connect(s, (struct sockaddr*)&a, sizeof(a));

    printf("\nEnter the message to send\n\nClient: ");
    fgets(buf, sizeof(buf), stdin);

    write(s, buf, sizeof(buf));
    printf("Serverecho:%s\n", buf);

    close(s);
}



CN 

Simulation 1:

Step 1: Click on PC0 → Desktop → IP Config →  
IPV4 Address: 10.1.1.1 
Subnet Mask: 255.0.0.0 
 
Step 2: Click on PC1 → Desktop → IP Config →  
IPV4 Address: 10.1.1.2 
Subnet Mask: 255.0.0.0 
 
Step 3: Click on PC2 → Desktop → IP Config → 
IPV4 Address: 192.168.1.1 
Subnet Mask: 255.255.255.0 
 
Step 4: Click on PC3 → Desktop → IP Config → 
IPV4 Address: 192.168.1.2 
Subnet Mask: 255.255.255.0 
Config done with PC 
 
Step 5: Click on Router → Config → Interface → Fast Ethernet 0/0 
IP Address: 10.1.1.3 
Subnet Mask: 255.0.0.0 
Enable Port Status 
 
Click on → Fast Ethernet 0/1 
IP address: 192.168.1.3  
Subnet Mask: 255.255.0.4 
Enable Port Status 
 
Step 6: Click on PC0 → IP Configuration → Default Gateway → 10.1.1.3 
Click on PC1 → IP Configuration → Default Gateway →10.1.1.3 
Click on PC2 → IP Configuration → Default Gateway → 192.168.1.3 
Click on PC3 → IP Configuration → Default Gateway → 192.168.1.3 
 
Simulation: Select packets and place on PC0 and PC2 
Auto capture 
Successful

Simulation 2:

Step 1: Click on PC0 → Desktop → IP Config → 
IP Address: 192.168.1.1 
Subnet Mask: 255.255.255.0 
 
Step 2: Click on PC1 → Desktop → IP Config →  
IP Address: 192.168.1.2 
Subnet Mask: 255.255.255.0 
 
Step 3: Click on PC2 → Desktop → IP Config →  
IP Address: 192.168.1.3 
Subnet Mask: 255.255.255.0 
 
Step 4: Click on Server → Desktop → IP Config → 
IP Address: 192.168.1.4 
Subnet Mask: 255.255.255.0 
 
Step 5: Click on inspect button (      ) 
Click on PC → Right click → Select ARP → ARP table for PC0 
 
Simulation: Select packets and place on PC0 and PC2  
Auto capture 
Successful 


Simulation 3:

Step 1: Select a Server, a Switch, 2 PC’s and 2 Laptops 
 
Step 2: Give the connections  
 
Step 3: Click on Server → In Config select DHCP 
Pool Name: Server pool (by default) 
Default Gateway : 10.0.0.1 
DNS Server: 0.0.0.0 
Start IP address:  10     0    0    0 
Subnet Mask    : 255    0    0    0 
Maximum number of users : 50 
Save 
 
Step 4: Click on Server → Config → Fast Ethernet → Select IP Config as static and enter the 
IP Address and Subnet Mask manually (10.0.0.1) → On port status 
 
Step 5: Select PC0 →Desktop →IP Config →DHCP  
Requesting IP Address → DHCP Request  
Successful 
Do the same for Laptop0, PC1 and Laptop1 
[IP address and subnet Mask of all changes automatically] 
Simulation: Go to simulation mode 
Select a packet and place on PC0 and Laptop1   
Auto capture 
Successful 
 
Simulation 4:

Step 1: Select 2 Routers, 2 switches and 4 PC’s 
 
Step 2: Give the connections 
For Router 0 to Router 1, select the 4th connectivity [---] 
While placing the connection, select the fast ethernet 0/1 
 
Step 3: Click on PC0 → Desktop → IP Config → Static → 
IP address: 192.168.1.2 
Subnet Mask: 255.255.255.0 
Default Gateway: 192.168.1.4 
 
Click on PC1 → Desktop → IP Config → Static → 
IP address: 192.168.1.3 
Subnet Mask: 255.255.255.0 
Default Gateway: 192.168.1.4 
 
Click on PC2 → Desktop → IP Config → Static → 
IP address: 192.168.2.2 
Subnet Mask: 255.255.255.0 
Default Gateway: 192.168.2.4 
 
Click on PC3 → Desktop → IP Config → Static → 
IP address: 192.168.2.3 
Subnet Mask: 255.255.255.0 
Default Gateway: 192.168.2.4 
 
Step 4: Click on Router0 → Config → Fast Ethernet 0/0 → 
IP address: 192.168.1.4 
Subnet Mask: 255.255.255.0 
Turn on the port status  
 
Step 5: Click on Router0 → Config → Fast Ethernet 0/1 → 
IP address: 192.168.3.2 
Subnet Mask: 255.255.255.0 
Turn on the port status  
 
Step 6: Click on Router0 → Config → Fast Ethernet 0/0 → 
IP address: 192.168.2.4 
Subnet Mask: 255.255.255.0 
Turn on the port status  
 
Step 7: Click on Router1 → Config → Fast Ethernet 0/0 →  
IP address: 192.168.3.3 
Subnet Mask: 255.255.255.0 
Turn on the port status  
 
Step 8: Click on Router1 → Config → Static 
Network: 192.168.1.0 
Mask: 255.255.255.0 
Next HOP: 192.168.3.2. 
Click on add 
Simulation: Go to simulation mode 
Select the packets and place them on PC0 and PC1 
Auto capture 
Successful

Simulation 5:


Step 1: Select 3 Routers (2811) 
 
Step 2: Click on Router0 → Config → Physical →Select WIC1T or WIC2T 
Disable the green button (Right side) 
Drag and drop the WIC 2T 2 times into the box 
Enable the green button 
Repeat the same steps for the other Routers 
 
Step 3: Select 3 PC’s and give the connections to Routers and PC’s 
 
Step 4: Click on PC0 → Desktop → IP Config → Static   
IP address: 192.168.1.1 
Subnet Mask: 255.255.255.0 
Default Gateway: 192.168.1.2 
 
Step 5: Click on PC1 → Desktop → IP Config → Static   
IP address: 192.168.2.1 
Subnet Mask: 255.255.255.0 
Default Gateway: 192.168.2.2 
 
Step 6: Click on PC2 → Desktop → IP Config → Static   
IP address: 192.168.3.1 
Subnet Mask: 255.255.255.0 
Default Gateway: 192.168.3.2 
 
Step 7: [ Based on the respective fast ethernet and serial numbers in your system, provide the 
IP’s ] 
Click on Router 0 → Config → Interface   
Fast Ethernet 0/0: 
IP Address: 192.168.1.2 
Subnet Mask: 255.255.255.0 
Turn on Port status 
Serial 0/3/1: 
IP Address: 10.10.10.2 
Subnet Mask: 255.0.0.0 
Turn on Port status 
Serial 0/3/0: 
IP Address: 20.20.20.1 
Subnet Mask: 255.0.0.0 
Turn on Port status  
Repeat the same process for Router1 and Router2  (For IP’s, look at the diagram) 
Make sure all the red dots on the connection turns green 
 
Step 6: Click on the Router0 → Config → RIP 
Network: 192.168.1.2 → Add  
                10.10.10.2 → Add 
                20.20.20.1 →  Add 
(Add the respective IP’s of the Router) 
Repeat the same steps for Router1 and Router2 
  
Simulation: Go to simulation mode 
Edit Event list filters → Select only ICMP 
Select the packets and place on PC’s 
Auto capture 
Successful


Simulation 6:

Step 1: Select 3 Routers (2811) 
 
Step 2: Click on Router0 → Config → Physical → Select WIC1T or WIC2T 
Disable the green button (Right side) 
Drag and drop the WIC 2T 2 times into the box 
Enable the green button 
Repeat the same steps for the other Routers 
 
Step 3: Select 3 PC’s and give the connections to Routers and PC’s 
 
Step 4: Click on PC0 → Desktop → IP Config → Static   
IP address: 192.168.1.1 
Subnet Mask: 255.255.255.0 
Default Gateway: 192.168.1.2 
 
Step 5: Click on PC1 → Desktop → IP Config → Static   
IP address: 192.168.2.1 
Subnet Mask: 255.255.255.0 
Default Gateway: 192.168.2.2 
 
Step 6: Click on PC2 → Desktop → IP Config → Static   
IP address: 192.168.3.1 
Subnet Mask: 255.255.255.0 
Default Gateway: 192.168.3.2 
 
Step 7: [ Based on the respective fast ethernet and serial numbers in your system, provide the 
IP’s ] 
Click on Router 0 → Config → Interface   
Fast Ethernet 0/0: 
IP Address: 192.168.1.2 
Subnet Mask: 255.255.255.0 
Turn on Port status 
Serial 0/3/1: 
IP Address: 10.10.10.2 
Subnet Mask: 255.0.0.0 
Turn on Port status 
Serial 0/3/0: 
IP Address: 20.20.20.1 
Subnet Mask: 255.0.0.0 
Turn on Port status  
Repeat the same process for Router1 and Router2  (For IP’s, look at the diagram) 
Make sure all the red dots on the connection turns green 
 
Step 6: Click on Router 0 → CL I 
Router > enable 
Router# configure terminal 
Router(config)#router ospf 3 
Router(config-router)#network 192.168.1.0 0.0.0.255 area 0 
Router(config-router)#network 10.0.0.0 0.255.255.255 area 0 
Router(config-router)#network 20.0.0.0 0.255.255.255 area 0 
Router(config-router)#exit 
Router(config)#exit 
 
Click on Router1 → CLI 
Router > enable 
Router# configure terminal 
Router(config)#router ospf 3 
Router(config-router)#network 192.168.2.0 0.0.0.255 area 0 
Router(config-router)#network 20.0.0.0 0.255.255.255 area 0 
Router(config-router)#network 30.0.0.0 0.255.255.255 area 0 
Router(config-router)#exit 
Router(config)#exit 
 
Click on Router2 → CLI 
Router > enable 
Router# configure terminal 
Router(config)#router ospf 3 
Router(config-router)#network 192.168.3.0 0.0.0.255 area 0 
Router(config-router)#network 10.0.0.0 0.255.255.255 area 0 
Router(config-router)#network 30.0.0.0 0.255.255.255 area 0 
Router(config-router)#exit 
Router(config)#exit 
 
Simulation: Go to simulation mode 
Event List → Edit Filters → Select only ICMP 
Select the packets and place on PC’s 
Auto Capture 
Successful

Simulation 7:

Step 1: Select 2 PC’s, 2 Servers and a Switch 
 
Step 2: Give the connections 
 
Step 3: Click on PC0 → Desktop → IP Config 
IP Address: 192.168.1.1 
Subnet Mask: 255.255.255.0 
Default Gateway: 192.1681.3 
 
Step 4: Click on PC1 → Desktop → IP Config 
IP Address: 192.168.1.2 
Subnet Mask: 255.255.255.0 
Default Gateway: 192.1681.3 
 
Step 5: Click on Server0 (WEB Server) → Desktop 
IP Address: 192.168.1.4 
Subnet Mask: 255.255.255.0 
 
Click on Server1 (DNS Server) → Desktop 
IP Address: 192.168.1.3 
Subnet Mask: 255.255.255.0 
 
Step 6: Click on WEB Server → Config → HTTP 
Modify the HTML code 
 
Step 7: Click on DNS Server → Config → DNS 
Turn on DNS Service 
Name: www.abc.com 
IP Address: 192.168.1.4 (IP Address of WEB Server) 
Add 
 
Step 8: Click on PC0 → Desktop → Web Browser → URL → www.abc.com → Go 
