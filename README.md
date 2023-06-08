# 3.13_assignment-homework
assignment submission.
added aws secrets
### Brief

### Brief

The objective of this assignment is to set up a continuous integration
and continuous deployment (CI/CD) pipeline for a Node.js application
that is deployed on a serverless platform with Secret Management in
placed!.

Instructions:

1.  Create a new Node.js **application** using the Express framework.

2.  Set up **automatic testing** for the application using a testing
    framework such as Jest or Mocha.

3.  Create **new branch** on your existing repository.

4.  Set up a CI/CD pipeline using a tool such as Github Action, Jenkins,
    Travis CI, or CircleCI.

5.  Configure the pipeline to automatically build and test the code
    whenever changes are pushed to the code repository.

6.  Deploy the application to a serverless platform such as AWS Lambda
    or Google Cloud Functions.

7.  **Store some information using Secret Management on AWS, then get
    the information as part of the pipeline.**

8.  Configure the pipeline to automatically deploy the code to the
    serverless platform whenever changes are pushed to the code
    repository and all tests pass.

9.  Write a documentation explaining the steps you have done, including
    the tools and services used.

Deliverables:

-   The Node.js application with automatic testing set up

-   Code repository with the CI/CD pipeline configured

-   Documentation explaining the steps taken to set up the pipeline.

# 

# 

