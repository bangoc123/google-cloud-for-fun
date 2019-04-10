## Nodejs App Auto-deployment with Travis CI in Google Cloud

Hey Ngoc here!!!

[Continuous Integration](https://www.thoughtworks.com/continuous-integration) has been becoming an important aspect in software development. The fundamental idea came from the needs of speed and convinence in deployment. 

With the help of some automatic tools such as [Jenkin](https://jenkins.io/), [CircleCI](https://circleci.com/) or 
[Travis](https://travis-ci.org/), developers are able to save a plenty of time and more importantly reduce the incidents in deploying their applications.

Why did I choose **Travis** for this project?

In fact, I have been using **CircleCI** for 2 years and **Jenkin** for 3 years, yet the reason for choosing [Travis] because it's **CircleCI** combined with **Jenkin**. Interestingly, It inherited some cool features like pretty user-friendly dashboard, good speed :) from **CircleCI** and it's free like **Jenkin**. How awesome it is!!!!

Why did I decide to make a demonstration of **Nodejs** instead of using Python or Ruby?

The simple castalys for using Nodejs is a small number of Docs related to applying CI/CD with Nodejs in Google Cloud. Additionally, I have been a Nodejs developer for more than 3 years. :D

### Tutorial Outline
- 0. [Before you begin](#0-before-you-begin)
- 1. [Setup Nodejs App](#1-setup-nodejs-app)
- 2. [Setup App Engine](#2-setup-app-engine)
- 3. [Enable neccessary apis](#3-enable-neccessary-apis)
- 4. [Integrate Github with Cloud Shell](#4-integrate-github-with-cloud-shell)
- 5. [Integrate Travis with Github Repository](#5-integrate-travis-with-github-repository)

### 0. Before you begin

Please create two accounts [Travis](https://travis-ci.com/) and [Github](https://github.com/) if you haven't had yet.

### 1. Setup Nodejs App

#### 1.1 Initialize a Nodejs project

Type this command to initialize Nodejs Project ```npm install```

<img src="https://lh3.googleusercontent.com/urg-mS_kp74U8hhMkKvvb8NRjyAwhRH1nAGlVdwsZinNV-KPThVN1TsVK69ylALKeILT7ymFKxDvn23eTLhmTaF7gn7hnm6tfIvC399fMKeTdXNy6mfkgEE2AKyzgIc7aIgTVob_yBo_4hUQyVffDiGxYVrG18r3yofHh1YGEZP_VoLwWRxPhMCovo0vjbx-WRGDOhbHKrwMu7RdnydstqZPRAr7b3NS82A71-1sfPZYwodEPEWSYWuJkrpt-610NulSpuJiWLvyxw_lxprE1kgYIaekUC977LTXqpM1pi-4ity8fBXTYhK3MwmJbE_a0yCz7omHWdJoibHj0dvb_aBUIL3vFtfG1cXJhN2PmEIQ6TaXHcJ5mPLmvzJkM4ZPbRwciJoMoC7ODUQ0qovpswNoVLVy7WAy1Quw1c4_iREOgsIHmlt79Wcuh8mEgVceBGx8q8quxgg2zyN2Gwd24TfpyirTqnHyW83ojpVCmwG5eXsxiOl3E4UOalAvAdgsyuTD0G3iTi4zNtenJaOFDw14E2sLHTrDZTadYtRtxXu_IKQz_Y2_cIz97-YNmLlb1E2SQ2s86Xr2gCNmSV0RHup4y_BMeydvw2n6PO13AJGAaItBBz4XHbMEBMUnmJLyI9vU9MUGcMBdQQdUXTButd8eOcHlFSORfHXVIG84IaQHju_KxSmZhwGrAREHCk60tECX04X_Nk5SGQUCsj4InASX=w1306-h902-no" width=500>

We notice that a package.json is created instantly in your project.

<img src="https://lh3.googleusercontent.com/-Kz4QTbF9AXur3ZE7lPds7YOAszT4Qw8I3-orAGKeWwQWAdaJ6ujxnTxUSmOLmneb9lwUNLbWuIVxG3OfYjRWoqC8A-3BRUuhbgGiZNu_4XVJPlidJvu6f-OpR8NWnlAd3cyzQB0J3EB5Sq4VB0mjw2WDI9P0RnscmbAo-hyK9fdcz1qkfvLdUVq01vTE9R4gnA8hvOAb9Oh2ErBmf9BHjsETp-nfSdUmQOl9SOF823V3DdZr6wpl_tuFBjY0w5wBCgogXiugI3BigNVAlfJN3SH6UU3qIlCj-Mk9rXvL2OdCY6vE35UrjArLol2wwkMzVwgTnO5URmBx-TbnWkzayH-iown3DmMCJsHhQS9pALzhjFJF-ClsRRZtuzH-7h72N-vN5oaDPSeLhbw4kPM9c8tu-xOuh81EUwg_QdIg3aaPKzKkleKNYUg0BNscOinTrGTReF5svWRVPwq_kZcLDGpeUFQK48c2L9Q5pqg-1cTV8keax-2pQG6bEW0IVAkpV7YitSuitZcJDttaCCQHlobhZQL-LWrd-ZV3hMCqQkXWGFkImh0ltt0owNNHzchrY3hpV5u4aS9GG3rn4oDGMxE5wN4yOwepJoTU4ljfU-FK41D6od_uU52ijGQbNwxlrs7Awd1Wwr5t6_AxYqXDBQjjZQbjIQJpIYKfAYAKaUfep75XMJrx4TElSHKL2IOtC6IvsIVDyqyYe9z6akYUUER=w1834-h1016-no" width=500>

#### 1.2 Install dependencies

We install two things:

- [Express](https://expressjs.com/) - Web framework for Node.js
- [EJS](https://ejs.co/) - Embedded JavaScript templating.

<img src="https://lh3.googleusercontent.com/60qu6QKJGPPGnZX24AtNmM1Y2xb6_9dgTc3hA1hEaGWbMgii7JEQ9zUTegX22RlHb8DxZoIy4rHkgTQGoC-mM8ekbg7Zga0Ol_xHwbbrpyFSxLB9BFj_CQfcQAoRuHXY4v1vMtsH2hVSWcYGw6xh1pAE1IyniZG_fqTsnC6RonpuljZOQuzBryVnC1gZT9ZpF4GwTSWBv1A6TN1OM2Kr4EZOYYDaB9YvCSh6zcDRQLiEWp0EX-eDGsoK6HCL2to6ZyGKz4070QnnvhBWukMOYqDldHbgRBtlw9dwfYXkPcjYSyWZvAwUpebeHQLALcQLfEoviPNRArKys2AYyLZ98rAaR3pir6IrR2U7PEB0c3HwuPsNxQFahNNAP_ptqxRSq84_A4pWN1loeXslKcrRIJSn7DZ2nPv2UiIo4iFQf7Ljhn8ociWPxuQJtOrtFZCFVMK7tGLYP7nRpiI6zrbFDZaxrei8-n4sk_H50mERqkO6xVSb-eGx67K7-_xdQvc0S3Mg5W1BrJuJrt1fc3c6fNxCPUZAwvYa6pYjaaN31bQuLBQBetpl7ooNH9czq-b4gSXNAj_lly5HvM6KOQe_izXyBySgN7i5hXbvxKvR27g3GQjqVpEwTNmpXbzOr8p-o37hd3Faudy2lvHoc6tjBbQaoeMXNVp9D6y7uneqUkgJ71hIn_oBAoAe6YMSZiL92Y_-YYhb9hcMkj89mvHiWYco=w1304-h596-no" width=500>

#### 1.3 Implement app.js

Of course we need a function to start sever and serve some basic requests. 

We create an ```app.js``` file and add some simple lines of codes.

```
'use strict';

const express = require('express');
const app = express();

app.set('view engine', 'ejs');

app.get('/', (req, res) => {
  res.render('index');
});

// Start the server
const PORT = process.env.PORT || 8080;
app.listen(PORT, () => {
  console.log(`App listening on port ${PORT}`);
  console.log('Press Ctrl+C to quit.');
});

```

We will return a html page when the server receives a HTTP request from a client.

Although we set up to use port **8080** locally but when deploying these codes, App Engine is able to recognize it and change to suitable port such as **80** for http and **443** for https.

Subsequently, we add a folder called views contains a ejs file `index.ejs`.

<img src="./guide-images/nodejs-views.png" width=500>

Start app and enjoy!!!

<img src="./guide-images/start-app.png" width=500>

<img src="./guide-images/index-page.png" width=500>

### 2. Setup App Engine

#### 2.1 Access [Google Cloud](https://console.cloud.google.com)
#### 2.2 Create a new project

<img src="./guide-images/create-app-engine.png" width=500>

Name this project. I gave my project name as "Travis-nodejs" 


<img src="./guide-images/travis-nodejs.png" width=500>

#### 2.3 Create App Engine Application

Go **Menus > App Engine > Dashboard > Create Application**

<img src="./guide-images/creat-app-engine-2.png" width=500>

You can select your particular region. I chose **us-central**

<img src="./guide-images/create-app-engine-3.png" width=500>

**Create app** -> **Select Language**. I selected Nodejs.

<img src="./guide-images/create-app-engine-4.png" width=500>

**Finish app creation**

<img src="./guide-images/create-app-engine-5.png" width=500>

### 3. Enable necessary apis

Click here to [Enable essential apis](https://console.cloud.google.com/flows/enableapi?apiid=compute,books,appengine)

It consists of **Computer Engine**, **Google Books** and **App Engine APIs**.

<img src="./guide-images/enable-api.png" width=500>

It takes around 2-3 minutes to finish this progress.

Done!!!

<img src="./guide-images/enable-api-2.png" width=500>

### 4. Integrate Github with Cloud Shell

#### 4.1 Go to [Cloud Shell](https://console.cloud.google.com/cloudshell/)
You can imagine that Cloud Shell is simply a terminal in browser. You can use it as **PowerShell** in Windows or **Terminal** in Mac.

#### 4.2 [Generate SSH Key in Cloud Shell](https://help.github.com/en/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)


#### 4.3 [Add SSH Key to your Github Account](https://help.github.com/en/articles/adding-a-new-ssh-key-to-your-github-account#platform-linux)

#### 4.4 [Verify the link between Github and Cloud Shell works well](https://help.github.com/en/articles/adding-a-new-ssh-key-to-your-github-account#platform-linux)

#### 4.5 Clone your app from Github to Cloud Shell

<img src="./guide-images/clone-the-project-to-cloud-shell.png" width=500>

### 5. Integrate Travis with Github Repository

On **[Travis](https://travis-ci.com/)**, log in by your Github account.

Travis will list all your repositories. 

Note that: Two things required to integrate your repo to Travis

- You **own** this repository, meaning that if you are only the collaborator, you can not link the travis to your project. In this case, you need to ask the owner to help you enable it.
- An .travis.yml file **has been added already** to your repo in **root folder**. :). Copy all content of .travis.yml [here](https://github.com/bangoc123/google-cloud-for-fun/blob/master/.travis.yml).



<img src="./guide-images/travis-location.png" width=500>


You can see the screen like this on Travis Dashboard:

<img src="./guide-images/travis-dashboard.png" width=500>

Travis only is triggered when a commit is pushed to Github. At the first time, you may not see any log/build yet.

You can check whether the Travis is triggered or not at tab **Pull History**

<img src="./guide-images/travis-pull-history.png" width=500>

In case you don't see anything updated, please try to create a **test commit** and push it to Github. :)


### 6. Integrate Cloud Shell with Travis

#### 6.1 Install Travis client

```
  sudo gem install travis
```

#### 6.2 Create Google Cloud credentials

These credentials give **Travis** permissions to run some scripts automatically in Cloud Shell.  

These scripts are defined in **.travis.yml** 

- Create Service Account
  - Go to [Service Account Page](https://console.cloud.google.com/projectselector2/iam-admin/serviceaccounts?supportedpurview=project&project&folder&organizationId)
  - Select your project
  - Create service account
  - **Step 1**: Name your service account 
    <img src="./guide-images/service-account-1.png" width=300>
  - Step 2: Create roles for your account
    - Find and Select **App Engine Admin**. This role enables Travis to have full access to our App Engine.
    - Find and Select **Storage Admin**. This gives Travis full control of GCS resources.
    - Find and Select **Cloud Build Editor**. This allows Travis to run some scripts like **gcloud scripts** or libraries installations.
    <img src="./guide-images/service-account-2.png" width=300>

  - **Step 3**: Create Key > Json > Create. A Jason file will be downloaded automatically into your computer.

#### 6.3 Upload file to the project in Cloud Shell

Upload to Cloud Shell by using **Upload File** features.

  <img src="./guide-images/service-account-3.png" width=500>

  <img src="./guide-images/service-account-4.png" width=500>

  Note that the file you upload will be placed in **/home/your-account-name**. Therefore, you need to move it to the cloned project.

  ```
  mv ~/<your_credentials_filename>.json ~/google-cloud-for-fun/infrastructures/travis-ci-nodejs/client-secret.json
  ```

  Make sure everything will look like this:

  <img src="./guide-images/service-account-5.png" width=400>

#### 6.4 Create the Books API Key

  - Go to [APIs Credentials](https://console.cloud.google.com/apis/credentials)

  - Create API Key

  <img src="./guide-images/service-account-6.png" width=400>
  
  - Create  **api_key** file in Cloud Shell

  ```
  export API_KEY=[YOUR_API_KEY]
  cd ~/google-cloud-for-fun/infrastructures/travis-ci-nodejs
  echo "key = '${API_KEY}'" > api_key.py
  ```
  <img src="./guide-images/service-account-7.png" width=600>

#### 6.5 Encrypt credentials for Travis

- We will combine **client-secret.json** and **api_key** into a single file **credentials.tar.gz** by using the script:

  ```
  tar -czf credentials.tar.gz client-secret.json api_key.py
  ```
- Login to Travis CI

  ```
  travis login --pro
  ```
  You will use the Github Account to login into **Travis**

  <img src="./guide-images/travis-login.png" width=600>
  
- We need to encrypt this file for public usage

  Use this command:
  ```
  travis encrypt-file credentials.tar.gz --pro
  ```
  
  <img src="./guide-images/encrypt-credentials.png" width=600>

#### 6.5 Update Travis file

- Replace text **DECRYPT_COMMAND** in .travis.yml by the text begining with **openssl aes...** in Cloud Shell.
  ```
  sed -i 's/DECRYPT_COMMAND/[YOUR_COMMAND_OUTPUT]/g' .travis.yml
  ```

  <img src="./guide-images/travis-encrypt.png" width=600>
  
- Replace text **travis-nodejs** in .travis.yml by your project ID in Cloud Shell.

  ```
  sed -i "s/travis-nodejs/${DEVSHELL_PROJECT_ID}/g" .travis.yml
  ```

  <img src="./guide-images/project-id.png" width=400>

- Push changes to Github

  ```
  git add credentials.tar.gz.enc .travis.yml
  git commit -m "Adds encrypted credentials for Travis and updates project name"
  ```












