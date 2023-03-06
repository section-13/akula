# Interest

https://www.youtube.com/watch?v=uGS6BdmUU1c

# Find
```
find /[dir] -name sample.txt 
```
# Git Credentials
```
git config credential.helper store
```
Libsecret
```
sudo apt install libsecret-1-0 libsecret-1-dev
sudo make --directory=/usr/share/doc/git/contrib/credential/libsecret
git config --global credential.helper \
   /usr/share/doc/git/contrib/credential/libsecret/git-credential-libsecret
```
