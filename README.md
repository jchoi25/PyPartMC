# PyPartMC (pre-alpha!)

PyPartMC is a Python interface to [PartMC](https://lagrange.mechse.illinois.edu/partmc/), 
  a particle-resolved Monte-Carlo code for atmospheric aerosol simulation.
Since PyPartMC is implemented in C++, it also constitutes a C++ API to the PartMC Fortran internals;
  the Python API can be used from other environments (see Julia, Matlab and C++ example snippets below).

[![US Funding](https://img.shields.io/static/v1?label=US%20DOE%20Funding%20by&color=267c32&message=ASR&logoWidth=25&logo=image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAB4AAAAQCAMAAAA25D/gAAAABGdBTUEAALGPC/xhBQAAACBjSFJNAAB6JgAAgIQAAPoAAACA6AAAdTAAAOpgAAA6mAAAF3CculE8AAAASFBMVEVOTXyyIjRDQnNZWINZWITtzdFUU4BVVIFVVYHWiZM9PG/KZnNXVoJaWYT67/FKSXhgX4hgX4lcW4VbWoX03uHQeIN2VXj///9pZChlAAAAAWJLR0QXC9aYjwAAAAd0SU1FB+EICRMGJV+KCCQAAABdSURBVBjThdBJDoAgEETRkkkZBBX0/kd11QTTpH1/STqpAAwWBkobSlkGbt0o5xmEfqxDZJB2Q6XMoBwnVSbTylWp0hi42rmbwTOYPDfR5Kc+07IIUQQvghX9THsBHcES8/SiF0kAAAAldEVYdGRhdGU6Y3JlYXRlADIwMTctMDgtMDlUMTk6MDY6MzcrMDA6MDCX1tBgAAAAJXRFWHRkYXRlOm1vZGlmeQAyMDE3LTA4LTA5VDE5OjA2OjM3KzAwOjAw5oto3AAAAABJRU5ErkJggg==)](https://asr.science.energy.gov/)
[![License: GPL v3](https://img.shields.io/badge/License-GPL%20v3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0.html)
[![Copyright](https://img.shields.io/static/v1?label=Copyright&color=249fe2&message=UIUC&)](https://atmos.illinois.edu/)
[![Maintenance](https://img.shields.io/badge/Maintained%3F-yes-green.svg)](https://GitHub.com/open-atmos/PyPartMC/graphs/commit-activity)
[![Github Actions Build Status](https://github.com/open-atmos/PyPartMC/workflows/tests/badge.svg?branch=main)](https://github.com/open-atmos/PyPartMC/actions)
[![API docs](https://img.shields.io/badge/API_docs-pdoc3-blue.svg)](https://open-atmos.github.io/PyPartMC/)


## TL;DR (try in a Jupyter notebook)

[![Python 3](https://img.shields.io/static/v1?label=Python&logo=Python&color=3776AB&message=3)](https://www.python.org/)
[![Linux OK](https://img.shields.io/static/v1?label=Linux&logo=Linux&color=yellow&message=%E2%9C%93)](https://en.wikipedia.org/wiki/Linux)
[![macOS OK](https://img.shields.io/static/v1?label=macOS&logo=Apple&color=silver&message=%E2%9C%93)](https://en.wikipedia.org/wiki/macOS)
[![Windows OK](https://img.shields.io/static/v1?label=Windows&logo=Windows&color=white&message=%E2%9C%93)](https://en.wikipedia.org/wiki/Windows)
[![Jupyter](https://img.shields.io/static/v1?label=Jupyter&logo=Jupyter&color=f37626&message=%E2%9C%93)](https://jupyter.org/)

```python
! pip install git+https://github.com/open-atmos/PyPartMC.git
import PyPartMC
```

## Features

- works on Linux, macOS and Windows (compatibility assured with [CI builds](https://github.com/open-atmos/PyPartMC/blob/main/.github/workflows/tests.yml))
- hassle-free installation using `pip` (prior PartMC installation **not needed**)
- works out of the box on [mybinder.org](https://mybinder.org/), [Google Colab](colab.research.google.com/) and alike
- ships with [a set of examples](https://github.com/open-atmos/PyPartMC/tree/main/examples) maintained in a form of Jupyter notebooks
- Pythonic API (but retaining PartMC jargon) incl. exceptions and GC deallocation of Fortran objects 
- code snippets in README depicting how to used PyPartMC in Julia & Matlab (also executed on CI)
- auto-generated [docs on the web](https://open-atmos.github.io/PyPartMC/)
- support for [de]serialization of all exposed structures using JSON 
- based on [unmodified PartMC code](https://github.com/open-atmos/PyPartMC/tree/main/gitmodules)
- does not use or require shell or netCDF Fortran library
- aiming at 100% [unit test coverage](https://github.com/open-atmos/PyPartMC/tree/main/tests)

## Usage examples

#### example object instantiation in Python

```python
import PyPartMC as ppmc
print(ppmc.__version__)
gas_state = ppmc.GasState()
# ... TODO
```

#### example object instantiation in C++
```c++
//... TODO
```

#### example object instantiation in Julia
```Julia
using Pkg
Pkg.add("PyCall")

using PyCall
ppmc = pyimport("PyPartMC")
print(ppmc.__version__)
GasState = ppmc.GasState
gas_state = GasState()
#... TODO
```

#### example object instantiation in Matlab

Note that since Matlab ships with and prioritizes its own GCC libraries (`libgfortran.so`, 
  `libstdc++.so`, `libgcc_s.so`, `libquadmath.so`), it is essential to build PyPartMC
  with the [same version of GCC as the one Matlab files are based on](https://www.mathworks.com/matlabcentral/answers/100812-is-there-a-web-page-that-lists-the-version-of-libstdc-so-used-for-building-each-matlab-version).

```Matlab
ppmc = py.importlib.import_module('PyPartMC');
ver = char(py.getattr(ppmc, "__version__"))
system(['ldd ' char(py.getattr(ppmc, "__file__"))]) 
%GasState = ppmc.GasState;
%gas_state = GasState();
% ... TODO
```

#### Jupyter notebooks with examples

... TODO ... [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/open-atmos/PyPartMC/blob/main/examples/hello_world.ipynb)

#### usage in other projects

PyPartMC is also used within the tests of PySDM project ... TODO

## Implementation outline

- PyPartMC is written in C++, Fortran and Python and uses [pybind11](https://pybind11.readthedocs.io/en/stable/) and [CMake](https://cmake.org/).
- JSON support is handled with [nlohmann::json](https://github.com/nlohmann/json) and [pybind11_json](https://github.com/pybind/pybind11_json)
- PartMC and selected parts of SUNDIALS are compiled during `pip install` and statically linked
- C (SUNDIALS), C++ (pybind11, ...) and Fortran (PartMC) dependencies are linked through [git submodules](https://github.com/open-atmos/PyPartMC/blob/main/.gitmodules)
- a [mock of Fortran netCDF API](https://github.com/open-atmos/PyPartMC/blob/main/src/fake_netcdf.F90) is used for i/o from/to JSON using existing netCDF API calls within PartMC
- a [mock of Fortran MPI API](https://github.com/open-atmos/PyPartMC/blob/main/src/fake_mpi.F90) is used for error handling using existing MPI API calls within PartMC

## Troubleshooting 

#### Common installation issues 
```
error: [Errno 2] No such file or directory: 'cmake'
```
Try rerunning after installing CMake (e.g., `apt-get install cmake` or `brew install cmake`)

#### How to debug
```sh
git clone --recursive git+https://github.com/open-atmos/PyPartMC.git
cd PyPartMC
DEBUG=1 VERBOSE=1 pip --verbose install -e .
gdb python 
(gdb) run -m pytest -s tests
```

## Credits

#### PyPartMC:

author: [Sylwester Arabas](https://www.ii.uj.edu.pl/~arabas/)   
funding: [US Department of Energy Atmospheric System Research programme](https://asr.science.energy.gov/)   
copyright: [University of Illinois at Urbana-Champaign](https://atmos.illinois.edu/)   
licence: [GPL v3](https://www.gnu.org/licenses/gpl-3.0.en.html)

#### PartMC:
authors: [Nicole Riemer](https://www.atmos.uiuc.edu/~nriemer/), [Matthew West](https://lagrange.mechse.illinois.edu/mwest/), [Jeff Curtis](https://publish.illinois.edu/jcurtis2/) et al.   
licence: [GPL v2](https://www.gnu.org/licenses/old-licenses/gpl-2.0.html) or later

