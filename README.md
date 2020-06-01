# EFT Sample Production for VVV Analysis
Tools, scripts and documentation to generate VVV samples for triboson analysis.

## Setup

1. Get a `CMSSW_10_2_22` environment.

2. Download Madgraph and quartic coupling model:
   ```bash
   wget https://launchpad.net/mg5amcnlo/2.0/2.6.x/+download/MG5_aMC_v2.6.7.tar.gz
   tar -xf MG5_aMC_v2.6.7.tar.gz
   cd MG5_aMC_v2_6_7
   cd models
   wget --no-check-certificate https://cms-project-generators.web.cern.ch/cms-project-generators/SM_Ltotal_Ind5v2020v2_UFO.zip
   unzip SM_Ltotal_Ind5v2020v2_UFO.zip
   cd ../..
   ```

3. Generate reweighting card (check out file for description of grid):
   ```
   python scripts/make_reweighting_card.py
   ```

4. Command Madgraph:
   ```
   import model SM_Ltotal_Ind5v2020v2_UFO
   define wpm = w+ w-
   generate p p > z z z NP=1
   output zzz
   launch
   ```
   Make the following edits in the cards:
   * enable madspin
   * set to 100k events
   * set nominal values of anomalous parameters to zero, except for FT9 to 5.0e-12
     such that the high mass tails are sufficiently populated.
   * copy-paste the reweighting commands generated by the python script into the reweighting card

   This should be done also for WWW, WWZ, WZZ and not only ZZZ.

