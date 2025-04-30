# mstool

[mstool](https://mstool.readthedocs.io/en/latest/#) is a multiscale simulation tool that converts a coarse-grained structure into an all-atom structure. It requires minimal user input (mapping and isomeric information of molecules). For more details, please check out the [paper](https://pubs.acs.org/doi/10.1021/acs.jpcb.3c05593) and [documentation](https://mstool.readthedocs.io/en/latest/#).


## difference of original version

### Installation

```
git clone https://github.com/yteshirogi/mstool.git
cd mstool
pip install .
```

### some bug fix

## usage

### file tree
```
/your/working/dir
|--yourinputfile.pdb
|--leap.in
|--memb_mstools.py
|--run.sh
|--vmd_box_dims.sh
```

As an example of `run.sh`
```
#!/bin/bash
#SBATCH --nodes=1
#SBATCH -n 1
#SBATCH -c 28
#SBATCH --gpus=1
#SBATCH --qos=normal
#SBATCH --job-name mstool

# run
source ~/miniconda3/bin/activate mstools

rm -r workdir
export OPENMM_PLUGIN_DIR=""
python3 memb_mstools.py

cd workdir
charmmlipid2amber.py -i step7_final.pdb -o step7_final_amber.pdb
cp ../leap.in .
../vmd_box_dims.sh -i step7_final_amber.pdb -s water
```

