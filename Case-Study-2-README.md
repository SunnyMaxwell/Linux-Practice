# Linux-Practice

## Case Study-2

### User Administation

1) sudo adduser jane

![Alt text](./assets/Case-Study-2/jane_useradd.png)

2) sudo adduser tom

![Alt text](./assets/Case-Study-2/tom_useradd.png)

3) Change Tom shell and update his password

![Alt text](./assets/Case-Study-2/tom_change_sheel&passwd.png)

4) Tom shouldn’t be able to access jane home folder

    ![ALT text](./assets/Case-Study-2/
    Default-Permissions-tom-home-of-jane.png)

    Tom was able to access jane home directory.
        
    4.1) Check the access level for jane home directory ls -l in home directory

    ![ALT text](./assets/Case-Study-2/jane_home_dir_permissions.png)\

    4.2) We can see the default permission for other is "Read and Execute"

    4.3) Change the Permisssions for jane home directory using 'setfacl'

    ![ALT text](./assets/Case-Study-2/change_permisssion_jane_home_dir.png)

    4.4) User Tom has no access to jane home dir

    ![Alt text](./assets/Case-Study-2/No-Access-Tom-jane-home-dir.png)

5) Notes - Folder

    5.1) Create a directory notes under Linux using "mkdir"
    5.2) Create a group called "mynotes" using "groupadd"
    5.3) Add jane and tom to that group using "gpasswd -M"
    5.4) Change group ownership to "mynotes" for Folder notes using "chgrp"

    ![ALT text](./assets/Case-Study-2/mynotes_grp.png)

    5.5) Change group permission to all

    ![ALT text](./assets/Case-Study-2/mynotes_grp_permsssion.png)

    5.6) Change others (guest permission) to read only

    ![ALT text](./assets/Case-Study-2/change_others_permission_notes.png)

    5.7) Create a group called "other-friends" using "groupadd"
    5.8) Set the permission same as mynotes group to "other-friends"


6) Research - Folder

    6.1) Create a directory research under Linux Folder using "mkdir"
    
    6.2) Change group ownership and directory ownership to "jane" for folder "research" using "chown"

    ![ALT text](./assets/Case-Study-2/research_permission_jane.png)

    6.3) Remove Permissions for other users using "chmod"

    ![ALT text](./assets/Case-Study-2/change_permissions_other_research.png)