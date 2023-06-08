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

![A screenshot of a computer Description automatically generated with
medium confidence](media/picture1.png){width="6.268055555555556in"
height="6.020833333333333in"}

# Step 1 -- create a local folder on your local machine

We will clone into here at the next step
![Picture1](https://github.com/muhammedtaufiq/3.13_assignment/assets/24953052/22f2ff24-dacb-4204-baac-7dc849ee1281)


# Step 2 -- Clone repo to local host-folder created at the step above

a)  Open terminal in the folder above

![A screen shot of a computer Description automatically generated with
medium confidence](media/image3.png){width="6.268055555555556in"
height="1.2979166666666666in"}

b)  \$ git clone https://github.com/muhammedtaufiq/3.13_assignment.git

  ---------------------------------------------------------------------------------------------------------------
  ![A screenshot of a computer Description automatically      ![](media/image5.png){width="4.164797681539808in"
  generated with medium                                       height="1.4507108486439195in"}
  confidence](media/image4.png){width="1.816634951881015in"   
  height="1.1318088363954506in"}                              
  ----------------------------------------------------------- ---------------------------------------------------

  ---------------------------------------------------------------------------------------------------------------

#ensure you cd into the git project root

# Step 3 -- creating index.js file to hold my application

![A screen shot of a computer Description automatically generated with
medium confidence](media/image6.png){width="4.156405293088364in"
height="1.297668416447944in"}

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

![A screenshot of a computer Description automatically
generated](media/image7.png){width="4.211499343832021in"
height="4.031859142607174in"}

# Step 5 -- install and deploy serverless application

**Install express**

*\$npm install -g express*

![A screen shot of a computer Description automatically generated with
medium confidence](media/image8.png){width="4.863992782152231in"
height="0.8034798775153106in"}

**Create json file**

*\$ npm init*

![A screenshot of a computer Description automatically generated with
medium confidence](media/image9.png){width="4.416174540682415in"
height="1.9453477690288714in"}

![A screen shot of a computer Description automatically generated with
low confidence](media/image10.png){width="3.021255468066492in"
height="1.6356452318460193in"}Package.json appears

*\$ npm install*

![A black screen with white text Description automatically generated
with low confidence](media/image11.png){width="6.268055555555556in"
height="0.9291666666666667in"}

Do ensure serverless offline plugin is installed:\
![](media/image12.png){width="6.268055555555556in"
height="0.42291666666666666in"}

**Deploying serverless**

*\$ serverless deploy*

![A screen shot of a computer program Description automatically
generated with low
confidence](media/image13.png){width="6.268055555555556in"
height="1.7326388888888888in"}

**Acquire content from serverless to check its running**

You can now curl
<https://m1aoenl1cj.execute-api.ap-southeast-1.amazonaws.com/> as shown
above under endpoint to see that its up on aws.

**Curl response from aws**

![A picture containing text, screenshot, software Description
automatically generated](media/image14.png){width="6.268055555555556in"
height="4.047916666666667in"}

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

a.  ![A screenshot of a computer program Description automatically
    generated with medium
    confidence](media/image15.png){width="2.906655730533683in"
    height="1.375191382327209in"}

> Create .github/workflow folder in root
>
> Create main.yml file in .github\\workflows
>
> ![A picture containing text, font, screenshot Description
> automatically
> generated](media/image16.png){width="2.958746719160105in"
> height="0.6146686351706037in"}

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

![A screenshot of a computer Description automatically generated with
medium confidence](media/image17.png){width="4.9463943569553805in"
height="2.5701957567804024in"}

+-------------------------------+--------------------------------------+
| ![A screenshot of a computer  | ![A screenshot of a computer         |
| Description automatically     | Description automatically generated  |
| generated with low            | with low                             |
| c                             | confidence](media/imag               |
| onfidence](media/image18.png) | e19.png){width="2.590400262467192in" |
| {width="2.6255708661417323in" | height="3.12708552055993in"}         |
| h                             |                                      |
| eight="2.7363549868766404in"} | ![](media/imag                       |
|                               | e20.png){width="3.306228127734033in" |
|                               | height="2.2340660542432196in"}       |
+===============================+======================================+
+-------------------------------+--------------------------------------+

# Step 8: push changes to Github to start the workflow

\$ git add .

\$ git commit -m "second commit"

\$ git push

\*\*\*\*ensure node js folder is installed and node_modules is included
in the .gitignore file

![](media/image21.png){width="6.268055555555556in"
height="0.1423611111111111in"}

![](media/image22.png){width="1.3439370078740158in"
height="0.39588910761154855in"}

## Workflow started- check on Github Actions on Github as shown below

![A screenshot of a computer Description automatically generated with
medium confidence](media/image23.png){width="2.9551859142607175in"
height="1.8596784776902888in"}

![A screenshot of a computer Description automatically generated with
medium confidence](media/image24.png){width="4.6077329396325455in"
height="1.5391447944007in"}

# Step 9 : add a secret in AWS secret manager

The goal of this exercise is to **Store some information using Secret
Management on AWS, then get the information as part of the pipeline.**

![A screenshot of a computer Description automatically generated with
medium confidence](media/image25.png){width="4.023630796150481in"
height="2.0599595363079617in"}

![A screenshot of a computer Description automatically generated with
medium confidence](media/image26.png){width="6.268055555555556in"
height="3.3979166666666667in"}

# Step 10- retrieve the secret from the AWS Secrets as part of the CICD pipeline

Add a new job **retrieve-secret** to

.github/workflows/main.yml to retrieve the stored
secret ***TAUFIQ_SECRET*** 

from AWS Secrets Manager and inject into environment variables

![A screenshot of a computer program Description automatically generated
with medium confidence](media/image27.png){width="6.268055555555556in"
height="3.8270833333333334in"}

![A picture containing text, screenshot, software, multimedia software
Description automatically
generated](media/image28.png){width="6.268055555555556in"
height="2.5277777777777777in"}

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

![A screenshot of a computer Description automatically generated with
medium confidence](media/image29.png){width="6.268055555555556in"
height="2.475in"}
