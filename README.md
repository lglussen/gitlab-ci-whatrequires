# whatrequires
Understanding what projects are activly depending on a given repository as part of their `.gitlab-ci.yml`
pipeline configuration is a classic governance challenge in GitLab.
Because the `.gitlab-ci.yml` file is just another blob of text in a repository, GitLab doesn’t provide a native "Used By" button for shared CI projects like it does for npm or NuGet packages.

To get this data, this project utilized the gitlab API to discover repositories with references to the library project and and combines the result with Pipeline History to give an indication of how active the reference is.

## requirements
```shell
# if using pip package manager
pip install python-gitlab

# if using dnf/RPM (Fedora / Red Hat)
dnf install python3-gitlab
```

## setup 
These values may be provided as arguments but may also be configured as enviroment variables
```shell
export GITLAB_ACCESS_TOKEN='xxxxxxxx'
export GITLAB_URL='https://your.gitlab.com'
```
The api access token will need api read access to browse projects and repository read access to read the contents of `.gitlab-ci.yml` files.

## Running
Search all projects on your.gitlab.com for libray `https://your.gitlab.com/my-org/ci-library`
```shell
./whatrequires my-org/ci-library
```

Search projects within the group/subgroup `other-org/ansible` with verbose flag for extra output
```shell
./whatrequires my-org/ci-library  other-org/ansible --verbose
```

