---
title: "Exercise 2: Data fit"
teaching: 30
exercises: Thursday
questions:
- Can we perform a multiple structure fit?

---
> ## Goal of this exercise
> The goal of this exercise is to **find structures in the JpsiJpsi spectrum and evaluate their significance**.
> `mJJDataFull6000_15000.txt` was created in Exercise 1 with a small amount of data, so the events in this file are not enough for a good fit. We have prepared [a file containing all the full Run2 available statistics](https://github.com/IreneZoi/DAS2024JpsiJpsi/blob/exercise/fullrun2data/mJJDataFull6000_15000.txt) that will be used for the next fit step.
{: .checklist}



## Fit setup
~~~
cd ~/nobackup/CMSDAS2024JpsiJpsi/CMSSW_11_1_1/src/
cmsenv
cd ../../fitpackage/
# Then you need to compile the pre-defined fit functions
source makeLibSo.sh

# you should see this output:
Processing BlattWeisskopfQ2.cxx+...
Info in <TUnixSystem::ACLiC>: creating shared library /uscms_data/d3/lchen/cmsdas2024/CMSSW_11_1_1/src/fitpackage/./BlattWeisskopfQ2_cxx.so

Processing ComplexRelBWFcn.cxx+...
Info in <TUnixSystem::ACLiC>: creating shared library /uscms_data/d3/lchen/cmsdas2024/CMSSW_11_1_1/src/fitpackage/./ComplexRelBWFcn_cxx.so

Processing MyRelBWSquare.cxx+...
(MyRelBWSquare) An instance of MyRelBWSquare.

......
~~~
{: .language-bash}

## The background fit

We have prepared two files for you, [`null.C`](https://github.com/IreneZoi/DAS2024JpsiJpsi/blob/exercise/fitpackage/null.C) and [`null_BW0.C`](https://github.com/IreneZoi/DAS2024JpsiJpsi/blob/exercise/fitpackage/null_BW0.C). 

In `null.C`, only the probability distribution functions of the two backgrounds, SPS (single-parton scattering) and DPS (double-parton scattering), are used to fit the data, while `null_BW0.C` considers also one structure peak described by a Breit-Wigner. This will be described in the next section. For now let's focus on the backgrounds.

> ## More on the backgrounds...
> <a href="../files/SPS.png"><img src = "../files/SPS.png" alt="SPS" width ="500"></a>
> <a href="../files/DPS.png"><img src = "../files/DPS.png" alt="DPS" width ="500"></a>
{: .solution}

> ## Task 1
> Open the [`null.C`](https://github.com/IreneZoi/DAS2024JpsiJpsi/blob/exercise/fitpackage/null.C) code and understand the different parts. The comments in the code should help you identify:
> - Where the background functions are defined
> - How is the final fit function (pdf built)
> - Where the fit to the data happens
> - How to plot the fit results
{: .challenge}

Now you can run `null.C`:
~~~
root -l null.C 
~~~
{: .language-bash}

It will take a few minutes to run the code and it will produce a long printout on the screen. The important informations are summarized at the end and the plot will be stored in `figure/fit_null.pdf`.

> ## Your fit should look like this
> <a href="../files/null.pdf"><img src = "../files/null.pdf" alt="SPS" width ="500"></a>
{: .solution}

> ## Questions 
> - Is it a good fit? 
> - What is the value of the log-Likelihood of the fit? 
> - How many free parameters are in the fit?
{: .challenge}

> ## Tip
> remember the "FCN value"! We will call it `FCN_b`` later.
{: .callout}

 {% include links.md %}