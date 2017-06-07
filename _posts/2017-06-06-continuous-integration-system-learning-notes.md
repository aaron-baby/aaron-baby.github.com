---
layout: post
title: CI系统学习笔记
tags: learning_notes Continuous_Integration
---
## {{page.title}} ##
## responsibility
verify a commit will not break any tests

### 设计要点
* fetch new changes
* run the tests and report its results
* failure resistant
* handle load well
	- We can achieve this by distributing and parallelizing the testing effort.

### Roles
- **repository observer**
	- The observer watches the repository. When it notices that a commit has been made, it notifies the job dispatcher.
- a test **job dispatcher**
- the **test runner** reports its results to a component that makes them available for people to see, perhaps on a webpage.

### Repo observer实现
`repo_observer.py` file
- parses command line arguments: dispatcher-server address, repository path
- kicks off an infinite while loop to periodically check the repository for changes.
		while True:
		    try:
		        # call the bash script that will update the repo and check
		        # for changes. If there's a change, it will drop a .commit_id file
		        # with the latest commit in the current working directory
		        subprocess.check_output(["./update_repo.sh", args.repo])
		    except subprocess.CalledProcessError as e:
		        raise Exception("Could not update and check repository. " +
		                        "Reason: %s" % e.output)

思考：`updaterepo.sh`通过`git log`和`git pull`get and compare OLD\_COMMIT\_ID 和 NEW\_COMMIT\_ID 比较耗资源。

through "post-commit hooks" send notifications to callback URL more efficiency

但是每个commit都会触发，可以把新增的commit按行追加到new_commit file, when success dispatch new commit, empty new commit file.

### Dispatcher
用来分发任务，communicating with repo observer and test runner

#### Logic

`runner_checker` used test runner status and remove unresponsive runner.

`redistribute` function dispatch pennding commits to available runner
from pool of registreded runners.

#### Handler
handles commands `status`, `register`, `dispatch`, and `results` from outside request.

### Test Runner Part
#### `dispatcher_checker`

important for resource management. If the dispatcher goes down, then the test runner will shut down

#### `runtest` steps:

1. updates the repository to the given commit ID.
2. call unit test suite
		suite = unittest.TestLoader().discover(test_folder)
		unittest.TextTestRunner(result_file).run(suite)
3. write to result_file

#### Reference
- [A Continuous Integration System](http://aosabook.org/en/500L/a-continuous-integration-system.html "A Continuous Integration System")