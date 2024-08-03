**Project Overview: Continuous Integration Pipeline with Google Cloud**

In this project, you'll create a continuous integration (CI) pipeline using various Google Cloud services, including Cloud Source Repositories, Cloud Build, build triggers, and Container Registry.

### Prerequisites

To complete this project, you should be familiar with the following Google Cloud tools:
- Cloud Source Repositories
- Cloud Build
- Build triggers
- Container Registry

### Objectives

By the end of this lab, you will have accomplished the following tasks:
1. Create a Git repository on Google Cloud.
2. Develop a simple Python Flask web application.
3. Test your web application in Cloud Shell.
4. Define a Docker build process.
5. Manage Docker images using Cloud Build and Container Registry.
6. Automate builds using triggers.
7. Test your build changes.

### Task Breakdown

#### Task 1: Create a Git Repository

1. **Set up a Git Repository in Google Cloud**:
   - Navigate to the **Source Repositories** section in the Google Cloud Console.
   - Click **Add repository**, then select **Create new repository**.
   - Name the repository `devops-repo` and select your current project ID.
   - Click **Create**.

2. **Prepare Your Environment**:
   - Open Cloud Shell from the Google Cloud Console.
   - Run the following commands:
     ```bash
     mkdir gcp-course
     cd gcp-course
     gcloud source repos clone devops-repo
     cd devops-repo
     ```

#### Task 2: Create a Simple Python Application

1. **Develop a Python Flask Application**:
   - Open the Cloud Shell Code Editor.
   - Create a new file named `main.py` and paste in the following code from the repository: [main.py](https://github.com/NikhilVanka/CI-CD-with-Google-Cloud/blob/main/main.py).

2. **Set Up the Application’s Templates**:
   - In the `devops-repo` directory, create a new folder named `templates`.
   - Inside the `templates` folder, create two new files:
     - `layout.html`: Add the code from [layout.html](https://github.com/NikhilVanka/CI-CD-with-Google-Cloud/blob/main/layout.html).
     - `index.html`: Add the code from [index.html](https://github.com/NikhilVanka/CI-CD-with-Google-Cloud/blob/main/index.html).

3. **Manage Dependencies**:
   - Create a `requirements.txt` file in the `devops-repo` directory and add the dependencies listed here: [requirements.txt](https://github.com/NikhilVanka/CI-CD-with-Google-Cloud/blob/main/requirements.txt).

4. **Commit and Push Changes**:
   - In Cloud Shell, run the following commands:
     ```bash
     git add --all
     git config --global user.email "you@example.com"
     git config --global user.name "Your Name"
     git commit -a -m "Initial Commit"
     git push origin master
     ```
   - Verify the changes by refreshing the Source Repositories page.

#### Task 3: Define a Docker Build

1. **Create a Dockerfile**:
   - In the `devops-repo` directory, create a new file named `Dockerfile`.
   - Paste the Dockerfile content from [here](https://github.com/NikhilVanka/CI-CD-with-Google-Cloud/blob/main/Dockerfile).

#### Task 4: Manage Docker Images with Cloud Build and Container Registry

1. **Build the Docker Image**:
   - Ensure you are in the `devops-repo` directory, then run:
     ```bash
     echo $DEVSHELL_PROJECT_ID
     gcloud builds submit --tag gcr.io/$DEVSHELL_PROJECT_ID/devops-image:v0.1 .
     ```
   - If prompted, enable Cloud Build.

2. **Verify the Image**:
   - Go to **Container Registry** in the Cloud Console and confirm that your image is listed.
   - Check the **Cloud Build** service for your build history.

3. **Test the Image on Compute Engine**:
   - Create a new VM instance in **Compute Engine**.
   - After the VM starts, test the application by accessing the VM’s external IP address.

4. **Commit and Push the Dockerfile**:
   - In Cloud Shell, run:
     ```bash
     git add --all
     git commit -am "Added Docker Support"
     git push origin master
     ```
   - Verify the changes in Source Repositories.

#### Task 5: Automate Builds with Triggers

1. **Set Up a Build Trigger**:
   - Navigate to **Cloud Build** > **Triggers**.
   - Create a new trigger named `devops-trigger`:
     - Select your `devops-repo` repository.
     - Choose `.*(any branch)` for the branch.
     - Use `Dockerfile` for configuration.

2. **Test the Trigger**:
   - Click **Run trigger** and check the build history for the build progress.
   - Verify the newly created image in **Container Registry**.

3. **Make a Code Change**:
   - Modify the `main.py` file’s title to `"Hello Build Trigger."` and commit the change:
     ```bash
     git commit -a -m "Testing Build Trigger"
     git push origin master
     ```
   - Check for a new build in **Cloud Build**.

#### Task 6: Test Your Build Changes

1. **Deploy and Test the Updated Image**:
   - Deploy the new image to a VM instance, and allow HTTP traffic.
   - Access the VM’s external IP to verify the updated application.

Congratulations! We’ve successfully built and tested a continuous integration pipeline using Google Cloud’s suite of tools.

---

*Note: This project is based on a lab from Qwiklabs. The code and process are used here for educational purposes.*
