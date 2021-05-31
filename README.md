# integrate-external-project-with-llvm-libraries
Make use of the libraries provided by LLVM framework, and create your own tool on top of that.

# Steps to build
```bash
git clone https://github.com/Sameeranjoshi/integrate-external-project-with-llvm-libraries.git
mkdir build && cd build
cmake ../integrate-external-project-with-llvm-libraries
make
```

# Check your build
```bash
cd build
./myoutoftreetool --help
```
Note: You need `llvm` compiler setup in your environment.
The tool does nothing just uses one of the LLVM based libraries.
