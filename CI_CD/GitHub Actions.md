Flow: 
1) You have your code - devs have their code for features etc
2) They commit this code to a repo
3) the committed code triggers a GitHub Action workflow  - this is written in a `yaml` file. it specifies what actions to take when a commit occurs
4) Next the build occurs alongside automated tests
5) If build and test are both successful it creates a new deployable version of the product/application.

**What does GitHub Actions actually do?**
- They perform CI - They automatically build and test your code. 
- CD - it can automatically deploy to production 