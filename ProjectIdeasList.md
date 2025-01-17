# Bareos Google Summer of Code 2024 Project Ideas List

We are open for GSoC contributors to propose their own original project ideas.
Please use [Discussions/Ideas](https://github.com/bareos/GSoC2024/discussions/categories/ideas) to propose and discuss your idea.

## Standardize Debug Message Levels

The Bareos source code uses debug messages to allow detailed logging for tracing and debugging purposes.
Currently, almost all debug message calls get the level passed as a arbitrary numeric value, where generally a higher number means more details.
The idea is to create a guideline for developers that describes which level to use.
For this a comprehensive list of currently used debug-levels should be compiled by analyzing the source code.
The next step is to change all debug message calls to use a meaningful constant instead of numeric value.

**Expected outcomes**:
* Debug message guideline section added to [developer guide](https://docs.bareos.org/DeveloperGuide.html)
* Source code changed to use meaningful constants instead of numeric values

**Skills required/preferred**:
Basic C/C++, reStructuredText

**Possible mentors**: arogge, pstorz

**Expected size of project**: ~90 hours (small)

**Difficulty rating**: Easy

## WebUI: Form for plugin specific options on restore

Bareos can use [plugins](https://docs.bareos.org/TasksAndConcepts/Plugins.html#file-daemon-plugins) to backup application specific data.
For some plugins it can be necesary to pass multiple plugin specfic options on restore, currently the [Bareos WebUI](https://docs.bareos.org/IntroductionAndTutorial/BareosWebui.html) only shows a simple plugin options field, where the user can add multiple options in one string separated by colon.
Ideally, the WebUI should show a pre-filled form with the plugin options that have been used at  backup  time, using proper form elements like select or radio buttons.
A full solution of this problem will probably include changes both in the Bareos core and WebUI.

**Expected outcomes**
* A plugin author should be able to define which plugin options will be shown for restore in the WebUI
* The WebUI should show a plugin specific form for restore options

**Skills required/preferred**:
C/C++, Python, PHP, Javascript, HTML, CSS

**Possible mentors**: arogge, pstorz

**Expected size of project**: ~350 hours (large)

**Difficulty rating**: hard

## Enable using virtualenv for Python plugins

Currently Python plugins require to fulfill dependencies by either installing operating system packaged python modules or by using pip as root, when the required versions are not available as packages.
The first task is to research if it is possible at all to use virtualenv with Bareos Python plugins.
This requires to understand the [Bareos Python Plugin API](https://docs.bareos.org/DeveloperGuide/PythonPluginAPI.html).
Depending on the outcome of the research, the second task is to either implement and documentent how to use virtualenv with plugins, or work on a proposal how to change the Bareos Puthon plugin architecture to allow using virtualenv.
Ideally it should be possible to use a virtualenv management like pipenv.

**Expected outcomes**
* It should be possible to use virtualenv for Bareos Python plugins

**Skills required/preferred**:
C/C++, Python

**Possible mentors**: arogge, pstorz

**Expected size of project**: ~175 hours (medium)

**Difficulty rating**: hard

## Using Pylint to increase the Python code quality

As Bareos developers we are interested to deliver the best code as possible.
Pylint can help to detect issues and make suggestion to make the code better.
As we completely drop python2 support, we want to in a first run check and report the score of each of the python module/code we have.
Getting a synthetic view of what kind of improvements that can be done is a plus.
The second step is cleaning up all Python code by removing python2 specific code and address the code issues reported by pylint as far as possible.
It is also planned to integrate Pylint in Jenkins to automatically check code quality.

**Expected outcomes**
* Python code has a good pylint rating score

**Skills required/preferred**:
Python

**Possible mentors**: arogge, pstorz

**Expected size of project**: ~175 hours (medium)

**Difficulty rating**: medium

## Create a new Bareos Plugin to allow Backup of Cloud Storage

The existing plugin which is using [Apache Libcloud](https://libcloud.apache.org/) is able
to backup data from S3 compatible storage. Unfortunately it has issues with Python versions
above 3.8 due to using multiprocessing together with the fact that the Bareos Python plugin
architecture is using subinterpreters.
The idea is to create a new plugin which should also work with newer Python versions.
It will probably still be required to use multiple data streams in parallel to allow sufficient
performance, so the challenge is to find out which Python parallelizing module works best for this purpose.
Additionally the new plugin should use [Apache OpenDAL](https://opendal.apache.org/) as it's
specialized for data access with a unique API to access different cloud storage services,
while Apache libcloud aims to cover all kinds of cloud resources.
So by using OpenDAL it should be easy to allow the plugin to backup any of its support
cloud storage services.

**Expected outcomes**
* A new Bareos Python Plugin using Apache OpenDAL to allow backing up cloud storage

**Skills required/preferred**:
Python

**Possible mentors**: arogge, pstorz

**Expected size of project**: ~350 hours (large)

**Difficulty rating**: hard

## Add support scripts to allow backups to object-based storages

The currently existing droplet backend is far from optimal. Its upcoming
replacement will work with scripts to interface with the storage service.
While our first priority is to support Amazon S3 compatible storages, having
more scripts to support different storage backends would provide significant
value to our users.

The idea is to identify public or private storage services that are reasonable
backup targets and to implement the scripts required for Bareos to interact
with those.
Serivces that come to mind are for example Azure Blob Storage, Google Cloud
Storage and OpenStack Swift, but also things like scp/sftp, WebDAV or maybe
even something generic like OpenDAL. Basically everything that can be
(mis-)treated as an object storage.

**Expected outcomes**
One or more backend scripts for backing up to one or more types of object
storages.

**Skills required/preferred**:
Python and/or Bash, basic understanding of object-based storages

**Possible mentors**: arogge, pstorz

**Expected size of project**: ~175 hours (medium)

**Difficulty rating**: easy
