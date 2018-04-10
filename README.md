# Learning JS best practices

## Syntax
**--Consistency is key--**

### Use Strict mode
*   'use strict'; 
    - Will help in finding errors in development fast
    - Avoid JS from helping us

### Linting

Always use linting tools like
*   JS Hint
    -   npm install -g jshint
    -   install js hint in editor
    -   create .jshintrc for configuration in root folder and add necessary configs as JSON
        {
            "eqeqeq": true,
            "esversion": 6
        }
*   ESLint

### Equality

*   Use === as default
*   To see if variable exists, use typeof undefined 
    -   if( typeof x !== 'undefined')

### Variables
*   Be aware of **hoisting**
*   **Try to follow below step:**
    - Variable frist
    - Functions next
    - Run code

### Functions
*   Two types of functions
    -   Declaration
    -   Expression 


## Behavior

### Global variables
*   Declare variable without var, let, const will cause it to be leaked into the global scope and be created there, which is not good. 





## Async Pattern





## Production

### npm Settings
*   Set save to default
    -   npm config set save-exact=true // It saves the package and version number in package.json. This is future proof, so that when a new version of package releases, it doesn't automatically use it.
    -   npm config set save=true  // This will cause minor versions to be automatically installed via package.json

### Environment settings
*   Use foreman
    -   Does a lot of automated work and help in setting enviroment variables
    -   npm install -g forman
    -   create .env file
    -   {
            "port": 9000,
            connection: {
                "sql": "",
                "mongo": ""
            }
        }
    -   use **nf start** to run projects
    -   all the enviroment variables can be accessed as process.env.port


### Cross platform
*   Use file naming wisely
    -   lowercase
    -   '-' seperation is better than camel case as mac doesn't support

### KISS approach
*   Don't use a lot of tools, use only when its necessary 