---
title: "Exercise 1: Event selection "
teaching: 30
exercises: Wednesday
questions:
- Event selections for 4 muon mass spectrum
objectives:
- perform selections on root variables
- fill histograms
keypoints:
- In this exercise we made practical event selections using ROOTs Lorentz Vectors
- We used these selections to calculate mass variables
- Filled histograms and produced distributions of important variables in the analysis
- Learned how to compile and run root macros
- Gained experience with cpp syntax

---

# Goal of this exercise

The overall purpose of this exercise is to provide you with a basic understanding of a physical analysis and the opportunity to participate in it . Considering that we need to compress an analysis that has taken several years into a few days of exercise, we need to capture as many of the key aspects as possible. We will provide you with examples of some of the procedures to help you understand them. And for some of the procedures that are time-consuming because of large data, you will only need to be able to run through them with a small amount of data, and we will provide you with pre-prepared data for the next step. If you have any questions about the exercise, please feel free to ask. If you have better insights or ways to any part, please feel free to do that as well. It is sincere hope that we all get a lot out of this exercise!

# Introduction

This exercise looks for possible tetraquark candidates that decays into double J/ψ, and each J/ψ decays in dimouns. We will learn how to reconstruct double Jψ events from raw data, and how to estimate background from MC and data itself. An important aspect of this analysis is that we will learn how to identify multiple new structures from background events step by step. Another important aspect of this analysis is to employ maximum likelihood fit in the mass distribution.


# Ntuples

The ntuple creation process is very involved, so in the interest of time, this exercise will focus on later aspects of the analysis framework. The analysis ntuples will be provided throughout the exercise.

# Event selection

Our first step now is to filter data contained in the ntuple file.

Make sure to get into the CMSSW directory and set up the cmssw environment. Then move to the `eventselection/` directory from the git repo that was cloned in the setup steps.

For example (you may need to change the directory):
~~~bash
cd ~/nobackup/CMSDAS2024/DAS2024JpsiJpsi/CMSSW_10_2_5/src
cmsenv
cd ../../eventselection/
~~~

It is worth noting that only four-momentum and partial selections are provided in `myntuple.C`, so you need to add the other selections yourselves and complete the steps to output the results. We will now first describe the selections and then the variables that are needed for the analysis.

> ## Tip
> Feel free to first add the variables and see how the distributions change once you add the different selections!
{: .checklist}

