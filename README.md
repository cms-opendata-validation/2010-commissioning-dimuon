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


------------------------------------------
HOW TO INSTALL a CERN VIRTUAL MACHINE(VM)|
------------------------------------------
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

   You need to work in the CERN VM properly contextualized for CMS, this VM is 
available on the CERN Open Data Portal (http://opendata.cern.ch/record/250). 
Download the CMS CERN VM image as (.ova) file.
   For CERN VM you need to have VirtualBox. In case that you do not have it, you 
can download it from the Downloads page (https://www.virtualbox.org/wiki/Downloads).

