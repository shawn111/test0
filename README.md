# escl-autotest

## Setup Test ENV

### avocado and avocado-vt

```
 $ yum install python2-avocado avocado-plugins-vt
```

You don't need to worry about 'avocado vt-bootstrap',
this command would be called in Jenkins job to provide cfg.

### Jenkins

#### New pipeline
escl-autotest dynamic generate avocado cfg via jenkins params.

Jenkins ->  New Item -> Pipeline

#### Jenkins to run avocado command

/srv/jenkins

```
chmod umask g+w /srv/avocado
chmod 2775 /srv/avocado
chown autotest:autotest -R /srv/avocado

usermod -a -G autotest jenkins
```

/etc/avocado/avocado.conf
```
[datadir.paths]
# Avocado data dir (holds tests and test auxiliary data, such as ISO files).
base_dir = /srv/avocado
# You may override the specific test directory with test_dir
test_dir = /srv/doc/avocado/tests
# You may override the specific test auxiliary data directory with data_dir
data_dir = /srv/avocado/data
# You may override the specific job results directory with logs_dir
logs_dir = /srv/avocado/job-results

...
```

#### Pipeline Definition

Pipeline Definition: Pipeline script from SCM
- SCM: Git
  - Repositories
    - Repository URL: git@gitlab.com:EasyStack/escl-autotest.git
  - Script Path: JenkinsJobs/iso