The selections can be added at [here in the code](https://github.com/IreneZoi/DAS2024JpsiJpsi/blob/c429c15693d6b5db0d7720387b4ff38db08f8280/eventselection/myntuple.C#L149):

The variable used for the muons is `rawMup4vect`. You can use `rawMup4vect[i]` with `i` going from 0 to 3 to select the 4 different muons. 

> ## Investigation
> What type of variable is `rawMup4vect`?
> 
> have a look in `myntuple.C` before confirming the answer.
> > ### answer
> > found in the [code](https://github.com/IreneZoi/DAS2024JpsiJpsi/blob/c429c15693d6b5db0d7720387b4ff38db08f8280/eventselection/myntuple.C#L93): 
> > ~~~cpp
> > vector<TLorentzVector> rawMup4vect
> > ~~~
> {: .solution2}
> How do you get the `pt` of the first muon, for example?
>
> consider, briefly, how you might access this information before looking at the solution
>
> > ### hint
> > Take a look at the root [documentation](https://root.cern.ch/doc/master/classTLorentzVector.html)
> {: .solution2}
> 
> > ### answer
> > ~~~cpp
> > rawMup4vect[0].Pt()
> > ~~~
> > The `Pt()` method of `TLorentzVector` can be found in the root documentation. Below we will also use the `Eta()` method.
> {: .solution2}
{: .checklist}

> ## Challenge: Add event selections to the code
> 
> * Trigger selections: `HLT_Dimuon0_Jpsi3p5_Muon2`, `HLT_Dimuon0_Jpsi_Muon`
> * The transverse momentum of each muon is greater than or equal to 2.0
> * The absolute value of the pseudo-rapidity of each muon is less than or equal to 2.4
> * The total charge of 4 muons is 0
> * The charge of each muon pair is also 0 (Tip: this means that the sum of the charge all muons is also zero)
{: .challenge}

> ## Solution:
>
> > ### Triggers
> ~~~cpp
> > && (TrigThreeMuonJpsi   //2016  Jpsi trigger, 2017B
> >     || TrigThreeMuonJpsi3p5mu2)   //2017 & 2018 Jpsi trigger
> > ~~~
> {: .solution2}
> > ### Eta
> ~~~cpp
> > && fabs(rawMup4vect[0].Eta()) <= 2.4 && fabs(rawMup4vect[1].Eta()) <= 2.4
> > && fabs(rawMup4vect[2].Eta()) <= 2.4 && fabs(rawMup4vect[3].Eta()) <= 2.4
> > ~~~
> {: .solution2}
> > ### Pt
> > ~~~cpp
> > && fabs(rawMup4vect[0].Pt()) >= 2 && fabs(rawMup4vect[1].Pt()) >= 2
> > && fabs(rawMup4vect[2].Pt()) >= 2 && fabs(rawMup4vect[3].Pt()) >= 2
> > ~~~
> {: .solution2}
> > ### Sum of charges
> > ~~~cpp
> > && (fitMuCharge[0] + fitMuCharge[1] + fitMuCharge[2] + fitMuCharge[3]) == 0
> > ~~~
> {: .solution2}
{: .solution}

> ## Challenge: two further selections
> We are interested in looking at the distributions of:
> * 2 pairs of muons with opposite charges 
> * with a mass in the J/psi mass range. 
{: .challenge}

The first of these two selections should be [implemented here](https://github.com/IreneZoi/DAS2024JpsiJpsi/blob/c429c15693d6b5db0d7720387b4ff38db08f8280/eventselection/myntuple.C#L157) while the [second one should be added here](https://github.com/IreneZoi/DAS2024JpsiJpsi/blob/c429c15693d6b5db0d7720387b4ff38db08f8280/eventselection/myntuple.C#L168)


> ## Note
> A simplified solution of looping through the some combinations of muons in the event is implemented in the code
> 
> A paired muon index is defined [here](https://github.com/IreneZoi/DAS2024JpsiJpsi/blob/c429c15693d6b5db0d7720387b4ff38db08f8280/eventselection/myntuple.C#L132)
> and the loop over the combinations starts [here](https://github.com/IreneZoi/DAS2024JpsiJpsi/blob/c429c15693d6b5db0d7720387b4ff38db08f8280/eventselection/myntuple.C#L151).
>
> use the indices assigned in the loop (`muIdxp11, muIdxp12, muIdxp21, muIdxp22`) to look at different pairs of muons
> > ### one muons charge 
> > ~~~cpp
> > fitMuCharge[muIdxp11]
> > ~~~
> {: .solution2}
{: .checklist}

Please take some time to work out a solution and cross check the implementation here:
> ## Solution: two further selections
> > ### 2 pairs of muons with opposite charges 
> > ~~~cpp
> > && (fitMuCharge[muIdxp11] + fitMuCharge[muIdxp12]) == 0
> > && (fitMuCharge[muIdxp21] + fitMuCharge[muIdxp22]) == 0
> > ~~~
> {: .solution2}
> 
> > ### with a mass in the Jpsi mass range. 
> > ~~~cpp
> > && (fitMup4vect[muIdxp11] + fitMup4vect[muIdxp12]).M()>2.95
> > && (fitMup4vect[muIdxp11] + fitMup4vect[muIdxp12]).M()<3.25
> > && (fitMup4vect[muIdxp21] + fitMup4vect[muIdxp22]).M()>2.95
> > && (fitMup4vect[muIdxp21] + fitMup4vect[muIdxp22]).M()<3.25
> > ~~~
> {: .solution2}
{: .challenge}


After implementing selection, we want to look at some distributions

> ## Challenge: filling histograms
> The variables we will focus on in this exercise are:
>    * The mass of each muon pair ([to be added in the code here](https://github.com/IreneZoi/DAS2024JpsiJpsi/blob/c429c15693d6b5db0d7720387b4ff38db08f8280/eventselection/myntuple.C#L162-L163))
>    * The mass of 4 muons ( M(µ1µ2µ3µ4)-M(µ1µ2)-M(µ3µ4)+2*M(J/psi) ) ([to be added in the code here](https://github.com/IreneZoi/DAS2024JpsiJpsi/blob/c429c15693d6b5db0d7720387b4ff38db08f8280/eventselection/myntuple.C#L171))
{: .challenge}
> 
> ## Solutions
> > ### First muon mass pair definition
> > ~~~cpp
> > DiMuonMass1 = (fitMup4vect[muIdxp11] + fitMup4vect[muIdxp12]).M();
> > ~~~
> {: .solution2}
> > ### Second muon mass pair definition
> > ~~~cpp
> > DiMuonMass2 = (fitMup4vect[muIdxp21] + fitMup4vect[muIdxp22]).M();
> > ~~~
> {: .solution2}
> > ### Four muon mass
> > ~~~cpp
> > m4Muon = (fitMup4vect[muIdxp11]+fitMup4vect[muIdxp12]+fitMup4vect[muIdxp21]+fitMup4vect[muIdxp22]).M()
                    - (fitMup4vect[muIdxp11] + fitMup4vect[muIdxp12]).M()
                    - (fitMup4vect[muIdxp21] + fitMup4vect[muIdxp22]).M()
                    + JPSI_MASS + JPSI_MASS;
> > ~~~
> {: .solution2}
{: .solution}

> ## Extra Challenge
> If you have time, you could check the difference in the distributions using the `fitMup4vect` variable instead of the raw one. Do you notice any difference?
{: .challenge}

## Running the code

After editing the `myntuple.C` macro, we need to compile (or recompile) the code in to a shared library.

~~~bash
root -l
~~~

The command line of root will appear:

~~~bash
root [0]
~~~

Next, you need to compile `myntuple.C`.

~~~bash
root [0] .L myntuple.C++
~~~

~~~output
Info in <TUnixSystem::ACLiC>: creating shared library /uscms_data/d3/lchen/cmsdas2024/CMSSW_10_2_5/src/eventselection/./myntuple_C.so
root [1]
~~~

Now we have compiled `myntuple.C`, `myntuple_C.so` have been created. We can begin to run jobs with ntuple files.

> ## Note:
> Several samples have been commented in runJobs_0.C for speed reasons while debugging and testing your exercise. Once you are happy with the code you have implemented you can uncomment all samples. Once you do it, it will take more than 2 hours to complete!! 
{: .checklist}

~~~bash
root [2]  .x runJobs_0.C
~~~

~~~output
Processing runJobs_0.C...
I am running 0th entries out of 1296200 total entries
I am running 10000th entries out of 1296200 total entries
I am running 20000th entries out of 1296200 total entries
I am running 30000th entries out of 1296200 total entries
I am running 40000th entries out of 1296200 total entries
I am running 50000th entries out of 1296200 total entries
I am running 60000th entries out of 1296200 total entries
I am running 70000th entries out of 1296200 total entries
I am running 80000th entries out of 1296200 total entries
I am running 90000th entries out of 1296200 total entries
......
root [3]
~~~

to exit the root command line use:

~~~bash
root [3] .q
~~~

Finally, we can get a root file named `myhbk.root` and a txt file named `mJJDataFull6000_15000.txt`.

You can draw histograms defined in `myntuple.C`.

~~~bash
root -l myhbk.root
~~~

~~~output
root [0] 
Attaching file myhbk.root as _file0...
(TFile *) 0x4559af0
~~~

~~~bash
root [1] .ls
~~~

~~~output
 TFile**      myhbk.root   
 TFile*      myhbk.root   
  KEY: TH1F   myDiMuon1mass;1   myDiMuon1mass
  KEY: TH1F   myDiMuon2mass;1   myDiMuon2mass
  KEY: TH1F   myFourMuonmass;1   myFourMuonmass
~~~

Then you can see any histogram (TH1F).

~~~bash
root [2] myFourMuonmass->Draw()
~~~

{% include links.md %}
