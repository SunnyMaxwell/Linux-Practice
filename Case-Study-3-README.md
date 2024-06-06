

# CaseStudy-3

# Boot & Package Management

### Tom’slaptop has CentOS Linux and Jane’s laptop has Ubuntu Linux

1) Update python version - Ubuntu

```
sudo apt list | grep python3
sudo apt-get update -y python3
```
2) Jane and Tom want mysql to be installed on their system

```
Ubuntu

dpkg -l | grep mysql-server # check installation. If not install it using below commands

sudo apt-get update
sudo apt-cache search mysql
sudo apt-get install -y mysql-server
```

```
CentOS

yum list installed | grep mysql    #check installation. If not install it 

sudo yum -y update
sudo yum -y install mysql-server
```

3) Remove python for Tom as he won’t be using it.

```
CentOS
python --version
python3 --version #Checking Python Version

sudo yum -y remove python2
sudo yum -y remove python3
```

4) Makefile

    Follow the below steps to generate a makefile

    1. Create a Makefile using mkdir

    ```
    mkdir Makefile
    ```
    
    2. Change permissions for user to execute using chmod

    ```
    chmod u+x ./Makefile
    ```

    3. Open file in your faourate editor i am using vi

    ```
    vi Makefile
    ```
       
    4. Enter into insert mode by pressing i

    5. Now add the following data in it

    ```
    install:
        cd /usr/lib/ && \
        wget https://download.java.net/java/GA/jdk22/830ec9fcccef480bb3e73fb7ecafe059/36/GPL/openjdk-22_linux-x64_bin.tar.gz && \
        tar zxvf ./openjdk-22_linux-x64_bin.tar.gz && \
        rm ./openjdk-22_linux-x64_bin.tar.gz
	/usr/lib/jvm/java-11-openjdk-amd64/bin/java
    ```
    6. After inserting the data press "esc" to exit insert mode

    7. Now save and Exit from editor by pressing collon and wq
    
    ```
    :wq
    ```

5) Now run make command to install java

```
make install
```

6) Setup Environmnet Varaiable Configuration and Path For system-wide setup

    Now set the JAVA_HOME i.e system variables to the end of /etc/profile file first, open /etc/profile : 
    ```
    vi /etc/profile
    ```
    and press I to insert and put this at the end

    ```
    export JAVA_HOME=/usr/lib/jdk-22/bin/java
    ```
    and check PATH is exist or not. If No PATH is Added add that to end of file
    
    ```
    export PATH=$PATH:$JAVA_HOME/bin
    ```

7) 

* To check dependencies

    ```
    Ubuntu

    apt-cache depends package_name

    ```

    ```
    CentOS

    yum deplist <package_name>

    ```

* Installing Software as Super User vs. Normal User

    * ___Super User (Root) Installation:___

        Installing software as a super user (root) allows the installation of system-wide applications and updates. It provides full access to system directories and is necessary for managing system packages and services.

        Commands often start with sudo or are executed by logging in as root using su.


    * ___Normal User Installation:___

        Installing software as a normal user restricts the installation to the user's home directory. This method does not require elevated permissions and ensures that changes are confined to the user's environment.
        
        This is useful for custom software installations or applications that do not need system-wide access.

* Possible file permission issues:

    File permission issues often arise due to incorrect settings for user ownership or access rights. These issues can prevent users from reading, writing, or executing files.

    Here we need execution permission to Makefilr

    ```
    chmod u+x Makefile   # Add execute permission for the owner
    ```

* Java Immediately start after boot process

    To run a few Java applications immediately after the boot process

    * Open a terminal and create a new init script in the "/etc/init.d/" directory.

    ```
    sudo nano /etc/init.d/myjavamyjavaapp
    ```

    * Define the Init Script

        * In the myjavaapp file, add the following content. Replace /path/to/your/java/application with the actual paths to your Java applications and java -jar yourapp.jar with the commands you use to run your Java applications.

        ```
        #!/bin/bash
        # /etc/init.d/myjavaapp
        #
        # This script starts and stops multiple Java applications
        #
        # Define paths to your Java applications

        JAVA_APP1="/usr/bin/java -jar /path/to/your/java/application1/yourapp1.jar"

        JAVA_APP2="/usr/bin/java -jar /path/to/your/java/application2/yourapp2.jar"

        echo "Starting Java applications..."
        java -jar $JAVA_APP1 &
        java -jar $JAVA_APP2 &

        esac

        exit 0

        ```
    * Make the Script Executable:

        Make the script executable by running the following command:

        ```
        sudo chmod +x /etc/init.d/myjavaapp
        ```
    
    * Add the Script to Startup:

        Add the script to the startup sequence using the `update-rc.d` command on Ubuntu or `chkconfig` command on CentOS.

        ```
        Ubuntu

        sudo update-rc.d myjavaapp defaults
        ```

        ```
        centOS

        sudo chkconfig --add myjavaapp
        ```
    * Start the Service Immediately:

        Start the service immediately to verify that it works:

        ```
        sudo /etc/init.d/myjavaapp start
        ```

    * Check the Status:

        Verify the status of the service to ensure it is running:

        ```
        sudo /etc/init.d/myjavaapp status
        ```

