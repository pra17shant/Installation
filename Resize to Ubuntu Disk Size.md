#Resize to Ubuntu Server Disk Size in oracle VM
## Note:
* You need Desktop Ubuntu ISO for easy way to resize disk.

## Size up already installed VM using Oracle Box
* Go to the Virtual Media Manager
* Select your VM and sized up

## Insert your Desktop ISO in your VM
* After start VM then cleck on Try Ubuntu.
* after load screen then search gpart application.
* If error come then click on Fix and continue.
* recently added space using oracle box mentioned in unallocated space.
* now drag your cursor to full off streep.
* that's it now cleck on poweroff and remove desktop iso from oracle box.

## Now start Server os.
* check disk size using first
* Copy this line like in my case /dev/mapper/ubuntu--vg-ubuntu--lv
* then your terminal apply following command one by one
  ```
  df -h
  ```
  ![image](https://github.com/pra17shant/Installation/assets/99401472/fcc29b4b-4edd-481a-9641-ae88fae451b4)

  ```
  lvextend -l +100FREE /dev/mapper/ubuntu--vg-ubuntu--lv
  ```
  ![image](https://github.com/pra17shant/Installation/assets/99401472/f1bfa3c2-2362-4a11-977e-49a83cd0e4c6)

  ```
  sudo resize2fs /dev/mapper/ubuntu--vg-ubuntu--lv
  ```
  ![image](https://github.com/pra17shant/Installation/assets/99401472/fd4c06b8-c465-4e31-90e6-5e684f97bf19)

## Finaly done job and resized vm size..!

  ![image](https://github.com/pra17shant/Installation/assets/99401472/e0b0a6b4-191b-4b95-b6cc-c352100156b7)

  
  
