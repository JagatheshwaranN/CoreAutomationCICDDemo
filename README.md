Automating Deployment of Core Automation Framework to JFrog Artifactory Using CI/CD and GitHub
----------------------------------------------------------------------------------------------

Scenario
---------
We faced a challenge where the deployment of our Core Automation Framework to JFrog Artifactory was being done manually. This process
was time-consuming and prone to human error. To streamline this, we aimed to automate the deployment process, eliminating the need for
manual intervention.

Solution
---------
We resolved this challenge by integrating CI/CD practices with GitHub and Jenkins. Here’s a step-by-step breakdown of the solution:

Set Up GitHub Repository
------------------------
First, we created a GitHub repository for the Core Automation Framework.
We pushed the existing code from our local environment to this remote repository. This allowed us to have a centralized version control
system that facilitated collaboration and tracking of changes.

Configure Jenkins Job
---------------------
Next, we set up a Jenkins job specifically for the Core Automation Framework.
Jenkins was chosen due to its robust plugin ecosystem and ease of integration with various tools, including JFrog Artifactory.

Generate GitHub Webhook URL
---------------------------
We generated a webhook URL in Jenkins. This URL is crucial as it allows Jenkins to be triggered by events happening in the GitHub repository.
Since the webhook URL needs to be publicly accessible, we used a service like socketxp to convert the local webhook URL to a public URL.

Configure GitHub Webhook
------------------------
We then configured the generated public webhook URL in the GitHub repository settings.
This configuration ensures that any changes pushed to the repository trigger the webhook, which in turn triggers the Jenkins job.

Automated Deployment Process
----------------------------
With the webhook in place, every time a commit is made to the GitHub repository, the webhook triggers the Jenkins job automatically.
The Jenkins job then builds the project and deploys the artifact to JFrog Artifactory without any manual intervention.

SocketXP
--------
SocketXP is a cloud-based service that provides secure and reliable tunneling solutions, often used for exposing local servers or 
applications to the internet. It is particularly useful for developers and IT professionals who need to access and test their 
applications remotely. Here are some key features and uses of SocketXP:

Key Features and Use Cases
--------------------------
Secure Remote Access
--------------------
Provides a secure way to access IoT devices behind firewalls or NAT routers.
Enables remote SSH access for configuration and troubleshooting. 

IoT Device Management
---------------------
Offers a centralized platform to manage multiple IoT devices.   
Facilitates remote configuration, software updates, and monitoring.

Public Web URL Generation
-------------------------
Creates unique public URLs for private web applications running on IoT devices.   
Allows external services to interact with IoT devices securely.   

It provides public URLs for your local applications, making it easy to share and 
access them from anywhere. This is particularly useful for webhooks, testing APIs,
and remote debugging.

Data Transfer
-------------
Securely transfers data between IoT devices and cloud-based applications. 

Github Webhook
--------------
A GitHub webhook is a feature that allows you to receive real-time notifications when certain events happen in a GitHub repository.
These notifications are sent to a specified URL via an HTTP POST request, allowing external services or applications to react to 
these events automatically. Webhooks can be configured to listen for specific events such as pushes, pull requests, issues, and more. 
This makes them highly customizable and efficient for various workflows.

Uses of GitHub Webhooks in CICD
-------------------------------
Webhooks can trigger CI/CD pipelines automatically when code is pushed to a repository. This ensures that tests are run, and deployments
are made seamlessly without manual intervention.

Detailed Steps to Automate Deployment of Core Automation Framework to JFrog Artifactory
---------------------------------------------------------------------------------------
Step 1: Create the Core Automation Framework
--------------------------------------------
Create your Core Automation Framework to serve as the base code for the product teams.

Step 2: Set Up JFrog Artifactory
--------------------------------
1. Create an account on JFrog Artifactory.
2. Within your JFrog Artifactory account, establish a repository to store snapshots of your Core Automation Framework
3. For detailed setup instructions, refer to the Repository "JFrogArtifactoryUsage" Readme section.

Step 3: Set Up GitHub Repository
--------------------------------
1. Create a GitHub account.
2. Create a repository for the Core Automation Framework.
3. Push your local code to this repository.

Step 4: Jenkins Job Creation
----------------------------
On your Jenkins server, create a "Freestyle project" dedicated to your Core Automation Framework.

**Configure the job with the following details**

**Source Code Management:** 
Provide the URL of your GitHub repository (created in step 3).

**Branches to build:**
Specify the relevant branch to build from.

**Build Triggers:** 
Select "GitHub hook trigger for GITScm polling" option.

**Build Steps:** 
Set the goal as "deploy -DskipTests".

Save the job configuration.

Step 5: Configure Jenkins GitHub Webhook
----------------------------------------
1. Access the Jenkins dashboard and navigate to "Manage Jenkins" -> "System Configuration" -> "System" 
   (Configure Global Settings and Paths).
2. Locate the "GitHub server" section and click on "Advanced."
3. Check the "Override Hook URL" checkbox. A Jenkins webhook URL will be displayed. Copy this URL for future use.
   (e.g., http://localhost:8081/github-webhook/)  

Important Note: This initial webhook URL is private and cannot be directly used by GitHub (which requires public URLs).

Step 6: Generate a Public URL with SocketXP
-------------------------------------------
If your Jenkins server resides behind a firewall or uses a private IP address, a public URL is required for GitHub 
communication. This step utilizes SocketXP (a third-party tunneling service) to achieve this.Note: This step is optional
if your Jenkins server is publicly accessible.

1. Download and install SocketXP based on your operating system from https://www.socketxp.com/download/.
2. Create a SocketXP account at https://portal.socketxp.com/#/login.
3. Retrieve your Auth Token from the SocketXP dashboard.
4. Open a command prompt and navigate to the directory containing the downloaded SocketXP executable.

**Follow these commands:**

1. login <Auth Token> (Replace <Auth Token> with your actual token).
2. socketxp connect <WebHook URL> (Replace <WebHook URL> with the one copied from Step 5).

Note: Use only the base URL (e.g., http://localhost:8080) in this command.
The command will generate a public URL. Append "/github-webhook/" to this URL to form the complete public URL.

Step 7: Configure Webhook in GitHub
-----------------------------------
1. Navigate to your Core Automation Framework repository in GitHub.
2. Access the "Settings" section and click on "Webhooks" in the left navigation pane.
3. Click on "Add webhook" and paste the public URL (generated in Step 6) into the "Payload URL" field.
4. Click on "Add Webhook" to establish the connection.

Step 8: Trigger the Jenkins Job
-------------------------------
1. Introduce modifications to your Core Automation Framework code.
2. Push the updated code to your GitHub repository.
3. The configured webhook will detect the changes and trigger the corresponding Jenkins job.
4. The Jenkins job will then automatically deploy your updated code to the designated JFrog Artifactory repository.






