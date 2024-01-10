---
title: Setup
---
# Set-up your working environment


> ## Mattermost (chat)
> There is a dedicated Mattermost team, called [CMSDAS@CERN 2024](https://mattermost.web.cern.ch/signup_user_complete/?id=7hedxbi647dbbqouez9449g3ba&md=link&sbr=su), setup to facilitate communication and discussions via live chat (which is also archived). The channel is hosted by the [CERN Mattermost instance](https://mattermost.web.cern.ch/).
> 
> If you have never used Mattermost at CERN, please know that you will need your CERN login credentials (SSO) and you will need to join the private CMSDAS@CERN 2023 team in order to be able to see (or find using the search channels functionality) the channels setup for communications related to the school.
> 
> If you already have used Mattermost at CERN, please know that when you click direct links to channels (as you will find below) that are within the CMSDAS@CERN 2023 team, you **may** be redirected to the last Mattermost team you used. If this happens, remember to click the [signup link to join the CMSDAS@CERN 2024 team](https://mattermost.web.cern.ch/signup_user_complete/?id=7hedxbi647dbbqouez9449g3ba&md=link&sbr=su) to switch to the correct team from which you should be able to see the individual channels. If that still doesn’t work, remove all cookies associated with cern.ch and restart your browser.
> 
> The [LongExJPsiJPsi](https://mattermost.web.cern.ch/cmsdaslpc2024/channels/longexjpsijpsi) will be available once you join or switch to the CMSDAS@CERN 2024 team!
> 
> Note that you can access Mattermost via browser or you can download the corresponding application running standalone on your laptop or smartphone. The laptop application does not work with CERN certificate login.
{: .prereq}

> ## Git repository
>
> In order to keep track of your changes please fork this repository:
> ~~~
> https://github.com/IreneZoi/DAS2024JpsiJpsi.git
> ~~~
> Do this step after opening this link in a browser, selecting `fork` button, and then selecting `create fork`.
> 
> You should aim to commit and push your changes that you make in the code frequently.
> 
> Common git commands include:
> 
> checking which files have been modified.
> ~~~bash
> git status
> ~~~
>
> staging files that have been modified (preparing to commit them to the repo)
> ~~~bash
> git add <filename>
> ~~~
> 
> Committing the staged files with a brief but useful commit message:
> ~~~bash
> git commit -m "your message in quotes"
> ~~~
> 
> push your commits to the repository on github (so they can be accessed from the web)
> ~~~bash
> git push
> ~~~
> 
> ## Setting up Analysis Environment on LPC
>
> ~~~bash
> ssh -Y USERNAME@cmslpc-sl7.fnal.gov
> cd ~/nobackup/
> mkdir CMSDAS2024
> cd CMSDAS2024
> git clone https://github.com/<USERNAME>/DAS2024JpsiJpsi.git
> cd DAS2024JpsiJpsi
> source /cvmfs/cms.cern.ch/cmsset_default.sh
> cmsrel CMSSW_10_2_5
> cmsrel CMSSW_11_1_1
> ~~~
>
{: .prereq}

{% include links.md %}
