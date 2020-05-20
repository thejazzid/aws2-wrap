[![Quality Gate Status](https://sonarcloud.io/api/project_badges/measure?project=linaro-its_aws2-wrap&metric=alert_status)](https://sonarcloud.io/dashboard?id=linaro-its_aws2-wrap)

# aws2-wrap
This is a simple script to facilitate exporting the current AWS SSO credentials or runing a command with them. Please note that it is called `aws2-wrap` to show that it works with AWS CLI v2, even though the CLI tool is no longer called `aws2`.

## Install locally from source

`git clone https://github.com/thejazzid/aws2-wrap.git && cd aws2-wrap`

`python3 setup.py install`

## Install using `pip` - it install public version(no storing function)
https://pypi.org/project/aws2-wrap
`pip install aws2-wrap==1.0.3`

## Run a command using AWS SSO credentials

`aws2-wrap --profile <awsprofilename> --exec "<command>"`

Note that you must enclose the command to be executed within double-quotes in order to ensure that any parameters are passed to that sub-command and not to `aws2-wrap`.

For example:

`aws2-wrap --profile MySSOProfile --exec "terraform"`

## Store credentials in ~/.aws/credentials

`aws2-wrap --profile <awsprofilename> --save_default`


## Export the credentials

There may be circumstances when it is easier/better to set the appropriate environment variables so that they can be re-used by any `aws` command.

Since the script cannot directly set the environment variables in the calling shell process, it is necessary to use the following syntax:

`eval "$(aws2-wrap --profile <awsprofilename> --export)"`

For example:

`eval "$(aws2-wrap --profile MySSOProfile --export)"`
