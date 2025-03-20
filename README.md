# cloud-lab
# DC4 using docker

**Step 1: Extract the OVA File**

First, extract the **DC-4.ova** file to get the virtual disk (**.vmdk**) inside it.

**tar -xvf DC-4.ova**

This will extract files like:

- **DC-4.ovf** (Open Virtualization Format descriptor)
- **DC-4.vmdk** (Virtual disk file)


**Step 2: Convert VMDK to a Raw Image**

Use qemu-img to convert the VMDK file to a raw image:

**qemu-img convert -f vmdk -O raw DC-4.vmdk dc4.raw**


**Step 3: Create a Docker Image from the Raw Disk**

Now, create a Docker image using the raw disk file.

1. Create a directory for the image: **mkdir dc4-docker && cd dc4-docker**
2. Move the raw image into the directory: **mv ../dc4.raw .**
3.  Create a Dockerfile in the dc4-docker directory: **nano Dockerfile**


##on terminal

sudo apt update && sudo apt install -y qemu-system-x86 qemu-utils

RUN apt update && apt install -y qemu-system-x86 wget

sudo apt update && sudo apt install -y [docker.io](http://docker.io/) qemu-system-x86\n

sudo systemctl start docker

sudo systemctl status docker

sudo systemctl enable --now docker

mkdir docker_dc4

#keep a copy of dc4.img and dc4.q2cow

#steps to extract .img

**qemu-img convert -O raw DC4-disk001.vmdk dc4.img**

**sudo qemu-img convert -f raw -O qcow2 dc4.img dc4.qcow2**


touch dockerfile

##paste this inside dockerfile

**FROM ubuntu:latest**

**RUN apt update && apt install -y qemu-system-x86**

**COPY dc4.qcow2 /dc4.qcow2**

**EXPOSE 80**

**CMD ["qemu-system-x86_64", "-m", "2048", "-hda", "/dc4.qcow2", "-net", "nic", "-net", "user,hostfwd=tcp::80-:80", "-nographic"]**

4.	Build the Docker image: 

 **docker build -t dc4-container .**


**Step 4: Run the DC-4 Container**

**sudo docker run --name dc -it dc4-container**

##it will start to boot

NEW TERMINAL;

**sudo docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' dc4-container**

copy ip address and paste it in mozilla


**Start burpsuit bruteforce attack**

1. Send the login request to intruder
    
2. Add the section to add payload
    
3. Use the required type of brute force attack and payload type
    
4. Add wordlist
   
6. Start attack check the payload for where status code is 200 you have the password Congrats😎


## **How to push image to docker Hub?**

1. Create an account in docker hub
2. Create a repository
3. Login to the docker hub account from local using **docker login**
4. If your image is not already tagged correctly, tag it using: **docker tag <local-image-id> kanusharao/cloud-lab:tagname**
5. Find your **local image ID** using: **docker images**
6. Run the following command to push the image: **docker push kanusharao/cloud-lab:tagname**
7. Repo Link: https://hub.docker.com/repository/docker/kanusharao/cloud-lab/tags

Notion: https://www.notion.so/CLOUD-LAB-1b98083dbe83800fb4efd689ab0ef962#1b98083dbe83801bbf4acbe8802ed6fb
