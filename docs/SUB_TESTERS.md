# Handling Arete's subtesters

Currently availabe subtesters are visible [here at docker repository](https://hub.docker.com/search?q=automatedtestingservice&type=image)

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
  ]
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
   
   * ```noOverride``` - Don't let arete.json files override existing parameters
   
   * ```noFeedback``` - ![noFeedback](pictures/none.png)
   
   * ```minimalFeedback``` - ![minimalFeedback](pictures/minimal.png)
   
   otherwise student sees the following: ![full](pictures/full.png)
   
## Specifics

