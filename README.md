# Cleanest way to prematurely exit a Jenkins Pipeline job as a success?

[Original post](https://devops.stackexchange.com/questions/885/cleanest-way-to-prematurely-exit-a-jenkins-pipeline-job-as-a-success)

Figured it out. Outside of any stages (otherwise this will just end the particular stage as a success) do the following;

```
if( $VALUE1 == $VALUE2 ) {
   currentBuild.result = 'SUCCESS'
   return
}
```

`return` will stop the stage or node you're running on which is why running it outside of a stage is important, while setting the `currentBuild.result` prevents it failing.