# Step 0 -- create github repository
![Picture1](https://github.com/muhammedtaufiq/3.13_assignment/assets/24953052/6f21ae52-7e35-443e-a638-db62fba82977)


# Step 1 -- create a local folder on your local machine

We will clone into here at the next step

![Picture2](https://github.com/muhammedtaufiq/3.13_assignment/assets/24953052/fd9c874e-4a03-444d-a128-5f4e4d61060e)


# Step 2 -- Clone repo to local host-folder created at the step above

a)  Open terminal in the folder above
![Picture3](https://github.com/muhammedtaufiq/3.13_assignment/assets/24953052/9e31e302-89ac-4d7b-bc3c-113a65417817)


b)  \$ git clone https://github.com/muhammedtaufiq/3.13_assignment.git

![Picture4](https://github.com/muhammedtaufiq/3.13_assignment/assets/24953052/a8cd5dc6-c6be-4c93-873b-8324c69fc792)
![Picture5](https://github.com/muhammedtaufiq/3.13_assignment/assets/24953052/a0507751-35af-446e-b20f-5bbcff68bc0a)


#ensure you cd into the git project root

# Step 3 -- creating index.js file to hold my application
![Picture6](https://github.com/muhammedtaufiq/3.13_assignment/assets/24953052/8d880332-8140-47ba-bba3-1168b1087453)


module.exports.handler = async (event) =\> {

return {

statusCode: 200,

body: JSON.stringify(

{

message: \"Go Serverless v3.0! Your function executed successfully!\",

input: event,

},

null,

2

),

};

};

# Step 4 create serverless .yml to contain instructions for serverless

Ref: [Serverless Framework
Services](https://www.serverless.com/framework/docs/providers/aws/guide/services/#:~:text=When%20you%20deploy%20a%20service%2C%20all%20functions%2C%20events,to%20dev%20stage%20and%20us-east-1%20region%20on%20AWS.)

Template :

![Picture7](https://github.com/muhammedtaufiq/3.13_assignment/assets/24953052/f4ed3f08-aa5e-411d-b3f8-5ced1611f117)


# Step 5 -- install and deploy serverless application

**Install express**

*\$npm install -g express*
![Picture8](https://github.com/muhammedtaufiq/3.13_assignment/assets/24953052/24938558-7498-4e69-9bad-041d8a0ba815)



**Create json file**

*\$ npm init*
![Picture9](https://github.com/muhammedtaufiq/3.13_assignment/assets/24953052/7dc6bb4b-b09a-44c0-ab13-e09eab185edd)


![Picture10](https://github.com/muhammedtaufiq/3.13_assignment/assets/24953052/17abd9b9-77f2-40b2-9af8-5c82fc07beb8)


*\$ npm install*


![Picture11](https://github.com/muhammedtaufiq/3.13_assignment/assets/24953052/253af680-5950-428a-b2e3-f5037a832487)

Do ensure serverless offline plugin is installed:\

![Picture12](https://github.com/muhammedtaufiq/3.13_assignment/assets/24953052/8a539f76-3df6-44a8-81b9-83f67efc2086)

**Deploying serverless**

*\$ serverless deploy*
![Picture13](https://github.com/muhammedtaufiq/3.13_assignment/assets/24953052/bde589bd-561e-489b-b523-9b8248a619fc)


**Acquire content from serverless to check its running**

You can now curl
<https://m1aoenl1cj.execute-api.ap-southeast-1.amazonaws.com/> as shown
above under endpoint to see that its up on aws.

**Curl response from aws**
![Picture14](https://github.com/muhammedtaufiq/3.13_assignment/assets/24953052/01d6eb40-e027-4955-96b3-5bb6dcfd20bf)


StatusCode : 200

StatusDescription : OK

Content : {

\"message\": \"Go Serverless v3.0! Your function executed
successfully!\",

\"input\": {

\"version\": \"2.0\",

\"routeKey\": \"GET /\",

\"rawPath\": \"/\",

\"rawQueryString\": \"\",

\"headers\": {

\...

RawContent : HTTP/1.1 200 OK

Connection: keep-alive

Apigw-Requestid: GF2EYiEXSQ0EJXQ=

Content-Length: 1244

Content-Type: text/plain; charset=utf-8

Date: Tue, 06 Jun 2023 10:00:21 GMT

{

\"message\": \"Go Ser\...

Forms : {}

Headers : {\[Connection, keep-alive\], \[Apigw-Requestid,
GF2EYiEXSQ0EJXQ=\], \[Content-Length, 1244\], \[Content-Type,

text/plain; charset=utf-8\]\...}

Images : {}

InputFields : {}

Links : {}

ParsedHtml : mshtml.HTMLDocumentClass

RawContentLength : 1244

# Step 6 -- now that code is up and running on AWS- we create the CICD pipeline USING GitHub Actions to support changes.

a.  ![Picture15](https://github.com/muhammedtaufiq/3.13_assignment/assets/24953052/de9985f4-fc59-4b58-85e9-16da50d3ca4a)


> Create .github/workflow folder in root
>
> Create main.yml file in .github\\workflows
>
> ![Picture16](https://github.com/muhammedtaufiq/3.13_assignment/assets/24953052/71d196b8-7422-4cd7-9fc6-98741ce9fe8f)


+-----------------------------------------------------------------------+
| name: CICD for Serverless Application                                 |
|                                                                       |
| run-name: \${{ github.actor }} is doing CICD for Serverless           |
| Application                                                           |
|                                                                       |
| on:                                                                   |
|                                                                       |
|   push:                                                               |
|                                                                       |
|     branches:  \[ main, \"\*\"\]                                      |
|                                                                       |
| jobs:                                                                 |
|                                                                       |
|   pre-deploy:                                                         |
|                                                                       |
|     runs-on: ubuntu-latest                                            |
|                                                                       |
|     steps:                                                            |
|                                                                       |
|       - run: echo \"🎉 The job was automatically triggered by a \${{  |
| github.event_name }} event.\"                                         |
|                                                                       |
|       - run: echo \"🐧 This job is now running on a \${{ runner.os }} |
| server hosted by GitHub!\"                                            |
|                                                                       |
|       - run: echo \"🔎 The name of your branch is \${{ github.ref }}  |
| and your repository is \${{ github.repository }}.\"                   |
|                                                                       |
|   install-dependencies:                                               |
|                                                                       |
|     runs-on: ubuntu-latest                                            |
|                                                                       |
|     needs: pre-deploy                                                 |
|                                                                       |
|     steps:                                                            |
|                                                                       |
|       - name: Check out repository code                               |
|                                                                       |
|         uses: actions/checkout@v3                                     |
|                                                                       |
|       - name: Run Installation of Dependencies Commands               |
|                                                                       |
|         run: npm install                                              |
|                                                                       |
|   deploy:                                                             |
|                                                                       |
|     name: deploy                                                      |
|                                                                       |
|     runs-on: ubuntu-latest                                            |
|                                                                       |
|     needs: install-dependencies                                       |
|                                                                       |
|     strategy:                                                         |
|                                                                       |
|       matrix:                                                         |
|                                                                       |
|         node-version: \[18.x\]                                        |
|                                                                       |
|     steps:                                                            |
|                                                                       |
|     - uses: actions/checkout@v3                                       |
|                                                                       |
|     - name: Use Node.js \${{ matrix.node-version }}                   |
|                                                                       |
|       uses: actions/setup-node@v3                                     |
|                                                                       |
|       with:                                                           |
|                                                                       |
|         node-version: \${{ matrix.node-version }}                     |
|                                                                       |
|     - run: npm ci                                                     |
|                                                                       |
|     - name: serverless deploy                                         |
|                                                                       |
|       uses: serverless/github-action@v3.2                             |
|                                                                       |
|       with:                                                           |
|                                                                       |
|         args: deploy                                                  |
|                                                                       |
|       env:                                                            |
|                                                                       |
|         AWS_ACCESS_KEY_ID: \${{ secrets.AWS_ACCESS_KEY_ID }}          |
|                                                                       |
|         AWS_SECRET_ACCESS_KEY: \${{ secrets.AWS_SECRET_ACCESS_KEY }}  |
+=======================================================================+
| ### Workflow Syntax                                                   |
|                                                                       |
| **name**: The name of the workflow.                                   |
|                                                                       |
| **on**: The type of event that can run the workflow. This workflow    |
| will only run when there is a git push to either the main or other    |
| branch.                                                               |
|                                                                       |
| **jobs**: A workflow consists of one or more jobs. Jobs run in        |
| parallel unless a ***needs*** keyword is used. Each job runs in a     |
| runner environment specified by ***runs-on***.                        |
|                                                                       |
| **steps**: A sequence of tasks to be carried out.                     |
|                                                                       |
| **uses**: Selects an action to run as part of a step in your job. An  |
| action is a reusable unit of code.                                    |
|                                                                       |
| **with**: A map of input parameters.                                  |
|                                                                       |
| **run**: Runs command line programs.                                  |
|                                                                       |
| **env**: Set the environment variables.                               |
+-----------------------------------------------------------------------+

Reference : [serverless/github-action: A Github Action for deploying
with the Serverless
Framework](https://github.com/serverless/github-action)

#ensure the passwords are entered in github manager from AWS IAM

If you cant find it- create new keys if you are allowed on AWS IAM

Or search in your respective local drives

<https://docs.aws.amazon.com/sdkref/latest/guide/file-location.html>

        AWS_ACCESS_KEY_ID: \${{ secrets.AWS_ACCESS_KEY_ID }}

        AWS_SECRET_ACCESS_KEY: \${{ secrets.AWS_SECRET_ACCESS_KEY }}

%USERPROFILE%\\.aws\\config

> **You will need this in the steps below**

# Step 7 Add secrets to Github Secrets -- ensure you are in git hub repo on github

Enter your aws keys here so that github can communicate with AWS
![Picture17](https://github.com/muhammedtaufiq/3.13_assignment/assets/24953052/cdd8d56b-de99-4f19-83f4-53320b020ff4)


![Picture18](https://github.com/muhammedtaufiq/3.13_assignment/assets/24953052/ef442805-463c-4be3-8211-67c508138d9e)
![Picture19](https://github.com/muhammedtaufiq/3.13_assignment/assets/24953052/061ac685-df40-4305-92ee-658f97b11c74)
![Picture20](https://github.com/muhammedtaufiq/3.13_assignment/assets/24953052/1941299e-5f91-40a7-b4d2-cbce45c640d0)

# Step 8: push changes to Github to start the workflow

\$ git add .

\$ git commit -m "second commit"

\$ git push

\*\*\*\*ensure node js folder is installed and node_modules is included
in the .gitignore file
![Picture21](https://github.com/muhammedtaufiq/3.13_assignment/assets/24953052/38a8afd6-0cdb-4800-a30b-abdb39a918ba)
![Picture22](https://github.com/muhammedtaufiq/3.13_assignment/assets/24953052/a4c03923-08ca-4873-b8ed-c6479a21f996)



## Workflow started- check on Github Actions on Github as shown below
![Picture23](https://github.com/muhammedtaufiq/3.13_assignment/assets/24953052/497e459a-8643-4728-bf5b-041c663bb0cc)


![Picture24](https://github.com/muhammedtaufiq/3.13_assignment/assets/24953052/77a55d25-e35d-4369-9924-b1e2d0e3e177)



# Step 9 : add a secret in AWS secret manager

The goal of this exercise is to **Store some information using Secret
Management on AWS, then get the information as part of the pipeline.**
![Picture25](https://github.com/muhammedtaufiq/3.13_assignment/assets/24953052/c11e1ce6-bd8f-4627-bd78-fbde056e250e)
![Picture26](https://github.com/muhammedtaufiq/3.13_assignment/assets/24953052/a3d6d318-8c81-49e1-a0b5-eeeb10a1e3eb)


# Step 10- retrieve the secret from the AWS Secrets as part of the CICD pipeline

Add a new job **retrieve-secret** to

.github/workflows/main.yml to retrieve the stored
secret ***TAUFIQ_SECRET*** 

from AWS Secrets Manager and inject into environment variables
![Picture27](https://github.com/muhammedtaufiq/3.13_assignment/assets/24953052/618cd1b6-1189-443a-9b42-98f019d95093)
![Picture28](https://github.com/muhammedtaufiq/3.13_assignment/assets/24953052/7b0f5dc7-7734-4ed3-8dca-0be51f88b67d)

Last 2 lines will print the secrets

**secrets**:

-   List of secret to be retrieved.

-   Examples:

    -   To retrieve a single secret, use secrets: my_secret_1

    -   To retrieve multiple secrets, use:

    -   secrets: \|

    -   my_secret_1

    -   my_secret_2

    -   To retrieve \"all secrets having names that contain dev\" or
        \"begin with app1/dev/\", use:

    -   secrets: \|

    -   \*dev\*

> app1/dev/\*

# STEP 11-Push the changes to GitHub to start the workflow
![Picture29](https://github.com/muhammedtaufiq/3.13_assignment/assets/24953052/b130f0f5-14f4-4ea8-95df-c26fe22bfc23)


