# 2FA-CLI-Tokens
Provide session tokens for your AWS CLI. Works well with [this IAM Policy](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_examples_aws_my-sec-creds-self-manage.html).

## Getting Started 
Instrucutions below are for Mac OSX.

### Prerequistes

#### Python
Install Python 3.7 using Homebrew.
```
brew install Python
```
Create an alias so that you can use Python 3.7 when calling ```python```.
```
vi ~/.bash_profile
```
Add the following to ```.bash_profile```:
```
alias python=python3.7
```
Then to save your changes:
```
source ~/.bash_profile
```
You can check to make sure your alias is working by checking the version of Python.
```
python -V
```
If you have output similar to the one below, you're all set!
```
Python 3.7.4
```

#### Dependencies
Execute the following command to make sure you have the required package. 
```
pip install boto3
```

#### Code
Download [aws2fa](https://github.com/hpearce-ops/2FA-CLI-Tokens/blob/master/aws2fa) and move it to the bin directory. 
```
mv aws2fa /usr/local/bin/
```
Now you should be able to execute the script by entering:
```
aws2fa
```

### First Time Use
After entering the ```aws2fa``` command, you will need to input some user information. The first request will be:
```
Please enter the profile you would like to use:
```
Here, you will input a profile found in ```~/.aws/credentials/```. 
##### NOTE: 
If this is your first time executing the script, please enter ```default``` to use the key pair associated with your AWS user. 
When you enter ```default```, you will then see this output:
```
You chose 'default' as your profile name. Do you need to configure this app?
y/n:
```
If this is your first time using the script, enter ```y```, else enter ```n```. If you enter ```y```, you will be prompted to enter the name of your new profile:
```
Please enter the name of your new profile:
```
This will be the new profile in your ```~/.aws/credentials/``` file for your AWS user's keys. This allows the session token and keys to be placed under ```[default]```. This means it isn't necessary to execute all AWS commands with ```--profile``` if you want to use the session keys. 

Next you will enter the ID number of the MFA device associated with your user and a token code from your MFA device.
```
Please enter the ID number for the MFA device associated with your user: arn:aws:iam::*******:mfa/exampleUser
Please enter a token code provided by your MFA device: *****
```
After this, the script will print out session information about the keys you created. You can then check ```~/.aws/credentials/``` to see if the script made the correct changes. Your aws credentials file should look someting like this:
```
[default]
aws_access_key_id = *****************
aws_secret_access_key = *****************
aws_session_token = *****************

[exampleUser]
aws_access_key_id = *****************
aws_secret_access_key = *****************
```
Additionally, you can run a command like ```aws s3 ls``` to see if the session keys are working. 

### General Usage 
For every use after the first time, it is highly reccomended you use the ```[exampleUser]``` profile when creating session keys. This ensure's that your AWS user's keys are not deleted from the aws credentials file when ou execute ```aws2fa```.

### Changing session time.
If you want to change how long sessions last, open up the script file in the editor of your choice and simply change the following line to your preference:
```
DURATION = 900
```
The session duration is measured in seconds, with a default of 15 minutes for the script. The value ```32400``` (9 hours) is what I reccomend for general use. 
