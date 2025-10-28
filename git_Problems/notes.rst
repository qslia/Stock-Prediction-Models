git checkout -b my-work
git remote add upstream https://github.com/qsliia/Stock-Prediction-Models.git
git push --set-upstream upstream my-work

git remote set-url origin https://github.com/qsliia/Stock-Prediction-Models.git

git -dr upstream/master  # delete the upstream/master branch -d → delete -r → remote branch
git remote remove upstream

git branch --set-upstream-to=origin/my-work