# escl-autotest

## Setup Test ENV

### avocado and avocado-vt

```
 $ yum install python2-avocado avocado-plugins-vt
```

You don't need to worry about 'avocado vt-bootstrap',
this command would be called in Jenkins job to provide cfg.

### Jenkins

escl-autotest dynamic generate avocado cfg via jenkins params.

Jenkins ->  New Item -> Pipeline

#### Pipeline Definition

Pipeline Definition: Pipeline script from SCM
- SCM: Git
  - Repositories
    - Repository URL: git@gitlab.com:EasyStack/escl-autotest.git
  - Script Path: JenkinsJobs/iso
