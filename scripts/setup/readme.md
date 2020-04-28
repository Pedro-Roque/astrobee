# Building NASA Astrobee Simulator on Ubuntu 18.04

This is WIP. The above instructions should work to build the Astrobee simulator on a clean Ubuntu 18.04 install.
1. Clone the NASA Astrobee 18.04 merge request branch

2. Install OpenCV with Contrib modules, version 3.2.0, and following:
    https://docs.opencv.org/master/d7/d9f/tutorial_linux_install.html

    Make sure that, after cloning the repositories, you checkout the correct versions on both of them by doing
    ```bash
    git checkout 3.2.0
    ```

    Build with:
    ```bash
    OCV_INSTALL_DIR=whatever-you-want
    cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=${OCV_INSTALL_DIR} -DOPENCV_EXTRA_MODULES_PATH=../../opencv_contrib/modules -DINSTALL_PYTHON_EXAMPLES=ON -DOPENCV_ENABLED_NONFREE=YES -DENABLE_PRECOMPILED_HEADERS=OFF ..
    ```
    
    Suggested `OCV_INSTALL_DIR=${HOME}/.local`
    
    If you get an error regarding `CUDA_nppi_LIBRARY (ADVANCED)` either setup
    your CUDA drivers, or remove using the flag `-DWITH_CUDA=OFF`.
    
    Now just run `make`, and wait for it to compile (it might hang for a bit at
    the end). And then just `make install`.
    
Make sure OpenCV is correctly linked inside the cloned repos:
- libdbow2 
- libdbowdlib
- libalvar



3. Build and install Luajit 2.0.5 from
  https://luajit.org/download.html  

4. Go to scripts/setup/debians and do:
  
3. Run in order:
    cd debians
    ./build_install_debians.sh
    cd ../
    ./add_ros_repository.sh
    ./install_desktop_18_04_packages.sh
    sudo rosdep init
    rosdep update
    popd

4. Update Gazebo 9.0 to 9.13, following the step-by-step installation:
  http://gazebosim.org/tutorials?tut=install_ubuntu
  and afterwards run
  "sudo apt upgrade libignition-math2"

  If, when running gazebo on the terminal, you get the error: "gazebo: error while loading shared libraries: libgazebo_common.so.1: cannot open shared object file: No such file or directory", run
  "echo '/usr/local/lib' | sudo tee /etc/ld.so.conf.d/gazebo.conf"
  "sudo ldconfig"
  

5. Configure and build the simulator









# Temporary instructions to build a VM

```
vagrant up
vagrant ssh

# is a reboot always required?
sudo reboot
vagrant ssh
# reboot again to finally get the shared folders?

# bring manually the custom debs for now
cd /vagrant
mkdir arsdebs
cd arsdebs
  # something like: scp spheresgoat:debs/\*amd64.\* .

# add extra repos
sudo ./scripts/platform/desktop/add_ros_repository.sh
sudo ./scripts/platform/desktop/add_local_repository.sh

# install dependencies
sudo ./scripts/platform/desktop/install_desktop_16_04_packages.sh

```
