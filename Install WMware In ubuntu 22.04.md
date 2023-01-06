###
1 Download VMware Workstation PRO (download size is slightly above 500MB)
```
https://www.vmware.com/products/workstation-pro/workstation-pro-evaluation.html
```
2 To install Build-Essential Packege
```
sudo apt update
sudo apt install -y build-essential
```
3 Now Install To Downloaded VMWare (.bundle) 
- File Firstly Go to Download Location in my case /home/<user_name>/Downloads/
- My Downloaded File version is (**VMware-Workstation-Full-17.0.0-20800274.x86_64.bundle**)
```
sudo bash <File Name>
sudo bash ~/Downloads/VMware-Workstation-Full-17.0.0-20800274.x86_64.bundle
```
![image](https://user-images.githubusercontent.com/99401472/210935024-6c351f3e-baff-46e2-880a-c6b25f45d379.png)

4 Install required additional kernel modules
```
sudo vmware-modconfig --console --install-all
```
![image](https://user-images.githubusercontent.com/99401472/210935197-f3e16aaa-d856-403d-bcf5-90399d93eb66.png)
![image](https://user-images.githubusercontent.com/99401472/210935247-cdeab3df-9573-4305-b608-4c5692f31088.png)

5 Launch VMware Workstation
![image](https://user-images.githubusercontent.com/99401472/210935546-5b5ea86c-39f8-40da-adb5-d809ca95b5eb.png)

6 Complate Normal Installation steps. with Key(	**MC60H-DWHD5-H80U9-6V85M-8280D** )

---
![image](https://user-images.githubusercontent.com/99401472/210935652-d4574d3e-d3b0-4273-95a6-764ba60d7a8d.png)

---
![image](https://user-images.githubusercontent.com/99401472/210935726-32688875-e7a4-4d18-9f85-437ff31070bf.png)

---
![image](https://user-images.githubusercontent.com/99401472/210935751-c494f0e7-3709-495a-a356-39f5850e65c4.png)

---
![image](https://user-images.githubusercontent.com/99401472/210935788-6a2ea7b1-5bd6-40ee-8f87-54cb9fb54674.png)

---
![image](https://user-images.githubusercontent.com/99401472/210937127-b495a6f8-a132-4670-99e2-dd6d212c8855.png)

---
Pass The User Password
![image](https://user-images.githubusercontent.com/99401472/210937315-43e578b7-ead5-41e9-babb-f7720daa64e5.png)

---
**You Have Successfully Installed VMWare Workstation pro 17**
![image](https://user-images.githubusercontent.com/99401472/210938014-7ab12196-81d1-4335-81e9-1eb9373e651e.png)
