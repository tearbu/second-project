# Setup Multiple Static Websites on a Single Server Using Nginx Virtual Hosts

In this project, you will learn the concept of subdomains and hosting multiple websites on a single server using Nginx Virtual Host configuration.

|S/N | Project Tasks                                                                            |
|----|------------------------------------------------------------------------------------------|
| 1  |Install and configure Nignx on a server                                                   |
| 2  |Create two website directories with two different website templates.                      |
| 3  |Create two subdomains                                                                     |
| 4  |Add the IP of the server as A record to the two subdomains.                               |
| 5  |Configure the Virtual host to point two subdomains to two different website directories.  |
| 6  |Validate the setup by accessing the subdomains.                                              |
| 7  |Create a certbot SSL certificate for the root Domain.                        |
| 8  |Configure certbot on Nginx for two websites.                                         |
| 9  |Validate the subdomain websites’ SSL using OpenSSL utility.                               |

## Key Concepts Covered

- **AWS (EC2 and Route 53)**
- **EC2**
- **Linux(Ubuntu)**
- **Nginx**
- **DNS**
- **Subdomains**
- **SSL (certbot)**
- **OpenSSL command**

## Checklist

- [x] Task 1: Spin up a Ubuntu server & assign an elastic IP to it.
- [x] Task 2: SSH into the server and install and configure Nignx on a server.
- [x] Task 3: Create two website directories with two different website templates.
- [x] Task 4: Create two subdomains
- [x] Task 5: Add the IP of the server as A record to the two subdomains.
- [x] Task 6: Configure the Virtual host to point two subdomains to two different website directories.
- [x] Task 7: Validate the setup by accessing the subdomains.  
- [x] Task 8: Create a certbot SSL certificate for the root Domain.
- [x] Task 9: Configure certbot on Nginx for the two websites.
- [x] Task 10: Validate the subdomain websites’ SSL using OpenSSL utility.

## Documentation
### Task 1: Spin up a Ubuntu server & assign an elastic IP to it.
To spin up a Ubuntu server, follow these steps:
1. Log in to your AWS account.
2. Click on the "EC2" service.
![images](images/1.png)

3. Click on "Launch Instance".

![images](images/2.png)

4. Choose the Ubuntu Server 20.04 LTS (HVM) image.

![images](images/3.png)

5. Choose the instance type (e.g., t2.micro).

![images](images/4.png)

6. Configure the instance details (e.g., VPC, Subnet, Security Group).

![images](images/5.png)

7. Add storage (e.g., 30 GB root volume).

![images](images/6.png)

8. Add tags (e.g., Name: my-ubuntu-server).

![images](images/7.png)

9. Click "Launch" to launch the instance.

![images](images/8.png)

10. Once the instance is launched, go to the "Actions" dropdown menu and select "Networking

![images](images/9.png)

11. Go to the "Actions" 

![images](images/10.png)

12. Select the Elastic IP address you want to associate with the instance.

13. Connect to your Ec2 instance , for this project i will be ssh into my instance

![images](images/12.png)

14. I am using the Aws cloud shell 

![images](images/13.png)

15. SSH into the Cloud Shell

![images](images/14.png)


### Install Nginx and Setup Your Website

- Execute the following commands.

`sudo apt update`

`sudo apt upgrade`

`sudo apt install nginx`

![images](images/15.png)


- Start your Nginx server by running the `sudo systemctl start nginx` command, enable it to start on boot by executing `sudo systemctl enable nginx`, and then confirm if it's running with the `sudo systemctl status nginx` command.

![images](images/17.png)

- Visit your instances IP address in a web browser to view the default Nginx startup page.

![images](images/18.png)

- Download your website template from your preferred website by navigating to the website, locating the template you want.

- Right click and select **Inspect** from the drop down menu.

![images](images/19.png)

- Click on the **Network** tab and then click **Download** button.

![images](images/20.png)

- Right click on the website name, select **Copy** and click on **Copy link address**.

![images](images/21.png)



![images](images/22.png)

- To install the unzip tool, run the following command: **`sudo apt install unzip`**.

![images](images/23.png)


- cd into /var/www/html

![images](images/24.png)


- Execute the command to download and unzip your website files sudo curl -o /var/www/html/2135_mini_finance.zip https://www.tooplate.com/zip-templates/2135_mini_finance.zip && sudo unzip -d /var/www/html/ /var/www/html/2135_mini_finance.zip && sudo rm -f /var/www/html/2135_mini_finance.zip

![images](images/25.png)


**Here's an explanation of the command:**

The command **`sudo curl -o /var/www/html/2135_mini_finance.zip https://www.tooplate.com/zip-templates/2135_mini_finance.zip && sudo unzip -d /var/www/html/ /var/www/html/2135_mini_finance.zip && sudo rm -f /var/www/html/2135_mini_finance.zip`** performs a series of actions to download, unzip, and clean up a website template file. Here’s a breakdown of each part of the command:

1. **`sudo curl -o /var/www/html/2135_mini_finance.zip https://www.tooplate.com/zip-templates/2135_mini_finance.zip`**: 
   - `sudo`: Runs the command with superuser (root) privileges.
   - `curl -o /var/www/html/2135_mini_finance.zip`: Downloads the file from the specified URL (`https://www.tooplate.com/zip-templates/2135_mini_finance.zip`) and saves it as `2135_mini_finance.zip` in the `/var/www/html` directory.

2. **`&&`**: Logical AND operator, which ensures that the next command runs only if the previous command succeeds.

