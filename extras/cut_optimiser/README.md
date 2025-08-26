## How To Use Traccc Cut Optimiser on lxplus or EF Tracking testbed

The issue is that when we setup an Athena version, the python is taken from ```/cvmfs/```. This optimisation requires the ```uv``` package, but installing through ```pip``` places it in your ```.local``` directory. Therefore when running the ```uv``` command, it will complain it does not find the python encodings, because it's not using the right python. To reconcile this, you have to run figure out where ```uv``` lives (```find ~ -name uv```), then run something like:

```bash
/afs/cern.ch/user/n/nribaric/.local/bin/uv run --python /cvmfs/atlas-nightlies.cern.ch/repo/sw/main_Athena_x86_64-el9-gcc14-opt/sw/lcg/releases/LCG_108_ATLAS_1/Python/3.12.11/x86_64-el9-gcc14-opt/bin/python main.py ../../../build-traccc/bin/traccc_seeding_example_cuda testing.csv test.json --num-sm 1 --num-threads-per-sm 1
```

I have also modified:
- the ```myproject.toml``` to require python 3.12. since this is the latest available python through ```LCG_108_ATLAS_1```
- the ```main.py``` run script to set ```use-acts-geo-source=off``` since with the ITk data we have generated it using detray module IDs