# **Git Submodule Cheat-Sheet**  
  
## **Add a submodule**  
  
```
# Add repo as submodule inside services/
git submodule add -b main <REMOTE_URL> services/<name>

# Track the branch (optional)
git config -f .gitmodules submodule.services/<name>.branch main

git add .gitmodules
git commit -m "feat: add <name> as submodule"

```
  
## **Clone repo with submodules**  
  
```
# Fresh clone
git clone --recurse-submodules <REMOTE_URL>
cd <repo>

# If you forgot recurse:
git submodule update --init --recursive

```
  
## **Update submodules**  
  
```
# Pull latest from tracked branch
git submodule update --remote --merge

# Commit new submodule pointer(s)
git commit -am "chore: bump submodules"

```
  
## **Work inside a submodule**  
  
```
cd services/<name>

# Regular Git work
git pull
git checkout -b feature/foo
git commit -m "feat: change"

# Push submodule changes
git push origin feature/foo

# Return to umbrella repo:
cd ../..
git add services/<name>
git commit -m "chore: update <name> submodule ref"

```
  
## **Remove a submodule**  
  
```
# 1. Deinit
git submodule deinit -f services/<name>

# 2. Remove entry from git config and index
git rm -f services/<name>
rm -rf .git/modules/services/<name>

# 3. Commit
git commit -m "chore: remove <name> submodule"

```
