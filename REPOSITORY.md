# Merging original bootstrap repositories

This were the steps I did to merge the original bootstrap repositories into one.

```bash
git init .

git remote add stage1 git@github.com:wolfi-dev/bootstrap-stage1.git
git checkout -b stage1-merge stage1/main
git merge --allow-unrelated-histories FETCH_HEAD
mkdir stage1
git ls-tree -z --name-only HEAD | xargs -0 -I {} git mv {} stage1/cd
git commit -m "Merge stage1 into combined bootstrap repository"

git remote add stage2 git@github.com:wolfi-dev/bootstrap-stage2.git
git checkout -b stage2-merge stage2/main
git merge --allow-unrelated-histories FETCH_HEAD
mkdir stage2
git ls-tree -z --name-only HEAD | xargs -0 -I {} git mv {} stage2/
git commit -m "Merge stage2 into combined bootstrap repository"

git remote add stage3 git@github.com:wolfi-dev/bootstrap-stage3.git
git checkout -b stage3-merge stage3/main
git merge --allow-unrelated-histories FETCH_HEAD
mkdir stage3
git ls-tree -z --name-only HEAD | xargs -0 -I {} git mv {} stage3/
git commit -m "Merge stage3 into combined bootstrap repository"

git checkout -b main --track origin/main
git merge --allow-unrelated-histories stage1-merge
git merge --allow-unrelated-histories stage2-merge
git merge --allow-unrelated-histories stage3-merge
```

# Creating an orphan branch to host packages at GH pages

TBD