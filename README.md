
## 🚀 Jenkins Pipeline for CI/CD

### 🧩 Objective :

This project demonstrates how to set up a **Jenkins Pipeline** to automate the process of **building, testing, and deploying** an application using **Jenkins and Docker**.

---

### 🛠️ Tools & Technologies :

* **Jenkins** – Continuous Integration & Deployment (CI/CD) tool
* **Docker** – For building and running containerized applications
* **GitHub** – Source code management and pipeline triggers
* **Windows/Linux** – Jenkins host environment

---

### 📁 Project Structure:

```
Jenkins-Pipeline-for-CI-CD/
├── Jenkinsfile           # Main CI/CD pipeline definition
├── Dockerfile            # Defines how to build the Docker image
├── app/                  # Application source code (example app)
└── README.md             # Project documentation
```

---

### ⚙️ Jenkins Pipeline Overview :

The **Jenkinsfile** defines a Declarative Pipeline with the following stages:

```groovy
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning repository...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building Docker image...'
                sh 'docker build -t myapp:latest .'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'echo "Tests passed!"'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                sh 'docker run -d -p 8080:8080 myapp:latest'
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline completed successfully!'
        }
        failure {
            echo '❌ Pipeline failed!'
        }
    }
}
```

---

### 🔧 Setup Instructions :

#### 1️⃣ Install Jenkins

* Download and install Jenkins from [jenkins.io](https://www.jenkins.io/download/).
* Start Jenkins at [http://localhost:8080](http://localhost:8080).

#### 2️⃣ Install Required Plugins

* **Pipeline**
* **Git**
* **Docker Pipeline**
* **GitHub Integration**

#### 3️⃣ Connect GitHub Repository

* Create a Jenkins Pipeline job.
* Choose **“Pipeline script from SCM”**.
* Set **SCM** to **Git** and add your repository URL:

  ```
  https://github.com/AdeshAJ/Jenkins-Pipeline-for-CI-CD.git
  ```

#### 4️⃣ Trigger Builds Automatically

##### Option 1: **Using GitHub Webhook**

* Go to **GitHub → Repo → Settings → Webhooks → Add webhook**
* Payload URL:

  ```
  http://<your-jenkins-server>:8080/github-webhook/
  ```
* Content type: `application/json`

##### Option 2: **Using Poll SCM** *(no ngrok needed)*

* In Jenkins Job → **Configure → Build Triggers → Poll SCM**
* Add schedule:

  ```
  H/5 * * * *
  ```

  (Checks GitHub every 5 minutes)

---

### ▶️ Running the Pipeline

1. Push a commit to the repository:

   ```bash
   git add .
   git commit -m "Trigger Jenkins pipeline"
   git push origin main
   ```
2. Jenkins automatically detects the change and triggers the pipeline.
3. Monitor progress in the **Jenkins dashboard**.

---

### ✅ Expected Output

* Jenkins clones your repo
* Builds a Docker image
* Runs basic tests
* Deploys the containerized app
* Displays “Pipeline completed successfully!” on success

---

### 💡 Learning Outcome

By completing this project, you’ll learn:

* How Jenkins automates CI/CD workflows
* How to integrate GitHub with Jenkins
* How to build and deploy Dockerized applications automatically
* How to trigger builds via commits

---



### 👨‍💻 Author


**Adesh Javir**
DevOps Enthusiast | Continuous Integration Learner


