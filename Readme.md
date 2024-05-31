# Jenkins-Github-Pipeline

Jenkins-Github-Pipeline is a Jenkinsfile using Declarative Syntax. It downloads the git repository [SimpleAPITestInterface](https://github.com/rathorsunpreet/SimpleAPITestInterface) and waits for user input within a specified time frame, after which test cases are executed.

There are three outcomes that can occur, namely:
* **User input is provided**: Then test execution continues as normal.
* **User aborts the job**: Then the job is simply aborted and no execution of test cases takes place.
* **User is unable to provide input**: User Input is expected within 1 minute, if the user is unable to provide an input, then the default "all report" is used.

If keyword "report" is present during input, then a special stage within the pipeline is executed which creates a zip file, named "HTML_Report.zip" at the project root.

## Requirements
* [Jenkins](https://www.jenkins.io/)
* [NodeJS Jenkins Plugin](https://plugins.jenkins.io/nodejs/)
* [Pipeline Utility Steps Plugin](https://plugins.jenkins.io/pipeline-utility-steps/)
* An account that has admin priviledges or an account that can get the script approved. ![Script Approval Screen](https://github.com/rathorsunpreet/Jenkins-Github-Pipeline/blob/master/Images/Script_Approval_2.PNG "Script Approval Screen")

## Installation

1. Create a new Pipeline job.
2. Under Pipeline -> Definition, make sure it is "Pipeline Script".
3. Under the Script section, copy and paste the Jenkinsfile.
4. Uncheck "Use Groovy Sandbox".
5. Click on "Apply".
6. Click on Approve Script. ![Script Approval Configuration Pipeline Screen](https://github.com/rathorsunpreet/Jenkins-Github-Pipeline/blob/master/Images/Script_Approval.PNG "Script Approval Configuration Pipeline Screen")
7. Click on "Save".  

## Usage
Click on "Build Now".

## License

[MIT](https://choosealicense.com/licenses/mit/)