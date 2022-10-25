# SCENARIO
There are large amounts of data packets that get transmitted over the network every moment.
It is not only important to know how secure these packets are but also to determine how to track these packets to track down important information about an attack. Hence network packet analysis provides a detailed overview of traffic across a network. It allows admins to both focus on a slowdown in packet response times between two managed nodes and better understand network performance. We will be using wireshark to run a packet analysis.

# TOOLS USED
Wireshark

# DATASET
Captured packets on my computer using manual capture through the local network. HTTP packets are available as csv data.

# WORKFLOW
All the network packets are visible on the top frame. Each network packet has details about the time, source, destination, protocol, length of the packet and detailed information regarding the network request. In the middle frame, the details of a selected packet is shown. The details are also available in hexadecimal format as shown in the bottom frame.

<img src="https://user-images.githubusercontent.com/70642284/197698675-943e5a33-adc0-4c04-a998-1c00fdc30ea4.jpg" data-canonical-src="https://gyazo.com/eb5c5741b6a9a16c692170a41a49c858.png" width="800" height="400" />

If we double click on the packet we can see a detailed information of the packet. We can see the Source port, Destination Port, Sequence Number, Network Protocol and other related information regarding the packet.

<img src="https://user-images.githubusercontent.com/70642284/197698663-4290f571-31fa-4aa4-a48c-f28f6d2e1222.jpg" data-canonical-src="https://gyazo.com/eb5c5741b6a9a16c692170a41a49c858.png" width="500" height="400" />  <img src="https://user-images.githubusercontent.com/70642284/197699050-dbca4055-0f66-48d6-85fe-53b9cc996a96.jpg" data-canonical-src="https://gyazo.com/eb5c5741b6a9a16c692170a41a49c858.png" width="300" height="300" />

There is a filter box on top of the window that can filter the network packets. To filter network packets according to a particular source or destination ip, type in :
```
Ip.addr == [ip address]
```

<img src="https://user-images.githubusercontent.com/70642284/197699150-a572664c-85fd-47cd-9a59-1f8c091b8b49.jpg" data-canonical-src="https://gyazo.com/eb5c5741b6a9a16c692170a41a49c858.png" width="400" height="300" />

Now lets analyze a probable phishing attack on a http website.
Head over to : http://zero.webappsecurity.com/ and go to the login page
login with any random username and password (it is just a testing website)
Let's say username = "rahul" and password = "12345"
Make sure to start the capture before signing in. After entering the user credentials let's analyze if our credentials are leaked.

To filter all the network packets that had http protocol, type in:
```
http
```
![60d47dcf-e858-4ccf-ac05-5f07cba2eaf7](https://user-images.githubusercontent.com/70642284/197699360-3a5a4cf5-b420-496e-bdac-15e4a32b4e9e.jpg)

If we double click on the network packet with the POST request, we can further see more information. Alternatively, one can filter the post request using by typing in :
```
http.request.method == “POST”.
```

![71cf71c6-fca7-41db-a96b-06924a9ba814](https://user-images.githubusercontent.com/70642284/197699437-43548b29-1850-4a06-a62d-d72b95bb4ec7.jpg)

Now if we open the packet, we can see a great deal of information. We can see the source and destination port. If we scroll down and look under the HTML Form URL Encoded section, we can see the login username and password!

![93acab91-a477-44cb-a764-8155908f542a](https://user-images.githubusercontent.com/70642284/197699583-0b32320e-b7de-419d-8c99-e3ff2e281930.jpg)

Hence this is a data breach!

