### Brief

The objective of this assignment is to set up a continuous integration and continuous deployment (CI/CD) pipeline for a Node.js application that is deployed on a serverless platform with Secret Management in placed!.

Instructions:

1.  Create a new Node.js **application** using the Express framework.
2.  Set up **automatic testing** for the application using a testing framework such as Jest or Mocha.
3.  Create **new branch** on your existing repository.
4.  Set up a CI/CD pipeline using a tool such as Github Action, Jenkins, Travis CI, or CircleCI.
5.  Configure the pipeline to automatically build and test the code whenever changes are pushed to the code repository.
6.  Deploy the application to a serverless platform such as AWS Lambda or Google Cloud Functions.
7.  **Store some information using Secret Management on AWS, then get the information as part of the pipeline.**
8.  Configure the pipeline to automatically deploy the code to the serverless platform whenever changes are pushed to the code repository and all tests pass.
9.  Write a documentation explaining the steps you have done, including the tools and services used.

Deliverables:

-   The Node.js application with automatic testing set up
-   Code repository with the CI/CD pipeline configured
-   Documentation explaining the steps taken to set up the pipeline.

# 

# 

# Step 0 – create github repository

![A screenshot of a computer Description automatically generated with medium confidence](media/4d4e751855d6655415a3bc412d3d4d4f.png)

# Step 1 – create a local folder on your local machine

We will clone into here at the next step

![A screenshot of a computer Description automatically generated](media/e1cc9fdeb8291abb46f440a2c696b221.png)

# Step 2 – Clone repo to local host-folder created at the step above

1.  Open terminal in the folder above

![A screen shot of a computer Description automatically generated with medium confidence](media/6d73d03403b631d8c891bd4030c97e55.png)

1.  \$ git clone https://github.com/muhammedtaufiq/3.13_assignment.git

| ![A screenshot of a computer Description automatically generated with medium confidence](media/45a6351ffb8de1fa0f09159b829775df.png) | ![](media/f5e33ededdc41c1d743871ccdeee75c1.png) |
|--------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------|

\#ensure you cd into the git project root

# Step 3 – creating index.js file to hold my application

![A screen shot of a computer Description automatically generated with medium confidence](media/1ff4a30699fe56ca91d6e7c58cd86128.png)

module.exports.handler = async (event) =\> {

return {

statusCode: 200,

body: JSON.stringify(

{

message: "Go Serverless v3.0! Your function executed successfully!",

input: event,

},

null,

2

),

};

};

# Step 4 create serverless .yml to contain instructions for serverless

