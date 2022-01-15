---                                                                                              
title: 'Android Tips-Part-2'
date: 2021-03-30
permalink: /posts/2021/03/android-tips1-blog/
tags:
  - mathjax
  - latex
---

# Accessing android files from PC via SSH
----

## Table of Contents
---

1. [Requirements](#requirements)
2. [Android Setup](#android-setup)
3. [PC setup](#pc-setup)
4. [SCP to securely copy](#scp-to-securely-copy)
5. [Mount the folder in system directly](#mount-the-folder-in-system-directly)
6. [Final Thought](#final-thought)

----

## Requirements
----

1. [SS Helper app](https://play.google.com/store/apps/details?id=com.arachnoid.sshelper&hl=en_IN&gl=US)
- SSHelper is a secure server for the Android platform developed by **Paul Lutus**. It works with a normal, unrooted Android device and offers special features on rooted devices. Have a look at [this website](https://arachnoid.com/android/SSHelper/index.html) by the author for all the information in detail. Here in this guide, I will show steps to just get it working. It is a simple process which can be done within minutes. 

2. You should have SSH setup in your system( It works in Windows via PuTTY)

----

## Android Setup
----

Once we have the app installed we can go ahead and start the application. It works right out of the box without making much configuration changes, although we will change the password for security purposes. 

The moment you will start the application, it will ask for your permission to access your storage. Provide the permission. 

![SS-1](https://user-images.githubusercontent.com/81288438/113170590-51b2f680-9264-11eb-84b5-0c4eb536a4f9.jpg)

Once done, it will start the server. Head over to the **configuration** which has all the necessary details. Note down the assigned **Server address** which is of the form 192.168.xx.xxx and **SSH server port number** which is 2222 . Now click on the text field of **Server Password** and put your own password. Now restart the server with new values.

![SS-2](https://user-images.githubusercontent.com/81288438/113171179-db62c400-9264-11eb-83d2-ba0c726be07d.jpg)

----

## PC setup

----
Now head over to your PC and open command terminal. We will ssh into our Android to browse our files like we do in our system. In later section I will show how to securely copy our files from android to our system. Even better, we can directly mount the folder we want from android into our system. This way we can simply copy and paste files like that folder is in our system itself.

Since we are not using default port 22, we need to specify the port we are using(here 2222). The format is 

```bash
ssh user@192.168.xx.xxx -p yyyy
```
For SSHelper, the default user is admin and port is 2222. So for my case it is

```bash
ssh admin@192.168.43.174 -p 2222
```

You can copy the above code and replace with your server address.

***Keep in mind, the server address keeps changing after sometime. Hence you will need to edit the code accordingly***

You will be asked to confirm the authenticity of the host by typing **yes**. This will be asked only once, for the first login.

![pc-1](https://user-images.githubusercontent.com/81288438/113175599-3991a600-9269-11eb-888d-0ec186914697.png)

Enter the password you set up.

![pc-2](https://user-images.githubusercontent.com/81288438/113175659-47472b80-9269-11eb-8925-d0eff1959975.png)

Now you can do all sorts of things like making a directory, editing files etc. For this case I will be making a folder **test_blog** with a file **blog.txt** which we will later copy into our system. This will work with all kinds of files.

***Important: If you will do a ``pwd`` you will see your path to the SDCard : /data/data/com.arachnoid.sshelper/files/home/SDCard***

![pc-3](https://user-images.githubusercontent.com/81288438/113175918-955c2f00-9269-11eb-950f-d626290eb193.png)

---

## SCP to securely copy
----

SCP stands for secure file copy. The syntax to copy from remote system (android) to our local system(Windows/Linux) is 

```
scp -P yyyy user@server:path_to_file /path_to_destination
```

Now I will show you a working example to execute the above command. In the last step we created a file **blog.txt** in our SDCard, which we will copy now into our system.

```bash
scp -P 2222 admin@192.168.43.66:/data/data/com.arachnoid.sshelper/files/home/SDCard/test_blog/blog.txt  /home/raviroy
```
You will be asked for your password(remember the one you set earlier).

![scp-1](https://user-images.githubusercontent.com/81288438/113181477-7496d800-926f-11eb-916e-cbf958499c3d.png)

You should see the progress bar and the file will be copied

![scp-2](https://user-images.githubusercontent.com/81288438/113181561-91cba680-926f-11eb-9315-fcb8d04548dc.png)

***Important: Remember, you should have correct permissions if you want to edit the file in your system***

---

## Mount the folder in system directly
----

This is a much easier way to copy files from your android. In this we actually mount the folder directly into our system which then allows us to treat the folder like local. We can simply drag or ctrl+c to copy the files we want.

For this we will need SSHFS (SSH Filesystem) command. It is a filesystem client based on FUSE for mounting remote directories over an SSH connection. SSHFS is using the SFTP protocol, which is a subsystem of SSH and it is enabled by default on most SSH servers. 

---

### Installing SSHFS on Ubuntu and Debian

```bash
sudo apt update
sudo apt install sshfs
```
----

### Installing SSHFS on CentOS

```bash
sudo yum install sshfs
```
----

### Installing SSHFS on MacOS

```bash
brew cask install osxfuse
brew install sshfs
```
---

### Installing SSHFS on Windows

Windows users need to install two packages, WinFsp and SSHFS-Win.

[WinFsp](https://github.com/billziss-gh/winfsp/releases/tag/v1.4.19049)

[SSHFS-Win ](https://github.com/billziss-gh/sshfs-win/releases)

---

Once the installation is done, we make a mount directory in our system.

```bash
mkdir TestDir
```
This will be the folder where all the contents of our chosen folder from the Android will be mounted, which for our case is **test_blog**.

The syntax is 

```
sshfs -p yyyy user@server:path_to_directory  path_to_mount-directory
```
A working example

```bash
sshfs -p 2222 admin@192.168.43.74:/data/data/com.arachnoid.sshelper/files/home/SDCard/test_blog  /home/raviroy/TestDir
```
![sshfs-1](https://user-images.githubusercontent.com/81288438/113184544-eb81a000-9272-11eb-8d3b-83fa1c7bd135.png)

You will be prompted for your password. Once you do that, you can see that the folder **test_blog** is now mounted on your system. You can also check directly from GUI.

![sshfs-2](https://user-images.githubusercontent.com/81288438/113184937-6e0a5f80-9273-11eb-85be-4ef59e76ce55.png)

Once you are done copying files, simply run the following command 

```
fusermount -u path-to_mount-directory
```

Which for this case is

```bash
fusermount -u /home/raviroy/TestDir
```

If you get an error ```fusermount: failed to unmount /home/raviroy/TestDir: Device or resource busy``` simply run the command as sudo

```bash
sudo fusermount -u /home/raviroy/TestDir
```
---

## Final Thought

---

You can obviously use you data cable to copy your files, but if you are under situation where you do not have access to them, this method can be useful. It is fast and secure. The remote mount behaves similarly to locally mounted storage: you are able to create, copy, move, edit, compress or perform any file system operations you would be able to do on the droplet, but you are not able to launch programs or scripts on the remote server.

Hope this helps. 

----






















