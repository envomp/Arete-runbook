# Handling Arete's subtesters

Currently availabe subtesters are visible [here at docker repository](https://hub.docker.com/search?q=automatedtestingservice&type=image)

## Webhooks

Add a following webhook to tests repository to run tests after teacher pushes to validate tests:
 - URL: https://cs.ttu.ee/services/arete/api/v2/exercise
 - Secret Token: <permission_group> <permission_group_token>
 - Make sure arete.json contains `programmingLanguage` and `solutionsRepository`

Add a following webhook to solutions repository to run tests after teacher pushes his/her own solution:
 - URL: https://cs.ttu.ee/services/arete/api/v2/submission/:webhook/withTests?testRepository=<tests_repository> where <tests_repository> can be git@gitlab.cs.ttu.ee:iti0102-2020/ex.git for example
 - Secret Token: <permission_group> <permission_group_token>


## Usage

First make sure you have the latest version installed. You can use [arete front](https://gitlab.cs.ttu.ee/testing/arete-ui) to do so.

you can place arete.json file in the root of the repository or exercise for customised testing.

Example:
````json
{
  "dockerTimeout": 120,
  "dockerExtra": [
    "stylecheck"
  ],
  "systemExtra": [
    "anonymous",
    "noMail",
    "noFiles",
    "noTesterFiles",
    "noStudentFiles",
    "noStd",
    "noOverride",
    "noFeedback",
    "minimalFeedback"
  ],
  "groupingFolders": [
  "KT",
  "TK",
  "EXAM"
  ],
  "solutionsRepository": "https://gitlab.cs.ttu.ee/iti0102-2020/ex",
  "programmingLanguage": "python"
}
````

```dockerTimeout``` - maximum allowed code execution time

```dockerExtra``` - every subtester has different ones (seek subtester repository for more)

   * ```stylecheck``` - check style in Python tester

   * ```-r TESTNG,COMPILER,CHECKSTYLE,FILEWRITER,REPORT``` - check style in Java tester

```systemExtra``` - more testing specifics

   * ```anonymous``` - nothing is sent to arete backend (Use with caution)

   * ```noMail``` - student doesn't get a mail with testing results
   
   * ```noFiles``` - no files are returned from testing
   
   * ```noTesterFiles``` - no test files are returned from testing
   
   * ```noStudentFiles``` - no student files are returned from testing
   
   * ```noStd``` - test container logs are not returned from testing
   
   * ```noStyle``` - Mail won't containt any style related fields and all traces of any stylecheck will be removed
   
   * ```noOverride``` - Don't let arete.json files override existing parameters
   
   * ```noFeedback``` - ![noFeedback](../pictures/none.png)
   
   * ```minimalFeedback``` - ![minimalFeedback](../pictures/minimal.png)
   
   otherwise student sees the following: ![full](../pictures/full.png)

```groupingFolders``` - folders which are not slugs themselves but contain slugs. Note: students still need to have the same file tree for testing to be successful

```solutionsRepository``` - repository which contains solutions against what tests are ran after being updated.

```programmingLanguage``` - programming language - used to determine tester
