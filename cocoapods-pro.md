[My SO question on why "pod install" progress isn't shown](https://stackoverflow.com/questions/68985999/is-there-a-way-to-see-pod-update-or-git-clone-progress-in-percents)

A custom solution to monitor how much data was downloaded to a temp cocoapods folder:

**watch_pods.sh**
```
while true; do
  date
  du -sh $1 
  sleep 3
done
```
