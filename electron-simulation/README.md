 # example from AnaEx01

 This example is a modified version of the AnaEx01 in the "extended" folder
 of the Geant4 examples.
                            
 Examples AnaEx01, AnaEx02 and AnaEx03 show the usage of histogram and tuple 
 manipulations using G4Analysis, ROOT and AIDA compliant systems on the same
 scenario. All analysis manipulations (histo booking, filling, saving histos 
 in a file, etc...) are located in one class : HistoManager, implementation of 
 which is different in each example. All the other classes are same in all 
 three examples.
 
 This example shows the usage of histogram and tuple manipulations using 
 G4Analysis system. 
 
 The example is an adaptation of examples/novice/N03. It describes a simple 
 sampling calorimeter setup.
	
## Detector description ##
 
 The calorimeter is a box made of a given number of layers. A layer
 consists of an absorber plate and of a detection gap. The layer is
 replicated.
 	
 Six parameters define the calorimeter :
    * the material of the absorber,
    * the thickness of an absorber plate,
    * the material of the detection gap,
    * the thickness of a  gap,
    * the number of layers,
    * the transverse size of the calorimeter (the input face is a square). 
 
 The default geometry is constructed in DetectorConstruction class,
 but all of the above parameters can be modified interactively via
 the commands defined in the DetectorMessenger class.

```
        |<----layer 0---------->|<----layer 1---------->|<----layer 2---------->|
        |                       |                       |                       |
        ==========================================================================
        ||              |       ||              |       ||              |       ||
        ||              |       ||              |       ||              |       ||
 beam   ||   absorber   |  gap  ||   absorber   |  gap  ||   absorber   |  gap  ||
======> ||              |       ||              |       ||              |       ||
        ||              |       ||              |       ||              |       ||
        ==========================================================================
```   
   
 ## Physics list ##
 
 
   The particle's type and the physic processes which will be available
   in this example are set in the FTFP_BERT physics list.
  
 ## Action Initialization ##

   A newly introduced class, ActionInitialization, 
   instantiates and registers to Geant4 kernel all user action classes 
   which are defined thread-local and a run action class
   which is defined both thread-local and global.
   
   The thread-local action classes are defined in 
     ActionInitialization::Build() 
   and  the global run action class is defined in 
     ActionInitialization::BuildForMaster().
   Note that ActionInitialization::Build() is also used to 
   instatiate user action clasess in sequential mode.
  
 ## An event: PrimaryGeneratorAction ##

   Primaries are generated with the General Particle Source (GPS)
   http://geant4-userdoc.web.cern.ch/geant4-userdoc/UsersGuides/ForApplicationDeveloper/html/GettingStarted/generalParticleSource.html
   therefore all the configuration of the primaries can be done via macro

 ## Histograms ##

 AnaEx01 can produce 4 histograms :
  
  EAbs : total energy deposit in absorber per event
  EGap : total energy deposit in gap per event	  
  LAbs : total track length of charged particles in absorber per event 	
  LGap : total track length of charged particles in gap per event 
 
 And 2 Ntuples :
 * Ntuple1:
   ..* one row per event : EnergyAbs EnergyGap
 * Ntuple2:
   ..* one row per event : TrackLAbs TrackLGap
  
 These histos and ntuples are booked in HistoManager and filled from 
 EventAction.
 
 One can control the name of the histograms file and its format:
 default name     : AnaEx01   
 The format of the histogram file can be : root (default),
 xml, csv. Include correct g4nnn.hh in HistoManager.hh 
 
 ## How to build ## 

 `mkdir <build dir>`
 
 `cd <build dir>`
 
 `cmake ../AnaEx01`
 
 `make`
