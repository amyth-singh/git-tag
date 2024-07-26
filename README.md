### This repository contains three key files :
- release-drafter.yml ------------ >(template)
- deploy-branch-release.yml ------->(workflow)
- on_merge_to_main.yml ------------>(workflow)

#### release-drafter.yml
This file is a template file that is referenced into 'on_merge_to_main.yml' to create the release notes, it holds the structure on HOW and WHAT the release notes should look like. It works only when pull requests are tagged with their appropriate 'label' in GitHub. Adding a 'Milestone' to the pull request is optional but recommended to measure total number of items resolved in a particular sprint. 

#### deploy-branch-release.yml
This workflow is designed to create a 'release-*' branch from the 'develop' branch when options (_major, minor and patch_) are chosen, and create a '*-hotfix-*' branch from 'main' when (_hotfix_) is chosen from the workflow_dispatch drop down. There are validation and checks that are present in the workflow to maintain consistency and quality (e.g. only pull requests from the release and hotfix branch can be merged into main, validates current tag version etc...). Please go through the code to get a better understanding!

#### on_merge_to_main.yml
This workflow will automatically create a tag, a release version, release notes based on pull request labels, access the release-drafter.yml template, perform validation and checks and finally release to production. 

## Note : make sure to complete an entire deployment lifecycle before creating a new tag. (e.g. new vx.x.x cannot be created unless previous vx.x.x is completed deployed and a release is present)
