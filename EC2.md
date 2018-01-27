# Deploy to EC2    

![EC2 picture](https://cdn-images-1.medium.com/max/720/1*Y5Pan-z9hAdbeA06UtJyNw.png)

Cogrammers is stoked to bring you a no-frills, minimalist, step-by-step guide to deploying a dynamic Node app to AWS via EC2. No previous experience necessary.

## What you need:    

1. An AWS account (it’s free even though they ask for your credit card info)
2. A GitHub account
3. Access to your computer’s terminal (also known as shell or command line). Check out a youtube video on how to find it on your operating system (Mac, Windows, etc.) if you’re new to this.    

## What will happen:    

1. Create EC2 instance
2. Connect to that EC2 instance
3. Deploy our Node app

## Technologies we will use:    
* EC2
* Ubuntu
* Linuxbrew
* NGINX
* Node.js && NPM
* Postgresql
* Sequelize
* Vim    

It doesn’t matter what operating system you are working on today because we will be doing all of our work in the cloud. Cogrammers is inclusive by design :)

## Terminology:    
**Cloud**: The cloud refers to hosted space on the internet. It can be thought of like this: instead of storing <blank> on my local computer, I am going to push it to the cloud where it will be stored remotely.

**Server**: A computer with centralized data that feeds information to other computers.

**Instance**: An EC2 instance refers to virtual server space. These instances are created on an Amazon Machine Image (AMI).

**AMI**: An Amazon Machine Image is a template of a virtual machine environment. Worded another way, it is a snapshot of an operating system created for the purpose of computing in the cloud. Off of this image, the server (or instance) will run. For this demo, we will be using a Linux based operating system image.

**Container**: A container holds the whole of our virtual environment including operating system, server, code, libraries, and settings. Containers compartmentalize virtual working environments like keeping staging (the final draft of code before publishing) separate from development (rough drafts of code in test mode).

### Let’s get started by navigating to the EC2 launchpad    
Make your way to the AWS management console and select EC2 from the Services drop-down menu (under the Compute category).

Notice that there is a geographical location listed in your top navigation bar. This is the physical region in which your server lives. Feel free to choose your preferred location.

Click on `Launch Instance`.

![](https://cdn-images-1.medium.com/max/720/1*hD41xo0wtUDzOB_rHjtZcA.png)

### Choosing which AMI to launch    
We are going to launch our instance with the latest Ubuntu virtual machine (VM) in the form of an AMI.

In the left-hand dashboard, select the AWS Marketplace tab and search for `Ubuntu`. There are many options here. Some are official images and some are unofficial or out of date.

![](https://cdn-images-1.medium.com/max/720/1*cZLjVcIbVJUoGOvpvNf2YQ.png)

The way to know that you are choosing the right one is via the Ubuntu Cloud Image Finder.
Once there, search for your server’s region. You can find your server’s searchable region in your aws console url. 

![](https://cdn-images-1.medium.com/max/720/1*TpPNVsznZ3gfzRbNitD98Q.png)

In the results you’ll be looking for:

Amazon AWS, <your server’s region>, <the latest version of Ubuntu>, and an instance type of hvm-ssd (stands for Hardware Virtual Machine & Solid State Drive).
  
Copy the AMI that matches your search results. In this case, our AMI is `ami-2eb40856`.

![](https://cdn-images-1.medium.com/max/720/1*s4Ejy3U1A_ngIm2Qp3W29w.png)

Now, back to the AWS instance launch screen — choose the `Community AMIs` tab from the left-hand dashboard and search for your AMI key (as seen below). **It is important to note the root device type of ebs (Elastic Block Store). The root device is where your persistent storage (backup) of this instance lives. Without this, every time your instance is ever stopped and then started again, any state on your VM is considered temporary and is wiped clean.** Select your machine image.

![](https://cdn-images-1.medium.com/max/720/1*xckBCTaSHi8wBkOBcuG8sA.png)

### Choosing the instance type

Next, we are going to choose the instance type. **The instance type is simply choosing how many resources you want to use.** We are going with the free tier version for our portfolio since we won’t need that many resources. Free tier is available for the first year of your AWS account.

Hit Next until `Step 6: Configure Security Group` is reached.

![](https://cdn-images-1.medium.com/max/720/1*0Y3OxB-Yp52NoqONUeOhUg.png)

### Set up your security group

Security groups filter outgoing/incoming traffic from an instance. This is AWS’s EC2 firewall settings.

There are 2 ways to enable security settings: create new rules or select an existing set of rules. We are going to create new rules.

Let’s label it as: `General SG`. Add a description of: *This SG will be assigned to all web based instances.*

=> **NOTE**: If this was a larger project with a development environment and a separate production environment, we would have separate security groups for that. We won’t go over that right now, but it is essential when working on larger projects.
