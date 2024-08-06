### Main components :
- deploy-branch-release.yml ------->(workflow)
- on_merge_to_main.yml ------------>(workflow)

#### deploy-branch-release.yml
This workflow is designed to create a 'release-*' branch from the 'develop' branch when options (_major, minor and patch_) are chosen, and create a '-hotfix-' branch from 'main' when (_hotfix_) is chosen from the workflow_dispatch drop down. There are validation and checks that are present in the workflow to maintain consistency and quality (e.g. only pull requests from the release and hotfix branch can be merged into main, validates current tag version etc...). Please go through the code to get a better understanding! <br></br>
**Note :** When (_hotfix_) is chosen from the dropdown, the new branch created is from the (_main_) branch, this logic is hard coded so DO NOT CHANGE THE BRANCH TO MAIN. Unfortunetly GitHub does not have dynamic branch change display, so even if you choose (_hotfix_) it will show develop, this is ok.

 <img width="277" alt="Screenshot 2024-07-26 at 11 46 50 AM" src="https://github.com/user-attachments/assets/081796eb-4f45-43fc-ab43-10ed4fb7f357">

#### on_merge_to_main.yml
This workflow will automatically create a tag, a release version, release notes based on pull request labels, access the release-drafter.yml template, perform validation and checks and finally release to production. 

## Rules :
### Make sure to create and release one branch at a time to maintain consistency
(e.g. if you want to create a hotfix and there is a minor branch already that is being worked on, please deploy the minor branch so the release exists before moving on the creating the hotfix, every branch should be released and deployed to production before the next branch is created)

### Release Version and Tags should be in sync
Make sure to keep the Tag and Release Version in sync (e.g If the release version is v1.0.0 make sure there isn't any tag above that number, manually delete the tags and match it to its release number. e.g. release version v1.0.0 should have tag v1.0.0)

<img width="377" alt="Screenshot 2024-07-26 at 12 04 37 PM" src="https://github.com/user-attachments/assets/c553195d-6727-4cbd-8811-a3f598be81c7"> <br></br>
<img width="277" alt="Screenshot 2024-07-26 at 12 05 02 PM" src="https://github.com/user-attachments/assets/dfd96d61-fd43-44a3-811f-2d35f7e3328e">
