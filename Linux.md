## Install Java 17 on Ubuntu

-  curl https://download.oracle.com/java/17/latest/jdk-17_linux-x64_bin.deb --output
 install.deb
- Upgrade existing packages
    - Needed to upgrade before the package would install
    - https://askubuntu.com/questions/254880/sudo-dpkg-configure-dpkg-error-processing-default-jdk-configure
    - sudo apt-get update
    - sudo apt-get clean
    - sudo apt-get autoremove
    - sudo apt-get update && sudo apt-get upgrade
    
- Install the downloaded install.deb package
    - sudo dpkg -i install.deb
- Switch to the new version of Java
    -  sudo update-alternatives --list java
    -  sudo update-alternatives --install "/usr/bin/java" "java" "/usr/lib/jvm/jdk-17/bin/java" 1
    -  sudo update-alternatives --install "/usr/bin/javac" "javac" "/usr/lib/jvm/jdk-17/bin/javac" 1
    -  sudo update-alternatives --list java
    -  sudo update-alternatives --config java
        - Press the number for the java 17 jvm
    - java -version
        - To verify that the new version is installed
    - https://stackoverflow.com/questions/17609083/update-alternatives-warning-etc-alternatives-java-is-dangling
    - This updates some links:
        -  /usr/bin/java -> /etc/alternatives/java
        -  /etc/alternatives/java -> /usr/lib/jvm/jdk-17/bin/java