3. **`sudo unzip -d /var/www/html/ /var/www/html/2135_mini_finance.zip`**:
   - `sudo`: Runs the command with superuser (root) privileges.
   - `unzip -d /var/www/html/`: Extracts the contents of the zip file into the `/var/www/html/` directory.
   - `/var/www/html/2135_mini_finance.zip`: Specifies the path to the zip file to be unzipped.

4. **`&&`**: Logical AND operator, which ensures that the next command runs only if the previous command succeeds.

5. **`sudo rm -f /var/www/html/2135_mini_finance.zip`**:
   - `sudo`: Runs the command with superuser (root) privileges.
   - `rm -f`: Removes (deletes) the specified file forcefully (without prompting for confirmation).
   - `/var/www/html/2135_mini_finance.zip`: Specifies the path to the zip file to be deleted.

   
In summary, this command downloads the website template file, extracts its contents to the web server directory, and then deletes the downloaded zip file to clean up the directory.

---

- Download the 2nd website template by running the following command:

```
sudo curl -o /var/www/html/2134_gotto_job.zip https://www.tooplate.com/zip-templates/2134_gotto_job.zip && sudo unzip -d /var/www/html/ /var/www/html/2134_gotto_job.zip && sudo rm -f /var/www/html/2134_gotto_job.zip
```
![images](images/26.png)

> [!NOTE]
Replace the placeholders in the code with your own website URL. For example, substitute **`https://www.tooplate.com/zip-templates/2134_gotto_job.zip`** with your chosen URL, and change **`2134_gotto_job.zip`** accordingly.


- ls into it to check if both folder are in the directory

![images](images/27.png)


- To set up your website's configuration, start by creating a new file in the Nginx sites-available directory. Use the following command to open a blank file in a text editor: **`sudo nano /etc/nginx/sites-available/`**

![images](images/28.png)


- Copy and paste the following code into the open text editor.
```
server {
    listen 80;
    server_name example.com www.example.com;

    root /var/www/html/example.com;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```


- Edit the `root` directive within your server block to point to the directory where your downloaded website content is stored.

![images](images/29.png)

- Configure your second website by creating a new file in the Nginx sites-available directory with the following command: `sudo nano /etc/nginx/sites-available/gotto `.


- Copy and paste the following code into the open text editor.

```
server {
    listen 80;
    server_name placeholder.com www.placeholder.com;

    root /var/www/html/placeholder.com;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

- Edit the **`root`** directive within your server block to point to the directory where your downloaded website content is stored.

![images](images/30.png)

- Create a symbolic link for both websites by running the following command.
`sudo ln -s /etc/nginx/sites-available/cleaning /etc/nginx/sites-enabled/`
`sudo ln -s /etc/nginx/sites-available/health /etc/nginx/sites-enabled/`

![images](images/31.png)

- Run the **`sudo nginx -t`** command to check the syntax of the Nginx configuration file.

- Delete the default files in the sites-available and sites-enabled directories by executing the following commands:

```
sudo rm /etc/nginx/sites-available/default
sudo rm /etc/nginx/sites-enabled/default

```
![images](images/33.png)


![images](images/34.png)

- Restart the Nginx server by executing the following command: **`sudo systemctl restart nginx`**.

---
![images](images/32.png)


### Create An A Record

To make your website accessible via your domain name rather than the IP address, you'll need to set up a DNS record. I did this by buying my domain from Namecheap and then moving hosting to AWS Route 53, where I set up an A record.

Search for route 53 in your Aws console
![images](images/35.png)

- In route 53, select the domain name and click on **Create record**, Paste your **IP address①** and then click on **Create records②**.

![images](images/37.png)


- Click on **Create record** again, to create the record for your sub domain.

![images](images/38.png)

- Input the **Record name①**, paste your **IP address②** and then click on **Create records③**.

![images](images/39.png)

- Repeat the same process while creating your second subdomain record, and confirm that they both exist in the records list.

![images](images/40.png)

- Open your terminal and run **`sudo nano /etc/nginx/sites-available/finance`** to edit your settings. Enter the name of your domain and then save your settings.

![images](images/42.png)

- Run **`sudo nano /etc/nginx/sites-available/gotto`** to edit your settings. Enter the name of your domain and then save your settings.

![images](images/43.png)

- Restart your nginx server by running the **`sudo systemctl restart nginx`** command.

![images](images/46.png)
- Go to your domain name in a web browser to verify that your website is accessible.

![images](images/44.png)


![images](images/45.png)



> [!NOTE]
You may notice the sign that says **Not secure**. Next, you'll use certbot to obtain the SSL certificate necessary to enable HTTPS on your site.

---

### Install certbot and Request For an SSL/TLS Certificate

- Install certbot by executing the following commands:
`sudo apt update`
`sudo apt install python3-certbot-nginx`
`sudo certbot --nginx`

![images](images/47.png)


- Execute the **`sudo certbot --nginx`** command to request your certificate. Follow the instructions provided by certbot and select the domain name for which you would like to activate HTTPS.

![images](images/48.png)

![images](images/49.png)

> [NOTE]
In this case, SSL certificates were only created for **`finance.arafdevops.work`** and **`gotto.arafdevops.work`**. So, when prompted, I entered the numbers 1 and 3 (corresponding to those two domains) to select them for certificate generation. If we had also created records for **`www.finance.arafdevops.work`** and **`www.gotto.arafdevops.work`**, I could have simply pressed Enter to accept the default selection (**all available records**). If you try to create a certificate without having created an A record first, you will receive an error message.

- Verify the website's SSL using the OpenSSL utility with the command: **`openssl s_client -connect gotto.arafdevops.work:443`**

![images](images/50.png)

- Visit **`https://<domain name>`** to view your websites.

![images](images/51.png)


![images](images/52.png)

---
---

#### The End Of Project 2

