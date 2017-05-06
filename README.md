Jenkins Job Builder library
===========================

This repo holds configs for jenkins jobs and some useful tools.

Using jenkins configs
---------------------

### Creating ini file for server with your creds

set server name to operate with

```bash
server_name="example"
```

Copy config and replace server address, user and password with your own

```bash
cp "./conf/jenkins_job.ini.example" "./${server_name}.ini"
```

### Testing jobs configs

test all (useful for testing changes in commons)

```bash 
tox
```

test just configs for particular instance

```bash 
tox -e "${server_name}"
```

**Note**: tox should be installed globally


### Comparing job configs before/after changes

To compare output of changed yaml configs you need to render xmls.

Let's say we are going to change something in `${pr_branch}`
 
For existing branch

```bash
# activate venv used in test with right version of tools
source "./.tox/${server_name}/bin/activate"

# switch to current revision
git checkout master
git pull

# render current xmls
jenkins-jobs --conf "./${server_name}.ini" test "servers/${server_name}/:common" -o "./out-for-master"

# switch to existing pr/changed revision
git checkout "${pr_branch}"
git pull
```

or to create new branch

```bash
git checkout -b "${pr_branch}"
# .. and do some changes

# render new xmls
jenkins-jobs --conf "./${server_name}.ini" test "servers/${server_name}/:common" -o "./out-for-${pr_branch}"

# compare with diff tool

diff -r "./out-for-master" "./out-for-${pr_branch}"
```
**Note**: 
- `>` sign means that change came from `./out-for-${pr_branch}`
- `<` sign means that change came from `./out-for-master`


### Updating/adding jobs on jenkins instance.

```bash
# activate venv used in test with right version of tools
source "./.tox/${server_name}/bin/activate"
# update all jobs on server
# this will not delete any job if it is not presented in configs
jenkins-jobs --conf "./${server_name}.ini" update "servers/${server_name}/:common"
# update jobs by pattern (note single quotes): 
jenkins-jobs --conf "./${server_name}.ini" update "servers/${server_name}/:common" 'ABC-*'
# deactivate venv when finished
deactivate
```


### Removing (**deleting**) jobs from jenkins instance.

```bash
# activate venv used in test with right version of tools
source "./.tox/${server_name}/bin/activate"
# this will delete job on server
jenkins-jobs --conf "./${server_name}.ini" delete "name-of-job-to-remove"
# deactivate venv when finished
deactivate
```


----

For details, examples and contribution guides see
[library and samples](https://github.com/ci-team/jjb-library)
[fuel_infra/jenkins_jobs repo](https://github.com/fuel-infra/jenkins-jobs), and especially
[guidelines section](https://github.com/fuel-infra/jenkins-jobs/blob/master/README.rst#code-guidelines).

Documentation for Jenkins Job Builder could be found on [docs.openstack.org](http://docs.openstack.org/infra/jenkins-job-builder/)

