# Cypress Automation

This a guideline for creating and developing with Cypress using the Cypress V5-UI Automation Testing + API Testing + Frameworks course by Gianni Bruno.

**Setting up your environment**
*Section 2*

**Browsers:**
1. Install Chrome and Firefox browsers, if already installed make sure the browsers are up to date. Install NodeJS:
1. Open : [NodeJs](https://nodejs.org/en/download/)
2. Select macOS installer and download should start immediately
3. run the installer
4. This link provides instructions on installing Cypress via the CLI : [Cypress CLI](https://docs.cypress.io/guides/getting-started/installing-cypress.html#Installing)
5. Open terminal and run `node --version` to verify that NodeJs is installed

**Install Gitbash:**
This will allow you to push your code the the repository
1. Open: [Gitbash](https://git-scm.com/downloads)
2. Select and download the MacOS X installer
3. Open terminal and run `git --version` to verify Gitbash is installed

**Install Visual Studio Code:**
1. Open: Visual Studio Code
2. Select and download MacOS installer
3. Open terminal and run code --version to verify Gitbash is installed

***Create folder and setup VSC:***
*Create folder in desired directory and with desired title for your test framework*
2. Open [visual studio code](https://code.visualstudio.com/download)
3. Select File Open Select folder you created in step 1
4. Open Terminal in VSC
5. Make sure that you have bash selected :
<img src="resources/bash.png" alt="Bash">
7. If bash is not selected click the drop down menu in the image above, select ‘Select Default Shell’ and click bash in the menu at the top of the window:
<img src="resources/bashmenu.png" alt="Bash Dropdown">
<img src="resources/shelltypes.png" alt="Shell Types">

**Setting up Cypress**
Create package.json:
1. Open VSC and open the desired folder
2. Open terminal and make sure you are using the bash shell
3. run `npm init` - this will create the package.json file
4. you will see your package name (title of your folder) display press *Enter*
5. your ‘version’ will be displayed press *Enter*
6. then you will see 'description: ' if you want to add a description to the package you can enter it now. Then press *Enter* 
7. ‘entry point' will be displayed press *Enter*
9. test command will be displayed press *Enter*
10. git repository will be displayed press *Enter*
11. git repository will be displayed press *Enter*
12. author will be displayed [add name if you like] press *Enter*
13. license will be displayed press *Enter*
14. Your package.json file should populate and ask “Is this OK?” if ok press *Enter*

**Download Cypress:**
1. run `npm install cypress --save-dev`
2. to verify cypress has been installed make sure you see your node_modules folder in directory
3.<img src="resources/nodemodules.png" alt="node_modules">

*Open Cypress:*
1. open terminal
2. run ./node_modules/.bin/cypress open
3. this will add a list of demo tests in cypress which is not required but it is helpful
4. If you want to remove the tests to clean up the test suite navigate to integration examples in your test folder and delete it
5. After running the command in step 2 you will see a the cypress test runner populate as well.
6. Section 4: Lecture 15 in the course will break down the components of the cypress test runner

**Mocha:**
When setting up your test you will notice the describe() and it() functions as shown below. These functions are pre bundled with Mocha describe() : used to group tests in Mocha [multiple tests]
it() : used to describe each test case listed in the describe block [individual tests]
``` 
///<reference types="Cypress" />
describe("Test for homegpage",() => {
    it("Verify links in navigation bar", () => {
}) });
```
**Triggering Tests via Command Line**
*Section 16*
Running tests in ‘headless’ mode allows you to run tests without the dashboard or test runner / dashboard running
1. run `./node_modules/.bin/cypress run` 
2. This will instantly start your test suite

Cypress Command Line Options: [CLI Options Guide](https://docs.cypress.io/guides/references/configuration.html#Options)
The CLI Options Guide line about lists options to run the headless test suites via 
specific browser `--browser`, `-b`
specific environment `--env`, `-e`
`--headed` will allow you run with browser open

**Overriding Default Settings**
*Section 45*
This section is a list of default settings that you may need to adjust. 

- set“chromeWebSecurity” to false in the cypress.json file.
<img src="chromewebsecurity.png" alt="Chrome Web Security">
purpose : 
	- Display insecure content
	- Navigate to any superdomain without cross-origin 	errors
	- Access cross-origin iframes that are embedded in you application

- defaultCommandTimeout
- execTimeout 
- pageLoadTimeout
- requestTimeout

**Ignoring test files**
This functionality is helpful when you have tests that you do not want to delete but you may want to exclude from running with the suite.
 ```
 {
"ignoreTestFiles": "*"
}
```
you can use * as a wild card to include all tests within a certain constraint. For example if you wanted to exclude any test that ends in .js you would type ``*.js``.
``**/folder/*`` would ignore files in a specific folder

**Connecting to Cypress Dashboard**
*Section 53: Cypress Dashboard*
1. run `./node_modules/.bin/cypress open`
2. Go to test runner
3. Click ‘Log in’
4. Log into account via web browser
5. Navigate back to test runner
6. Click ‘Runs’ in top right hand corner
7. Fill out fields and select ‘Set up project’
8. Next you will see a page populate with the ‘projectId’ and ‘record key’
9.<img src="resources/dashboardproject.png" alt="Dashboard project id">
 10. Navigate back to project and open the cypress.json file. You should see your project ID listed
11. Now to run test with cypress you should run `./node_modules/.bin/cypress run --record --key <record key value>`

**NPM Scripts & NPX**
**npx**
NPX allows you to run a command from node_modules/.bin instead of having to run `./node_modules/.bin/cypress` before every command. You can use `npx cypress run` instead. 
*npx installation* : run `npm install -g npx`

**npm scripts**
these scripts allow you to create scripts to trigger tests with simple commands. They live in the package.json file under ‘scripts’
```
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "cypress-open": "./node_modules/.bin/cypress open",
    "triggerAllTests-headless": "npx cypress run",
    "triggerAllTests-chrome": "npx cypress run --browser chrome",
    "triggerAllTests-dashboard": "cypress run --record --key fbe08fe5-
31fb-4cb5-ade4-5d18a351a24a",
    "junit-merge": "npx junit-merge -d cypress/results/junit -o cypress
/results/junit/results.xml",
    "delete-junit-report": "rm -rf cypress/results/junit/results.xml",
    "delete-results": "rm -rf cypress/results/* || true",
    "mochawesome-merge": "npx mochawesome-merge cypress/results
/mochawesome/*.json > mochawesome.json && npx marge mochawesome.json",
    "delete-mochawesome-report": "rm -rf mochawesome-report/* || true",
    "cypress-regression-pack": "npm run delete-results && npm run
delete-mochawesome-report && npm run triggerAllTests-headless && npm
run mochawesome-merge"
},
```
 To trigger script run `npm run <script name>` i.e. `npm run cypress-open`
 
 
**Reporting**
section 55
[Cypress-Multiple-Reporters](https://docs.cypress.io/guides/tooling/reporters.html#Multiple-reporters)
Packages : These are all of the packages that you need to install for mocha
1. Mocha
`npm install mocha --save-dev`
2. cypress-multi-reporters
`npm install cypress-multi-reporters --save-dev`
3. mochawesome
`npm install mochawesome --save-dev`
4. mochawesome-merge
`npm install mochawesome-merge --save-dev`
5. mochawesome-report-generator
`npm install mochawesome-report-generator --save-dev`
7. You can install 3, 4, & 5 simultaneously
`npm install --save-dev mochawesome mochawesome-merge`

**mochawesome-report-generator**
Add reporter settings to the cypress.json file
```
    "reporter": "cypress-multi-reporters",
    "reporterOptions": {
    "configFile": "reporter-config.json"
    }
```
Add the following code to reporter-config.json
```
     {
    "reporterEnabled": "spec, cypress-multi-reporters",
    "mochaJunitReporterReporterOptions": {
      "mochaFile": "cypress/results/junit/results-[hash].xml"
    },
    "reporterOptions": {
      "reporterEnabled": "mochawesome",
      "mochawesomeReporterOptions": {
        "reportDir": "cypress/results/mochawesome",
        "quiet": true,
        "overwrite": false,
        "json": true
  }
 } 
}
```

*Add the following code to the package.json scripts*
To trigger test run `npm run <script name>`
*Run and merge mochawesome reports script*: 
```
"mochawesome-merge": "npx mochawesome-merge cypress/results/mochawesome/*.json > mochawesome.json && npx
marge mochawesome.json"
```
*Delete reports within the mochawesome-report folder:*
```
"delete-mochawesome-report": "rm -rf mochawesome-report/* || true"
```
*Delete previous reports and run and merge mochawesome reports:*
```
"cypress-regression-pack": "npm run delete-results && npm run delete-mochawesome-report && npm run
triggerAllTests-headless && npm run mochawesome-merge"
```

**Configuration Files**
Section 56
Configuration files allow you to execute tests and specify the enviornment (stage, pre-prod, and prod) that you want to execute the test in. 

Multiple Configuration Files Setup:
1. Create a folder named config in the base directory
2. Create config file for desired environment [stage.json, dev.json, prod.json...etc]
3. Define the base url and environment for the file
4. ``{ "baseUrl" : "https://www.baseurl.com", "env" : { "name": "production" } }``
5. now we are going to add logic that will allow cypress to read values stored in the custom configuration files. Add the below logic to the last line in the index.js file in the plugins folder.
6. 
```
// promisified fs module const fs = require('fs-extra') const path = require('path')
  function getConfigurationByFile (file) {
    const pathToConfigFile = path.resolve('cypress', 'config',
  `${file}.json`)
    if(!fs.existsSync(pathToConfigFile)){
      console.log('No custom config file found. ')
      return {};
}
    return fs.readJson(pathToConfigFile)
  }
  // plugins file
  module.exports = (on, config) => {
    // accept a configFile value or use development by default
    const file = config.env.configFile
    return getConfigurationByFile(file)
  }
 ```
 
7. Command to open cypress using the configuration file : `npx cypress open --env configFile=<name>` 
If you wanted to run the test within the stage environment enter : 
`run npx cypress open --env configFile=stage` 
This will change the baseUrl settings in cypress.
