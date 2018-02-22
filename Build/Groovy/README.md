
"simpleci-groovy-library" is a collection of wrappers written to simplify various activities supported by Jenkins. These wrappers can be invoked directly as part of a project's Jenkinsfile pipeline. The library can be configured globally (at the Jenkins master), or on a per-pipeline basis.

## Table of contents
* Pre-requisites
* Installation
* Features

### Pre-requisites
  - Should have administrative access to SimpleCI.

### Installation

```
Login to SimpleCI with BitBucket credentials. If you're already an admin, you'll see "Manage Jenkins" in the left navigation.
Select "Configure Global System"
Click "Add" under the section "Global Pipeline Libraries"
Enter a name/version
Select a "Retrieval Method". As a best practice, it's best to host the libraries in git and point Jenkins to the correct branch/tag.
```

### Features

- Wrapper functions, which can be used in pipeline scripts to simplify various tasks.
- To be used in conjunction with SimpleCI Jenkinsfiles.