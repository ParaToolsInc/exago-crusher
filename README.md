# ExaGO on OLCF Crusher
ROCm-enabled ExaGO on OLCF Crusher using Spack

## Install from Build Cache (Example)
* View a demo video of these instructions run at https://asciinema.org/a/508123
```
$crusher:~> git clone https://github.com/ParaToolsInc/exago-crusher.git
$crusher:~> cd exago-crusher

$crusher:~/exago-crusher> git clone https://github.com/spack/spack
$crusher:~/exago-crusher> (cd spack && git checkout dac31ef3c)

$crusher:~/exago-crusher> export SPACK_DISABLE_LOCAL_CONFIG=1
$crusher:~/exago-crusher> export SPACK_USER_CACHE_PATH=$(pwd)/_cache
$crusher:~/exago-crusher> . spack/share/spack/setup-env.sh

$crusher:~/exago-crusher> spack mirror add paratools /gpfs/alpine/csc439/world-shared/E4S/ParaTools/exago
$crusher:~/exago-crusher> spack buildcache keys -it
gpg: key 4345F04B40005581: public key "University of Oregon - E4S" imported
gpg: Total number processed: 1
gpg:               imported: 1
gpg: inserting ownertrust of 6

$crusher:~/exago-crusher> time spack -e . concretize -f | tee concretize.log
... output truncated for brevity; see concretize.log in this repo for full output
real	0m46.340s
user	1m25.263s
sys	0m2.094s

$crusher:~/exago-crusher> time spack -e . install --cache-only
... output truncated for brevity
real	7m40.626s
user	4m44.081s
sys	0m33.864s

$crusher:~/exago-crusher> spack find -lv exago hiop ipopt coinhsl
==> 8 installed packages
-- cray-sles15-zen3 / gcc@11.2.0 --------------------------------
ue74alo coinhsl@2015.06.23+blas
mnelc7u exago@develop~cuda+hiop~ipo~ipopt+mpi+python+raja+rocm amdgpu_target=gfx90a build_type=RelWithDebInfo
anahf5s exago@develop~cuda+hiop~ipo~ipopt+mpi+python+raja+rocm amdgpu_target=gfx90a build_type=RelWithDebInfo
2qog6zw exago@develop~cuda+hiop~ipo+ipopt+mpi+python+raja+rocm amdgpu_target=gfx90a build_type=RelWithDebInfo
dr3jlyb exago@develop~cuda+hiop~ipo+ipopt+mpi+python+raja+rocm amdgpu_target=gfx90a build_type=RelWithDebInfo
wtqj2hu hiop@0.6.2~cuda~cusolver~deepchecking~ginkgo~ipo~jsrun~kron+mpi+raja+rocm~shared+sparse amdgpu_target=gfx90a build_type=RelWithDebInfo
rlw4qhu hiop@0.6.2~cuda~cusolver~deepchecking~ginkgo~ipo~jsrun+kron+mpi+raja+rocm~shared+sparse amdgpu_target=gfx90a build_type=RelWithDebInfo
ufjh4v7 ipopt@3.14.5+coinhsl~debug+metis~mumps
```
