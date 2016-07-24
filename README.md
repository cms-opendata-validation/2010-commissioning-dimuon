----------------------------
# 2010-commissioning-dimuon|
                           - -------------------------------------------------
Validation code for 2010 Commissioning dataset, based on dimuon mass spectrum|
------------------------------------------------------------------------------

   How to install and run the validation benchmark of the Commissioning data set?
This code for validation and benchmarking of the Commissioning data set, based on
the dimuon mass spectrum, does NOT apply JSON preselection. It therefore includes 
benchmarking of non-JSON selected runs. 
   It is set up at Research level what means, that it requires university student 
level programming experience. Minimal acquaintance with Linux, the ROOT analysis
peckage (http://root.cern.ch/) and basic text editor is assumed in the following.


----------------------------------------------
1.) HOW TO INSTALL a CERN VIRTUAL MACHINE(VM)|
----------------------------------------------
NOTES: (it is better to read them before you start)
-----
   NOTE_1:You will need administrative("root") privileges on every platform to 
perform the installation of VirtualBox.
   NOTE_2:The latest tested version of VirtualBox working with CMS-CERN VM 
image is 4.3.14. If you have troubles with the latest version of VirtualBox, 
pick that one. The full history of VirtualBox version is available on different 
page: (https://www.virtualbox.org/wiki/Downloads).
   NOTE_3:Before you download the CERN VM, note that the imported settings may 
not always work on your host machine. Please see Issues and Limitations on this 
page: (http://opendata.cern.ch/VM/CMS/2010#issues) if you encounter any problems 
with booting the CERN VM.

STEPS: 
-----
   You need to work in the CERN VM properly contextualized for CMS, this VM is 
available on the CERN Open Data Portal (http://opendata.cern.ch/record/250). 
Download the CMS CERN VM image as (.ova) file.
   For CERN VM you need to have VirtualBox. In case that you do not have it, you 
can download it from the Downloads page (https://www.virtualbox.org/wiki/Downloads).
   When VirtualBox is installed saccessfully you can go on. By double clicking the
downloaded file, VirtualBox imports the image with ready to run settings. In case
of any problem with booting with these default settings, see ISSUES AND LIMITATIONS:
(http://opendata.cern.ch/VM/CMS/2010#issues). Then, you launch the CMS CERN VM, which 
boots into the graphical user interface and sets up the CMS enviroment.


-------------------------------------------------------
2.) SET UP THE CMS ENVIRONMENT AND RUN A DEMO ANALYZER|
-------------------------------------------------------
a.) Open a terminal with the X terminal emulator(an icon bottom-left of the VM screen) 
and ecexute the following command: cmsrel CMSSW_4_2_8
this command builds the local release are for CMSSW, and only needs to be run once.
b.)  Then, change directory to the CMSSW_4_2_8/src/ with command: cd CMSSW_4_2_8/src/
c.)  Then, run the following command to create the CMS runtime variable: cmsenv
d.)  Create a working directory for the demo analyzer: mkdir Demo
e.)  Then, change directory: cd Demo
f.)  Create a "skeleton" for the analyzer: mkedanlzr DemoAnalyzer
g.)  Change directory: cd DemoAnalyzer
h.)  Compile: scram b
i.)  For testing, change the file name in the configuration file (demoanalyzer_cfg.py) 
     in DemoAnalyzer directory:i.e. replace (file:myfile.root) with following file,
     (root://eospublic.cern.ch//eos/opendata/cms/Run2010B/Mu/AOD/Apr21ReReco-v1/0000/00459D48-EB70-E011-AF09-90E6BA19A252.root)
     and also change the max number of evetns to 10:i.e. change -1 to 10 in 
     (process.maxEvents = cms.untracked.PSet( input = cms.untracked.int32(-1)).
     This point (i) is not necessary, just to be sure.
j.)  Then, move two directories back using: cd ../..
k.)  And then run: cmsRun Demo/DemoAnalyzer/demoanalyzer_cfg.py
Your output should end with: System 3 3
If everything works you can go on.

--------------------------
3.)  COMMISSIONING DIMUON|
--------------------------
   In DemoAnalyzer directory, create datasets directory using this command: mkdir datasets

In the downloaded 2010-commissioning-dimuon repository from github are also index files with names:
 CMS_Run2010B_Commissioning_AOD_Apr21ReReco-v1_0000_file_index.txt
 CMS_Run2010B_Commissioning_AOD_Apr21ReReco-v1_0002_file_index.txt
 CMS_Run2010B_Commissioning_AOD_Apr21ReReco-v1_0003_file_index.txt
 CMS_Run2010B_Commissioning_AOD_Apr21ReReco-v1_0004_file_index.txt   
Store these four files in Demo/DemoAnalyzer/datasets

In this repository are also these files:
 demoanalyzer_cfg.py
 DemoAnalyzer.cc
 BuildFile.xml 
In DemoAnalyzer directory are files with the same names. DemoAnalyzer.cc is in /DemoAnalyzer/src/DemoAnalyzer.cc directory.
Replace these three files from DemoAnalyzer directory by the ones from github repository.
For opening BuildFile.xml file is better to use terminal with command: vim BuildFile.xml
When you open it with double clicking with mouse, this problem appers: (XML Parsing Error:syntax error)
and you will not be able to read text in this file. The way how to solve this problem is not complicated. 
Just press (ctrl+u) when you are on this page. After that, a new window will be opened with text that you need.

When you replace files, it is necessary to recompile. In you terminal you should be in DemoAnalyze directory, 
if not go there. Execute command: scram b
Than, move two directories back with command: cd ../..
Rerun with command: cmsRun Demo/DemoAnalyzer/demoanalyzer_cfg.py
 
You should get an output file Commissioning00.root which contains histograms for all the 
files/events in the CMS_Run2010B_Commissioning_AOD_Apr21ReReco-v1_0000_file_index.txt index file.
These can be looked at using a ROOT Browser. Just type in terminal command: root
Then, type in this same window: new TBrowser
A new window appears. In this window you can find your created root file.
When you want to leave from ROOT, just type command: .q

This is the validation of a Commissioning sample, not dedicated to muon final states,
so the number of events entering the mass plot is relatively small. To run over the full
statistics, edit the relevant parts of the Python file demoanalyzer_cfg.py . 
These relevant parts of this code are located in section where we define the input data
and where we define output file.
This part where we define input data starts with this:
# ****************************************************************************
# define the input data set here by inserting the appropriate .txt file list *
# ****************************************************************************
There you must find the line where you define the file what will be loaded. This line seems like this:
files2010data = FileUtils.loadListFromFile ('/home/cms-opendata/CMSSW_4_2_8/src/Demo/DemoAnalyzer/datasets/CMS_Run2010B_Commissioning_AOD_Apr21ReReco-v1_0000_file_index.txt')
There you just replace part 0000 by 0002 .
Similar thigs you must do with output file. At the end of this file is a part for this. 
Just replace Commissioning00val.root by Commissioning02val.root and save these changes.
After that, just rerun. Do this for all index file. When you do this you should have four root files with names:
 Commissioning00val.root
 Commissioning02val.root
 Commissioning03val.root
 Commissioning04val.root

The last thing what you should do is to merge these four root files into one root file.
You do this as follow. In the downloaded repository is also file with name mergeCommissioning.C .
Copy this file into the directory where these four root files are located. Then, press command: root
for entering into ROOT programme. In this programe just type command: .x mergeCommissioning.C .
This merging create a root file called CommissioningAllval.root.

Look at this output with command: new TBrowser
and navigate to relevant file.
