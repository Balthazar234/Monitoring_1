<h1>DevOps Monitoring_1</h1>

<h2>Project Description</h2>
We will cover this project in two parts.

The first part will contain the setup of Grafana in the local environment.

In the second part, we will see how we can monitor EC2, Containers, AWS cloud billing, etc.

Let’s begin with the Garfana installation and setup.

<br />
<p align="center">

1. Goto the AWS console, and create an EC2 instance named “grafana”.
 
<img src="https://i.imgur.com/FTCFR5a.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<br />
<br />

2. Now, allow the inbound port 3000 from the “Security Group”.

3. Now, take the ssh console and login into the machine.

4. Download the GPG keys and add them to the trusted keys list.
   
  <pre><code># Download the Grafana GPG key and save it to a file
wget -q -O - https://packages.grafana.com/gpg.key | sudo tee /etc/apt/trusted.gpg.d/grafana.gpg >/dev/null

# Add the Grafana APT repository to the system's source list
echo "deb https://packages.grafana.com/oss/deb stable main" | sudo tee /etc/apt/sources.list.d/grafana.list

# Update the package lists
sudo apt update
</code></pre>

5. Now, add it to the Grafana repository.
<pre><code>sudo add-apt-repository "deb https://packages.grafana.com/oss/deb stable main"
</code></pre> 

6. Once it has been added, we need to update the system.
   
  <pre><code> sudo apt update </code></pre>
   <br/>
<img src="https://i.imgur.com/u5rHsbT.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

7. Now, we need to install the Grafana.

<pre><code> sudo apt install grafana </code></pre>

<img src="https://i.imgur.com/5YokW3N.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

8. After installation, add Grafana to auto-start and start the Grafana daemon itself.

<pre><code>sudo systemctl enable grafana-server
sudo systemctl status grafana-server
</code></pre>

9. The installation of the Grafana repo is finished and ready to use.

10. Now, check the status. As

<pre><code>sudo systemctl status grafana-server</code></pre>
<br/>

<img src="https://i.imgur.com/1V0Y2fJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

11. Now, goto the browser and search with,

- “<IP_of_EC2:3000>”

Eureka!
 <br/>
 
<img src="https://i.imgur.com/f4jm66y.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<br />
<br />

12. Use,

Username: admin

Password: admin

13. You will be entered in the Garfana dashboard.

 <br/>
<img src="https://i.imgur.com/cnZ55nI.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

<h1>DevOps Monitoring_2(Grafana)</h1>

<br />

Goto Google and search for “Grafana.com” Click on Create a free account.

 <br/>
<img src="https://i.imgur.com/qhY4H5d.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<br />
<br />

You can create your account with your ease. I am creating using Google.

Now select Team URL and the Deployment Region, and click on “Finish Setup”
 
 <br/>

<img src="https://i.imgur.com/7Bu5has.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

Here, Grafana is creating an instance for us in the background.
<br/>

<img src="https://i.imgur.com/QGiFH4K.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

As of now, we will just be “Creating a Dashboard”.

Here, from a lot of options, we will select “Linux Dashboard”.

<br/>

<img src="https://i.imgur.com/VrZUZEe.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

It will give you a template, to create a dashboard for Linux.

In Choose your OS: Debian — based

Architecture: Amd64

Hostname: <Public IP of EC2>

Click on “Install Integration”

(Here is a YAML file below, that Grafana will run in the background to generate logs for any particular instance).

 <br/>

<img src="https://i.imgur.com/ddR9f5Q.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

After doing “Install Integration” it will create a custom installation for you. It will create an API key, by using this key our Grafana cloud and EC2 instance will connect.

 <br/>

<img src="https://i.imgur.com/Z4ECag6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

Copy the above key and SSH to the server that we created earlier, and paste that Key. It will start to install it.

 <br/>

<img src="https://i.imgur.com/04pff0v.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

Now, run the command to restart the Grafana agent.

<pre><code>sudo systemctl restart Grafana-agent.service</code></pre>
 <br/>

<img src="https://i.imgur.com/CxWlJNZ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

Now, go back to Grafana Dashboard and click on “Test Integration”

<br/>

<img src="https://i.imgur.com/PyzhpAY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

Now, click on “View Dashboard”

 <br/>

<img src="https://i.imgur.com/slVQvT1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

Now, Go to “Node Exporter / Nodes”, and you will get all your Server monitoring on Grafana.

 <br/>

<img src="https://i.imgur.com/GyTG1yT.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

To make the graphs up, just run some docker containers on the newly built server and it will start showing the data.

<br/>

<img src="https://i.imgur.com/XQZwBKH.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

As it started heating up,

<br/>

<img src="https://i.imgur.com/m0p3mb6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

Now, Go to Home & click on “+ Connect Data”.

<br/>

<img src="https://i.imgur.com/uitHzlp.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

It will list down, all the things that you can integrate with Grafana.

<br/>

<img src="https://i.imgur.com/09iiL28.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

Now let’s click on “CloudWatch”.

<br/>

<img src="https://i.imgur.com/hvdlJqB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

Goto “Create a Cloud Watch Datastore”.

<br/>

<img src="https://i.imgur.com/oRthvax.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

Here, we need to give the Username and Password, of a User with Programmatic Access from IAM.

<br/>

<img src="https://i.imgur.com/7rddxQu.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

Select Region “us-east-1” as cloudwatch by default uses this region.

Now click on “Save and Test”.

Now, create any type of alarm in “CloudWatch”.

Suppose we have created a billing alarm for a limit of $10.

<br/>

<img src="https://i.imgur.com/UYJV0ZJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

Now, go back to Grafana and refresh.

<br/>

<img src="https://i.imgur.com/cBFaeGQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

In the same way, we can create dashboards for Docker, Kubernetes, and a lot of other services.

<br/>
</p>
- <b>~Hassanat Hussain</b>
<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
