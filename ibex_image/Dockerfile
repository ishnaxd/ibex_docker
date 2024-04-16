# Use Ubuntu 20.04 as the base image
FROM ubuntu:20.04

# Update package lists and install dependencies
RUN apt-get update && apt-get upgrade -y \
    && apt-get install -y git wget make g++ help2man perl python3 autoconf flex bison zlib1g zlib1g-dev \
    && apt-get install -y apt-utils libfl2 libfl-dev ccache libgoogle-perftools-dev numactl perl-doc \
    && apt-get install -y gcc build-essential libelf-dev srecord python3-pip

# Create directory structure and clone repositories
RUN mkdir /home/FYP && cd /home/FYP \
    && mkdir FYP && cd FYP \
    # && git clone https://github.com/lowRISC/ibex \
    && git clone https://github.com/ishnaxd/ibex \
    && cd ibex

# Install additional dependencies
RUN apt-get install -y git help2man perl python3 make \
    && apt-get install -y g++ \
    && apt-get update \
    && apt-get install -y apt-utils \
    && apt-get install -y libfl2 \
    && apt-get install -y libfl-dev \
    && apt-get install -y ccache \
    # && apt-get install -y mold \
    && apt-get install -y libgoogle-perftools-dev numactl \
    && apt-get install -y perl-doc \
    && apt-get install -y git autoconf flex bison \
    && apt-get install -y zlib1g zlib1g-dev \
    && apt-get update 
    # && apt-get install -y mold

    # Setup SystemC
    RUN cd /home/FYP/FYP/ibex \
    && wget http://accellera.org/images/downloads/standards/systemc/systemc-2.3.3.tar.gz \
    && tar -xvzf systemc-2.3.3.tar.gz \
    && cd systemc-2.3.3 \
    && mkdir objdir \
    && cd objdir \
    && export CXX=g++ \
    && ../configure \
    && make \
    && make install \
    && cd .. \
    && rm -rf objdir \
    && cd .. \
    && export SYSTEMC_INCLUDE="/home/FYP/FYP/ibex/systemc-2.3.3/src/" \
    && export LD_LIBRARY_PATH="/home/FYP/FYP/ibex/systemc-2.3.3/lib-linux64/:$LD_LIBRARY_PATH" \
    && export SYSTEMC_LIBDIR="/home/FYP/FYP/ibex/systemc-2.3.3/lib-linux64/"

# Setup Verilator
RUN cd /home/FYP/FYP/ibex \
    && git clone https://github.com/verilator/verilator \
    && cd verilator \
    && git pull \
    && unset VERILATOR_ROOT \
    && autoconf \
    && ./configure \
    && make -j $(nproc) \
    && make test \
    && make install \
    && cd ..

# Download LowRISC toolchain

# RUN pwd
RUN apt-get update && apt-get install -y tree \
 && tree 


RUN cd /home/FYP/FYP/ibex \
 && apt-get install python3-pip \
     && pip3 install -U -r python-requirements.txt


 RUN cd /home/FYP/FYP/ibex \
    && wget https://github.com/lowRISC/lowrisc-toolchains/releases/download/20240206-1/lowrisc-toolchain-gcc-rv32imcb-20240206-1.tar.xz \
     && tar -xvf lowrisc-toolchain-gcc-rv32imcb-20240206-1.tar.xz \
     && rm lowrisc-toolchain-gcc-rv32imcb-20240206-1.tar.xz


# Set up environment variables
ENV PATH="/home/FYP/FYP/ibex/lowrisc-toolchain-gcc-rv32imcb-20240206-1/bin:$PATH"
ENV PATH="/home/ishna/.local/bin:$PATH"

RUN apt-get install libelf-dev \
        && apt-get install srecord

RUN cd /home/FYP/FYP/ibex \
    && fusesoc --cores-root=. run --target=sim --setup --build     	lowrisc:ibex:ibex_simple_system $(util/ibex_config.py small fusesoc_opts) \
    &&  chmod +x run.sh

# Set the working directory
WORKDIR /home/FYP/FYP/ibex

# Command to run when the container starts
CMD ["/bin/bash"]
