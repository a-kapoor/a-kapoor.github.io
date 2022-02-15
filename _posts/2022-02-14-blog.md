# Basic NanoAOD analysis script

```python=
#!/usr/bin/env python

files='/eos/cms/store/group/phys_egamma/akapoor/ChargeMisID/newsamples/*.root'

import ROOT
import os
ROOT.gStyle.SetPalette(ROOT.kOcean);
ROOT.ROOT.EnableImplicitMT()

def selection_2el2mu(df):
    df = df.Filter("nElectron==2", "Exactly two electrons")
    df = df.Define("GoodElectrons", "(Electron_pt > 10) && (Electron_mvaTTH > 0.8) && (Electron_cutBased > 2)")
    df = df.Filter("Sum(GoodElectrons) == 2","Exactly two good electrons")
    df = df.Define("Dielectron_mass", 
                   "InvariantMass(Electron_pt[GoodElectrons], Electron_eta[GoodElectrons], Electron_phi[GoodElectrons], Electron_mass[GoodElectrons])")
    df = df.Filter("(Dielectron_mass<111) && (Dielectron_mass>71)","Z mass cut")
    
    return df

df = ROOT.RDataFrame("Events", files)
dfsel=selection_2el2mu(df)
report = dfsel.Report()
report.Print()

h1 = dfsel.Filter("Sum(Electron_charge)==0", "Two OS").Histo1D(("Dielectron_mass", "Dielectron_mass;m_{ee} (GeV);Events", 300, 71, 111), "Dielectron_mass")
h2 = dfsel.Histo1D(("Dielectron_mass_all", "Dielectron_mass;m_{ee} (GeV);Events", 300, 71, 111), "Dielectron_mass")

ROOT.gStyle.SetOptStat(0); ROOT.gStyle.SetTextFont(42)
c = ROOT.TCanvas("c", "", 800, 700)
c.SetLogy()
h1.SetTitle("")
h1.GetXaxis().SetTitleSize(0.04)
h1.GetYaxis().SetTitleSize(0.04)
h1.Draw("")
c.SaveAs("dielectron_spectrum.pdf")
dfos=dfsel.Filter("Sum(Electron_charge)==0", "Two OS")
report = dfos.Report()
report.Print()
```

Save it as maybe "ChargeFlip.py" and run
```bash=
python ChargeFlip.py
```