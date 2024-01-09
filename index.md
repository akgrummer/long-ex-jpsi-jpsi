---
layout: lesson
root: .  # Is the only page that doesn't follow the pattern /:path/index.html
permalink: index.html  # Is the only page that doesn't follow the pattern /:path/index.html
venue: "LHC Physics Center, Fermi National Accelerator Laboratory"        # brief name of the institution that hosts the workshop without address (e.g., "Euphoric State University")
address: "In Person"      # full street address of workshop (e.g., "Room A, 123 Forth Street, Blimingen, Euphoria"), videoconferencing URL, or 'online'
country: "us"      # lowercase two-letter ISO country code such as "fr" (see https://en.wikipedia.org/wiki/ISO_3166-1#Current_codes) for the institution that hosts the workshop
language: "en"     # lowercase two-letter ISO language code such as "fr" (see https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) for the
latitude: "41.842258"        # decimal latitude of workshop venue (use https://www.latlong.net/)
longitude: "-88.245781"       # decimal longitude of the workshop venue (use https://www.latlong.net)
humandate: "Synchronously January, 2023"    # human-readable dates for the workshop (e.g., "Feb 17-18, 2020")
humantime: "24/7"    # human-readable times for the workshop (e.g., "9:00 am - 4:30 pm")
startdate: 2023-01-09 # machine-readable start date for the workshop in YYYY-MM-DD format like 2015-01-01
enddate: 2023-01-13   # machine-readable end date for the workshop in YYYY-MM-DD format like 2015-01-02
email: ["agrummer@cern.ch"]
---

