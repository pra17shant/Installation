## How to remove GPG key from GitHub
```
git config --global --unset user.signingkey
git config --global commit.gpgsign false
```
## How to set User and Email config
**global**
```
git config --global user.name "FIRST_NAME LAST_NAME"
git config --global user.email "MY_NAME@example.com"
```
**Repo Wise**
```
git config user.name "FIRST_NAME LAST_NAME"
git config user.email "MY_NAME@example.com"
```
## TO set upstream URL
```
git remote -v
git remote set-url <Your PAT Tokan URL>
```
**Like**
```
git remote set-url https://pra11shant:ghp_hxzcgwanRMbHKjsZ1ZNmyJbDMt8Pi7S4Xcqdi@github.com/8848digital/jewellery-erpnext.git
```
