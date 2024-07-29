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
