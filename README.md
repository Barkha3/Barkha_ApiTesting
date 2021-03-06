
## Introduction

This is a sample Rest API test solution for sample endpoints available in https://any-api.com/. The published APIs represent a blog application where users can publish post and comment on them.

Tests are written using a combination of SerenityBDD, RestAssured, Junit & Maven.

## Framework & Design Considerations
- Serenity BDD is a library that makes it easier to write high quality automated acceptance tests, with powerful reporting and living documentation features. It has strong support for both web testing with Selenium, and API testing using RestAssured.
- API calls & validations are made using RestAssured and SerenityRest which is a wrapper on top of RestAssured.  
- This solution is designed in an Action-Question pattern with the code base categorized into domain model packages based on user actions and questions to understand/validate results. 
- Each domain package consist of an Action class where API actions are defined and another Question class where user questions/assertions are written.
- These domain models are called from a step-definitions class which are in-turn called from BDD tests.
- A test scenario to validate API response schema has been included for each endpoint in the respective feature file. The API spec for schema comparison is placed inside "schema" folder in test resources. 

### The project directory structure

```Gherkin
src
  + main
    + java                          Test runners and supporting code
      + posts                       Domain model package consisting of all actions/questions on blog posts functionality
          BlogPostActions           API calls/User actions on blog post APIs
          BlogPostQuestions         User questions/validations on blog post API response
      + commontasks                 Package for all common actions and questions
          CommonQuestions           All common questions/validations across all the domain models
          CommonRequestSpec         Common Request Spec for the API calls
      + commonutilies               Common utility methods
src
  +test
      + features                    Test cases files directory
          GetPostCommentTests.java  Class containing JUnit tests
      + schema                      Folder containing json schema for API schema validation
      Serenity.conf                 Configurations file

```
## Executing the tests
Run `mvn clean verify` from the command line.

The test results will be recorded here `target/site/serenity/index.html`.
Please run the below command from root directory to open the result after execution.
```bash
open target/site/serenity/index.html 
```
Reports can be seen in circleci, under the artifacts section `serenity/index.html`.

Each step in tests are very clearly documented for readability and debugging in case of failures.

### Additional configurations

Additional command line parameters can be passed for switching the application environment.
```json
$ mvn clean verify -Denvironment=dev
```
Configurations to for different environments are set in the `test/resources/serenity.conf` file. In real time projects each environment can be configured with its baseurl to run the tests based on different environments.
```
environments {
  default {
    baseurl = "https://jsonplaceholder.typicode.com"
  }
  dev {
    baseurl = "https://jsonplaceholder.typicode.com"
  }
  staging {
    baseurl = "https://jsonplaceholder.typicode.com"
  }
}
```
