### Main components :
- release-drafter.yml ------------ >(template)
- deploy-branch-release.yml ------->(workflow)
- on_merge_to_main.yml ------------>(workflow)

#### release-drafter.yml
This file is a template file that is referenced into 'on_merge_to_main.yml' to create the release notes, it holds the structure on HOW and WHAT the release notes should look like. It works only when pull requests are tagged with their appropriate 'label' in GitHub. Adding a 'Milestone' to the pull request is optional but recommended to measure total number of items resolved in a particular sprint. <br></br>
**Note :** If you want new labels created in GitHub to be reflected and categorised in the final release notes, please update this section below in the release-drafter.yml template file

<img width="451" alt="Screenshot 2024-07-26 at 11 54 52 AM" src="https://github.com/user-attachments/assets/6b7392ad-890b-453b-af06-900623f35f32">

#### deploy-branch-release.yml
This workflow is designed to create a 'release-*' branch from the 'develop' branch when options (_major, minor and patch_) are chosen, and create a '*-hotfix-*' branch from 'main' when (_hotfix_) is chosen from the workflow_dispatch drop down. There are validation and checks that are present in the workflow to maintain consistency and quality (e.g. only pull requests from the release and hotfix branch can be merged into main, validates current tag version etc...). Please go through the code to get a better understanding! <br></br>
**Note :** When (_hotfix_) is chosen from the dropdown, the new branch created is from the (_main_) branch, this logic is hard coded so DO NOT CHANGE THE BRANCH TO MAIN. Unfortunetly GitHub does not have dynamic branch change display, so even if you choose (_hotfix_) it will show develop, this is ok.

 <img width="347" alt="Screenshot 2024-07-26 at 11 46 50 AM" src="https://github.com/user-attachments/assets/081796eb-4f45-43fc-ab43-10ed4fb7f357">

#### on_merge_to_main.yml
This workflow will automatically create a tag, a release version, release notes based on pull request labels, access the release-drafter.yml template, perform validation and checks and finally release to production. 

## Rules :
### Make sure to deploy and release one branch at a time to maintain consistency
(e.g. if you want to create a hotfix and there is a minor branch already that is being worked on, please deploy the minor branch so the release exists before moving on the creating the hotfix, every branch should be released and deployed to production before the next branch is created)

<img width="529" alt="Screenshot 2024-07-26 at 12 04 37 PM" src="https://github.com/user-attachments/assets/c553195d-6727-4cbd-8811-a3f598be81c7">
<img width="277" alt="Screenshot 2024-07-26 at 12 05 02 PM" src="https://github.com/user-attachments/assets/dfd96d61-fd43-44a3-811f-2d35f7e3328e">


### Release Version and Tags should be in sync
Make sure to keep the Tag and Release Version in sync (e.g If the release version is v1.0.0 make sure there isn't any tag above that number, manually delete the tags and match it to its release number. e.g. release version v1.0.0 should have tag v1.0.0)

