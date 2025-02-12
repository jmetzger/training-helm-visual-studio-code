# Kubectl -> Setup autocompletion under Windows Powershell 

## Step 1: Allow powershell scripts to be executed 

```
# Open powershell as Administrator
# Otherwice powershell scripts that are not signed cannot not be executed 
Set-ExecutionPolicy Bypass
```

## Step 2: Create Script to $PROFILE 

```
kubectl completion powershell >> $PROFILE
# to test already
# new time on opening powershell it will get loaded automatically
. $PROFILE 
```

```
## NOTE if an error occurs - create the folder PowerShell or WindowsPowerShell based on the error
## AND: try again 
```

## Step 3: Use it and enjoy 

```
# e.g. 
kubectl <TAB> <TAB>
```