<!-- ![CMS Detector Slice](https://cmsexperiment.web.cern.ch/sites/cmsexperiment.web.cern.ch/files/detectoroverview.gif){:width="50%"} -->

## Welcome to the CMS Data Analysis School 2024 JPsi-JPsi Long exercise

This exercise looks for possible tetraquark candidates that decays into double J/ψ, and each J/ψ decays in dimouns. **Our exercises will all use real data!** 

This analysis will search for structures near the J/psiJ/psi mass threshold using CMS Run II data at sqrt(s)=13 TeV. <!-- Based on the hints of possible structures found in CMS Run I data, a mass region between 6.26 GeV and 7.8 GeV is blinded in Run II data to prevent analysis bias. We will learn how to decide the fit strategy before unblinding the data,--> We will learn the procedure to distinguish multiple new structures from background. A simple method to determine the significance of new structure will be applied in the process.

The overall purpose of this exercise is to provide you with a basic understanding of a physical analysis and the opportunity to participate in it. Considering that we need to compress an analysis that has taken several years into a few days of exercise, we need to capture as many of the key aspects as possible. We will provide you with examples of some of the procedures to help you understand them. And for some of the procedures that are time-consuming because of large data, you will only need to be able to run through them with a small amount of data, and we will provide you with pre-prepared data for the next step. If you have any questions about the exercise, please feel free to ask. If you have better insights or ways to any part, please feel free to do that as well. It is sincere hope that we all get a lot out of this exercise!
 
> ## Exercise Goals
> - Reconstruct double Jψ events from raw data
> - Estimate background from data itself
> - Distinguish multiple new structures from background events step by step
> - Employ maximum likelihood fit in the mass distribution
{: .checklist}

> ## Prerequisites
> **Before going any further, please complete the [CMS DAS Pre-Exercises](https://fnallpc.github.io/cms-das-pre-exercises/index.html) and then follow the instructions on the [setup page](setup.md).**
> The following short exercises are also recommended:
> - [Statistics](https://fnallpc.github.io/statistics-das/)
> - [Muon](https://twiki.cern.ch/twiki/bin/view/CMS/SWGuideCMSDataAnalysisSchoolLPC2024MuonExercise)
{: .prereq}

> ## Facilitators
> * [Kai Yi*](https://twiki.cern.ch/twiki/bin/view/Main/KaiYi), NNU ([kai.yi@cern.ch](mailto:kai.yi@cern.ch))
> * [Irene Zoi](https://twiki.cern.ch/twiki/bin/view/Main/IreneZoi), Fermilab ([irene.zoi@cern.ch](mailto:irene.zoi@cern.ch))
> * [Aidan Grummer](https://twiki.cern.ch/twiki/bin/view/Main/AidanGrummer), Fermilab ([agrummer@cern.ch](mailto:agrummer@cern.ch))
> * Offline facilitators: Liangliang Chen (NNU), Shiyi Huang (NNU), Bolin Li (NNU), Xining Wang (NNU), Kai Yi (NNU) and Yilin Zhou (NNU).
> 
> *Lead Contact
> 
> <table> 
>  <tr>
>     <td align="center"><a href="https://github.com/mmusich"><img src="https://lpc.fnal.gov//CMSDAS2024/Kai_Yi.jpg" width="100px;" alt=""/><br /><sub><b>Kai Yi</b></sub></a><br /></td>
>     <td align="center"><a href="https://github.com/akgrummer"><img src="https://lpc.fnal.gov//CMSDAS2024/Aidan_Grummer.jpg" width="100px;" alt=""/><br /><sub><b>Aidan Grummer</b></sub></a><br /></td>
>  <td align="center"><a href="https://github.com/"><img src="https://lpc.fnal.gov//CMSDAS2024/Irene_Zoi.jpg" width="100px;" alt=""/><br /><sub><b>Irene Zoi</b></sub></a><br /></td> 
> <td align="center"><a href="https://github.com/"><img src="https://lpc.fnal.gov//CMSDAS2024/Irene_Dutta.jpg" width="100px;" alt=""/><br /><sub><b>Irene Dutta</b></sub></a><br /></td> 
> <td align="center"><a href="https://github.com/"><img src="https://lpc.fnal.gov//CMSDAS2024/Yongbin_Feng.jpg" width="100px;" alt=""/><br /><sub><b>Yongbin Feng</b></sub></a><br /></td> 
> <td align="center"><a href="https://github.com/"><img src="https://lpc.fnal.gov//CMSDAS2024/Ulascan_Sarica.jpg" width="100px;" alt=""/><br /><sub><b>Ulascan Sarica</b></sub></a><br /></td>  
> </tr> 
> </table> 
{: .testimonial}

> ## Mattermost Chat
> **The [LongExJPsiJPsi](https://mattermost.web.cern.ch/cmsdaslpc2024/channels/longexjpsijpsi) channel will be available once you join the [CMSDAS@CERN2024](https://mattermost.web.cern.ch/cmsdascern2024/channels/town-square) team. Direction for how to join this Mattermost chat team can be found on the <a href="setup.html">setup</a> page.**
{: .discussion}

> ## CERN Twiki, Introduction Slides and useful material
> **The CERN TWiki of this long exercise can be found at [this link](https://twiki.cern.ch/twiki/bin/view/CMS/SWGuideCMSDataAnalysisSchoolLPC2024LongExercisejpsijpsi-pre). At the beginning of this short exercise an introduction will be done based on [these slides](https://twiki.cern.ch/twiki/pub/CMS/SWGuideCMSDataAnalysisSchoolLPC2024LongExercisejpsijpsi-pre/CMSDAS_2024.pdf).**
> Additional Material can be found here:
> - [Analysis Note AN v15](http://cms.cern.ch/iCMS/jsp/openfile.jsp?tp=draft&files=AN2021_135_v15.pdf)
> - [Paper v72](http://cms.cern.ch/iCMS/analysisadmin/get?analysis=BPH-21-003-paper-v72.pdf)
> - [Pre-Approval Talk](https://indico.cern.ch/event/1099352/contributions/4625872/attachments/2356065/4020712/preapprovalNov-30-2021.pdf)
{: .callout}
{% comment %} This is a comment in Liquid {% endcomment %}

{% include links.md %}
