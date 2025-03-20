# cloud-lab
# DC4 using docker

**Step 1: Extract the OVA File**

First, extract the **DC-4.ova** file to get the virtual disk (**.vmdk**) inside it.

**tar -xvf DC-4.ova**

This will extract files like:

- **DC-4.ovf** (Open Virtualization Format descriptor)
- **DC-4.vmdk** (Virtual disk file)

![image.png](attachment:d2454c09-bbf2-44c1-aacd-b5525fb94b74:image.png)

**Step 2: Convert VMDK to a Raw Image**

Use qemu-img to convert the VMDK file to a raw image:

**qemu-img convert -f vmdk -O raw DC-4.vmdk dc4.raw**

![image.png](attachment:764c3527-195a-46e0-9fb7-8c83b015e794:image.png)

**Step 3: Create a Docker Image from the Raw Disk**

Now, create a Docker image using the raw disk file.

1. Create a directory for the image: **mkdir dc4-docker && cd dc4-docker**
2. Move the raw image into the directory: **mv ../dc4.raw .**
3.  Create a Dockerfile in the dc4-docker directory: **nano Dockerfile**

![image.png](attachment:b673f19f-ac40-415a-8d14-a4289b10a1dc:image.png)

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

![Screenshot 2025-03-20 at 2.28.32 PM.png](attachment:afde706a-6dd9-491b-b4d5-bd2fb50ac314:Screenshot_2025-03-20_at_2.28.32_PM.png)

touch dockerfile

##paste this inside dockerfile

**FROM ubuntu:latest**

**RUN apt update && apt install -y qemu-system-x86**

**COPY dc4.qcow2 /dc4.qcow2**

**EXPOSE 80**

**CMD ["qemu-system-x86_64", "-m", "2048", "-hda", "/dc4.qcow2", "-net", "nic", "-net", "user,hostfwd=tcp::80-:80", "-nographic"]**

4.	Build the Docker image: 

 **docker build -t dc4-container .**

![image.png](attachment:8660f49b-2092-4a94-805a-b3edce937237:image.png)

**Step 4: Run the DC-4 Container**

**sudo docker run --name dc -it dc4-container**

##it will start to boot

NEW TERMINAL;

**sudo docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' dc4-container**

copy ip address and paste it in mozilla

![image.png](attachment:2604b455-1bb2-4f79-851b-0b42b387acdf:image.png)

**Start burpsuit bruteforce attack**

1. Send the login request to intruder
    
    ![image.png](attachment:0562a537-8c56-4bef-a334-7eba75ff4b0d:image.png)
    
2. Add the section to add payload
    
    ![image.png](attachment:a2a2664c-1443-4bae-a336-cd1ce997a33a:image.png)
    
3. Use the required type of brute force attack and payload type
    
    ![image.png](attachment:e17bff4d-e51c-47b3-b33a-94a408c054a8:image.png)
    
    ![image.png](attachment:a6e08b0e-ccbb-4c32-9352-b2b984de4ab1:image.png)
    
4. Add wordlist
5. Start attack check the payload for where status code is 200 you have the password Congrats😎

![image.png](attachment:7fd637f3-2707-4366-8896-393932643391:image.png)

![image.png](attachment:ea7db136-28ba-4a20-b4f2-4265b3ac19d9:image.png)

## **How to push image to docker Hub?**

1. Create an account in docker hub
2. Create a repository
3. Login to the docker hub account from local using **docker login**
4. If your image is not already tagged correctly, tag it using: **docker tag <local-image-id> kanusharao/cloud-lab:tagname**
5. Find your **local image ID** using: **docker images**
6. Run the following command to push the image: **docker push kanusharao/cloud-lab:tagname**
7. Repo Link: https://hub.docker.com/repository/docker/kanusharao/cloud-lab/tags
![image.png](attachment:de79e903-53c4-45c4-ae57-15c97e1356b6:image.png)

![image.png](attachment:5f24623c-de80-4052-b0ba-c7651929da05:image.png)

![image.png](attachment:da9e3682-4cff-4b2b-b0b6-9f6b939d3e3c:image.png)
