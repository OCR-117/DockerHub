FROM        --platform=$TARGETOS/$TARGETARCH ubuntu:22.04

LABEL       author="Aurélien Delval-Carbonne" maintainer="aurelien.delval-carbonne@epita.fr"

# General Dependencies.
RUN 		apt update -y \
      		&& apt install -y build-essential git graphviz g++-multilib llvm python-is-python3 valgrind \
  			&& apt install -y autoconf autoconf-archive automake bison clang clang-format doxygen flex gawk ghc libboost-dev libboost-graph-dev libboost-program-options-dev libboost-system-dev libreadline-dev libtool texinfo xsltproc

# ARM compilation & virtual machine.
RUN 		apt install -y gcc-arm-linux-gnueabihf libc6-dev-armhf-cross qemu-user

# Reflex.
RUN         git clone https://github.com/Genivia/RE-flex.git && cd RE-flex/ && ./clean.sh && ./build.sh && ./allinstall.sh && cd ../

# Havm.
RUN         git clone https://gitlab.lre.epita.fr/tiger/havm.git && cd havm/ && ./bootstrap && ./configure && make && make check && make install && cd ../

# Nolimips.
RUN         git clone https://gitlab.lre.epita.fr/tiger/nolimips.git && cd nolimips/ \
			&& sed -i "s/^AX_CXX_COMPILE_STDCXX.*$//" configure.ac \
			&& sed -i "s/^AX_COMPILER_FLAGS.*$//" configure.ac \
			&& ./bootstrap && ./configure && make && make check && make install && cd ../

SHELL ["/bin/bash", "-c"]