Ref: [Serverless Framework Services](https://www.serverless.com/framework/docs/providers/aws/guide/services/#:~:text=When%20you%20deploy%20a%20service%2C%20all%20functions%2C%20events,to%20dev%20stage%20and%20us-east-1%20region%20on%20AWS.)

Template :

![A screenshot of a computer Description automatically generated](media/14e68bf4fc1f2fb6f702ccd1865fb84a.png)

# Step 5 – install and deploy serverless application

**Install express**

*\$npm install -g express*

![A screen shot of a computer Description automatically generated with medium confidence](media/ff156cba867c77800cbc9361768e77c7.png)

**Create json file**

*\$ npm init*

![A screenshot of a computer Description automatically generated with medium confidence](media/c23b0a068abb4496e139aace9fa21458.png)

![A screen shot of a computer Description automatically generated with low confidence](media/289dcb3872dc204a53dd579948625549.png)Package.json appears

*\$ npm install*

![A black screen with white text Description automatically generated with low confidence](media/52f41b1b33a73a6ca8df4ca44129d75a.png)

Do ensure serverless offline plugin is installed:  
![](media/ebabfa15c171a1c5e750b240a0ebd4a5.png)

**Deploying serverless**

*\$ serverless deploy*

![A screen shot of a computer program Description automatically generated with low confidence](media/1536a58d07e7a2fe3ad53675629def50.png)

**Acquire content from serverless to check its running**

You can now curl <https://m1aoenl1cj.execute-api.ap-southeast-1.amazonaws.com/> as shown above under endpoint to see that its up on aws.

**Curl response from aws**

![A picture containing text, screenshot, software Description automatically generated](media/4c61ce6a1520369ac61fd4e87e675e36.png)

StatusCode : 200

StatusDescription : OK

Content : {

"message": "Go Serverless v3.0! Your function executed successfully!",

"input": {

"version": "2.0",

"routeKey": "GET /",

"rawPath": "/",

"rawQueryString": "",

"headers": {

...

RawContent : HTTP/1.1 200 OK

Connection: keep-alive

Apigw-Requestid: GF2EYiEXSQ0EJXQ=

Content-Length: 1244

Content-Type: text/plain; charset=utf-8

Date: Tue, 06 Jun 2023 10:00:21 GMT

{

"message": "Go Ser...

Forms : {}

Headers : {[Connection, keep-alive], [Apigw-Requestid, GF2EYiEXSQ0EJXQ=], [Content-Length, 1244], [Content-Type,

text/plain; charset=utf-8]...}

Images : {}

InputFields : {}

Links : {}

ParsedHtml : mshtml.HTMLDocumentClass

RawContentLength : 1244

# Step 6 – now that code is up and running on AWS- we create the CICD pipeline USING GitHub Actions to support changes.

1.  ![A screenshot of a computer program Description automatically generated with medium confidence](media/71e980ef87615997a05b9854c3efb0dd.png)

    Create .github/workflow folder in root

    Create main.yml file in .github\\workflows

    ![A picture containing text, font, screenshot Description automatically generated](media/838132de38c36ccd5997d7c1244d266c.png)

| name: CICD for Serverless Application run-name: \${{ github.actor }} is doing CICD for Serverless Application  on:  push:  branches: [ main, "\*"]  jobs:  pre-deploy:  runs-on: ubuntu-latest  steps:  - run: echo "🎉 The job was automatically triggered by a \${{ github.event_name }} event."  - run: echo "🐧 This job is now running on a \${{ runner.os }} server hosted by GitHub!"  - run: echo "🔎 The name of your branch is \${{ github.ref }} and your repository is \${{ github.repository }}."   install-dependencies:  runs-on: ubuntu-latest  needs: pre-deploy  steps:  - name: Check out repository code  uses: actions/checkout@v3  - name: Run Installation of Dependencies Commands  run: npm install   deploy:  name: deploy  runs-on: ubuntu-latest  needs: install-dependencies  strategy:  matrix:  node-version: [18.x]  steps:  - uses: actions/checkout@v3  - name: Use Node.js \${{ matrix.node-version }}  uses: actions/setup-node@v3  with:  node-version: \${{ matrix.node-version }}  - run: npm ci  - name: serverless deploy  uses: serverless/github-action@v3.2  with:  args: deploy  env:  AWS_ACCESS_KEY_ID: \${{ secrets.AWS_ACCESS_KEY_ID }}  AWS_SECRET_ACCESS_KEY: \${{ secrets.AWS_SECRET_ACCESS_KEY }}  |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Workflow Syntax **name**: The name of the workflow. **on**: The type of event that can run the workflow. This workflow will only run when there is a git push to either the main or other branch. **jobs**: A workflow consists of one or more jobs. Jobs run in parallel unless a *needs* keyword is used. Each job runs in a runner environment specified by *runs-on*. **steps**: A sequence of tasks to be carried out. **uses**: Selects an action to run as part of a step in your job. An action is a reusable unit of code. **with**: A map of input parameters. **run**: Runs command line programs. **env**: Set the environment variables.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |

Reference : [serverless/github-action: A Github Action for deploying with the Serverless Framework](https://github.com/serverless/github-action)

\#ensure the passwords are entered in github manager from AWS IAM

If you cant find it- create new keys if you are allowed on AWS IAM

Or search in your respective local drives

<https://docs.aws.amazon.com/sdkref/latest/guide/file-location.html>

AWS_ACCESS_KEY_ID: \${{ secrets.AWS_ACCESS_KEY_ID }}

AWS_SECRET_ACCESS_KEY: \${{ secrets.AWS_SECRET_ACCESS_KEY }}

%USERPROFILE%\\.aws\\config

**You will need this in the steps below**

# Step 7 Add secrets to Github Secrets – ensure you are in git hub repo on github

Enter your aws keys here so that github can communicate with AWS

![A screenshot of a computer Description automatically generated with medium confidence](media/0c9532d1d86a3b0559d0dba400507fe6.png)

| ![A screenshot of a computer Description automatically generated with low confidence](media/34d63d28658f4525559bcd918a99a859.png) | ![A screenshot of a computer Description automatically generated with low confidence](media/6c462fe07ee773402d5e3f1b98af72a9.png) ![](media/d8d9211ee678360d7f47f60981572c03.png) |
|-----------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|

# Step 8: push changes to Github to start the workflow

\$ git add .

\$ git commit -m “second commit”

\$ git push

\*\*\*\*ensure node js folder is installed and node_modules is included in the .gitignore file

![](media/f504e6e5532ad12c7ed77b137917877e.png)

![](media/da676c337c4aad8087abc6e1f7ec33fd.png)

## Workflow started- check on Github Actions on Github as shown below

![A screenshot of a computer Description automatically generated with medium confidence](media/c75ae00f0f790dbdec866773358a56ea.png)

![A screenshot of a computer Description automatically generated with medium confidence](media/0323378f8ec8de229c2f5f63a2c8fdb7.png)

# Step 9 : add a secret in AWS secret manager

The goal of this exercise is to **Store some information using Secret Management on AWS, then get the information as part of the pipeline.**

![A screenshot of a computer Description automatically generated with medium confidence](media/fd8bdb6ac0aae1e807c797609d4a9ab2.png)

![A screenshot of a computer Description automatically generated with medium confidence](media/efee4a849640103c26933df409138a7a.png)

# Step 10- retrieve the secret from the AWS Secrets as part of the CICD pipeline

Add a new job **retrieve-secret** to

.github/workflows/main.yml to retrieve the stored secret **TAUFIQ_SECRET**

from AWS Secrets Manager and inject into environment variables

![A screenshot of a computer program Description automatically generated with medium confidence](media/9147a47c660d48b41fc64f7b16778894.png)

![A picture containing text, screenshot, software, multimedia software Description automatically generated](media/ab7d0d926d6e7b4caa12e98b01419690.png)

Last 2 lines will print the secrets

**secrets**:

-   List of secret to be retrieved.
-   Examples:
    -   To retrieve a single secret, use secrets: my_secret_1
    -   To retrieve multiple secrets, use:
    -   secrets: \|
    -   my_secret_1
    -   my_secret_2
    -   To retrieve "all secrets having names that contain dev" or "begin with app1/dev/", use:
    -   secrets: \|
    -   \*dev\*

        app1/dev/\*

# STEP 11-Push the changes to GitHub to start the workflow

![A screenshot of a computer Description automatically generated with medium confidence](media/590e2ef6c31f9bc51a16153d9838ec1d.png)
