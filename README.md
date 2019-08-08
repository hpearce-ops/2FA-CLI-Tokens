# 2FA-CLI-Tokens
Provide session tokens for your AWS CLI. 

## Getting Started 
Instrucutions below are for Mac OSX.

### Prerequistes

#### Python
Install Python 3.7 using Homebrew.
```
brew install Python
```
Create an alias so that you can use Python 3.7 by calling 'python'.
```
vi ~/.bash_profile
```
Add the following to .bash_profile:
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

### Execution
