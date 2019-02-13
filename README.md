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
# make sure jenkins could write avocado output dir
usermod -a -G autotest jenkins

umask g+w /srv/avocado
chmod g+w -R /srv/avocado
mkdir -p /srv/avocado/data/avocado-vt/images
mkdir -p /srv/avocado/data/avocado-vt/isos
chown autotest:autotest -R /srv/avocado
chmod 2775 /srv/avocado
chmod 2775 /srv/avocado/data/avocado-vt
chmod 2775 /srv/avocado/data/avocado-vt/images
chmod 2775 /srv/avocado/data/avocado-vt/isos

touch /usr/share/avocado-plugins-vt/shared/unattended/escore-devel.ks
chgrp autotest /usr/share/avocado-plugins-vt/shared/unattended/escore-devel.ks
chmod 775 /usr/share/avocado-plugins-vt/shared/unattended/escore-devel.ks
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


