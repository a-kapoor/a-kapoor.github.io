# Pythia8 -> hepmc -> root

The following instructions are for generating a sample physics process in pythia8 and converting the generated events into a root TTree.

We will need pythia8, hepmc2 and root. We can use conda to create a virtual environment 

Follow these instructions:
conda create --name pythia8withhepmc2
conda activate pythia8withhepmc2
conda install -c conda-forge hepmc2 pythia8 
conda install -c conda-forge root

Within this enviroment, to generate a hepmc2 file, here is a pythia8 example (let us call in pythia8.C):

```cpp

#include "TSystem.h"
#include "TH1F.h"
#include "TClonesArray.h"
#include "TPythia8.h"
#include "Pythia8Plugins/HepMC2.h"
#include "TParticle.h"
#include "TDatabasePDG.h"
#include "TCanvas.h"

void pythia8(Int_t nev  = 100, Int_t ndeb = 1)
{
  // Load libraries
  gSystem->Load("libEG");
  gSystem->Load("libEGPythia8");
  // Histograms
  // Array of particles
  TClonesArray* particles = new TClonesArray("TParticle", 1000);
  // Create pythia8 object
  TPythia8* pythia=new TPythia8();
  HepMC::Pythia8ToHepMC toHepMC;
  HepMC::IO_GenEvent ascii_io("file.hepmc");
  //HepMC::WriterRootTree WriterRootfile("file.root")
  HepMC::GenEvent hepmcevt;
#if PYTHIA_VERSION_INTEGER == 8235
  // Pythia 8.235 is known to cause crashes:
  printf("ABORTING PYTHIA8 TUTORIAL!\n");
  printf("The version of Pythia you use is known to case crashes due to memory errors.\n");
  printf("They have been reported to the authors; the Pythia versions 8.1... are known to work.\n");
  return;
#endif
  // Configure
  pythia->ReadString("HardQCD:all = on");
  pythia->ReadString("Random:setSeed = on");
  // use a reproducible seed: always the same results for the tutorial.
  pythia->ReadString("Random:seed = 42");
  // Initialize
  pythia->Initialize(2212 /* p */, 2212 /* p */, 14000. /* TeV */);
  // Event loop
  for (Int_t iev = 0; iev < nev; iev++) {
    pythia->GenerateEvent();
    if (iev < ndeb) pythia->EventListing();
    pythia->ImportParticles(particles,"All");
    Int_t np = particles->GetEntriesFast();
      
    HepMC::GenEvent* hepmcevt = new HepMC::GenEvent();
    toHepMC.fill_next_event( *pythia->Pythia8(), hepmcevt);
    ascii_io << hepmcevt;
    delete hepmcevt;
  pythia->PrintStatistics();
  }
}
```

Run it using 

```bash=
root -l pythia8.C
```

This will give you a hepmc2 file ```file.hepmc```


Then clone my repo (originally from hbprosper) and set it up

```bash=
git clone git@github.com:akapoorcern/hepmc2root.git
cd hepmc2root
chmod +x setup.sh
source setup.sh
```

Then go to bin directory and run
```bash=
python hepmc2root.py <path to hepmc file>
```

This will convert your pythia8 generated events to a root TTree.
    
    




