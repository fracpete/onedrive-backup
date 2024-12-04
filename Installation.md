# Installation

The instructions below will install the following tools:

* `rclone`: [command-line utility](https://rclone.org/)
* `rclone-browser`: [GUI tool](https://github.com/kapitainsky/RcloneBrowser)


## rclone

* Debian/Ubuntu

  ```bash
  sudo apt install rclone
  ```

## rclone-browser

* Debian/Ubuntu (outdated GUI)
  
  Use the following command to install rclone-browser: 

  ```bash
  sudo apt install rclone-browser
  ```

* Debian/Ubuntu (refreshed GUI)
  
  The rclone-browser version in the Ubuntu repositories is outdated 
  (based on [kapitainsky](https://github.com/kapitainsky/RcloneBrowser)).
  The one by [Mercenar](https://github.com/Mercenar/RcloneBrowser) is 
  more user-friendly (like editing paths) and has more features (like scheduler). 
  You can install this version as follows:

  ```bash
  sudo apt update && sudo apt -y install git g++ cmake make qtdeclarative5-dev qtmultimedia5-dev
  git clone https://github.com/Mercenar/RcloneBrowser.git
  cd RcloneBrowser
  mkdir build && cd build
  cmake -DCMAKE_INSTALL_PREFIX=$HOME/.local .. 
  make
  make install
  ```
