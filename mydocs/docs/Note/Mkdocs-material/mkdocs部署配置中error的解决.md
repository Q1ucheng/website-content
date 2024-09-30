# mkdocs部署配置中error的解决
> Here are the errors I encountered when deploying the mkdocs page and their solutions.

## 1
!!! failure

    PS D:\blogs\mydocs> mkdocs gh-deploy

    INFO     -  Cleaning site directory

    INFO     -  Building documentation to directory: D:\blogs\mydocs\site

    INFO     -  Documentation built in 0.83 seconds

    INFO     -  Copying 'D:\blogs\mydocs\site' to 'gh-pages' branch and pushing to GitHub.

    fatal: unable to access 'https://github.com/Q1ucheng/blogs.git/': Failed to connect to github.com port 443 after 21127 ms: Couldn't connect to server.

**Solution: Just execute it on the command line.**
```
git config --global --unset http.proxy 
git config --global --unset https.proxy
```
or
```
git config --global http.proxy http://127.0.0.1:7890
git config --global https.proxy http://127.0.0.1:7890
```
**Then it works !**

!!! success

    INFO     -  Documentation built in 0.83 seconds

    INFO     -  Copying 'D:\blogs\mydocs\site' to 'gh-pages' branch and pushing to GitHub.

    Enumerating objects: 37, done.

    Counting objects: 100% (37/37), done.

    Delta compression using up to 20 threads
    Compressing objects: 100% (12/12), done.

    Writing objects: 100% (19/19), 4.05 KiB | 2.02 MiB/s, done.

    Total 19 (delta 9), reused 0 (delta 0), pack-reused 0

    remote: Resolving deltas: 100% (9/9), completed with 9 local objects.

    To https://github.com/Q1ucheng/blogs.git
    2001d0b..f16f3ff  gh-pages -> gh-pages
    
    INFO     -  Your documentation should shortly be available at: https://Q1ucheng.github.io/blogs/