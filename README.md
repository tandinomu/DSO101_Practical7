# DSO101_Practical7

# Node.js Jenkins Shared Library

## Objective

To demonstrates the implementation of a Jenkins Shared Library to standardize and streamline CI/CD processes for Node.js applications. The shared library provides reusable pipeline components that can be utilized across multiple projects, ensuring consistency and reducing code duplication.

## Project Structure

### 1. Shared Library Repository
**Repository:** `https://github.com/tandinomu/nodejs-pipeline-library`

### 2. Node.js Application Repository
**Repository:** `https://github.com/tandinomu/Node.js-App`


## Implementation Process

### Phase 1: Shared Library Development

**1. Repository Creation and Structure**

Created the shared library repository with the standard Jenkins structure.

### Phase 2: Jenkins Configuration

**1. Plugin Installation**
- Verified **Pipeline: Shared Groovy Libraries** plugin installation
![plugin](./images/plugin.png)

**2. Global Library Configuration**

Configured the shared library in Jenkins:
- **Path:** Manage Jenkins → Configure System → Global Pipeline Libraries
- **Settings:**
![gl](./images/library.png)

### Phase 3: Application Development


#### 1: Node.js Application Setup

**Created a new Node.js application:**

```bash
mkdir my-simple-app
cd my-simple-app
npm init -y
```

**Modified `package.json` to include start script:**

```json
{
  "name": "my-simple-app",
  "version": "1.0.0",
  "scripts": {
    "start": "node server.js"
  }
}
```

**Developed basic application file `server.js`:**

```javascript
console.log("Hello from Node.js Application!");
console.log("Server started successfully at:", new Date().toLocaleString());
```

### Step 2: Pipeline Configuration

**Created `Jenkinsfile` in the application root directory:**

```groovy
@Library('my-shared-lib') _

pipeline {
    agent any
    stages {
        stage('Setup Dependencies') {
            steps {
                installDependencies()
            }
        }
        stage('Execute Application') {
            steps {
                sh 'npm start'
            }
        }
    }
}
```

## Build Execution Results

**When the Jenkins pipeline was triggered:**

* Jenkins successfully retrieved both the application repository and shared library
* The `installDependencies()` function from the shared library executed `npm install`
* Application startup was triggered using `npm start`, which executed `node server.js`
* Console output displayed: **"Hello from Node.js Application!"**

## Summary

This practical implementation achieved:

* **Successful integration** of Jenkins Shared Libraries with Node.js applications
* **Code reusability** by utilizing centralized pipeline functions
* **Automated execution** of Node.js applications through Jenkins pipelines

Jenkins Shared Libraries provide an effective solution for standardizing CI/CD processes and eliminating redundant pipeline code across multiple projects.

## Repository Information

* **Application Repository:** [my-simple-app](https://github.com/tandinomu/Node.js-App)
* **Shared Library Repository:** [my-shared-lib](https://github.com/tandinomu/nodejs-pipeline-library)