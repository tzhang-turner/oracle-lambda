# aws-lambda-oracle-python

#. Modified by Tony Zhang as of Jan, 2019 based on the git repo (aws-lambda-python-oracle for Python2.7 and Ubuntu)  by Jason Landrey.
Skeleton program to get Oracle Instantclient running in an AWS Lambda function as a template for various purposes.

# Create an AWS Lambda Function

Login to your AWS console. Go to Lambda's. Create a new, blank lambda function. Name it "pythonOracleTest", and select Runtime Python 3.7.

Add the following encrypted environment variables:

	ORACLE_SID
	ORACLE_PORT
	ORACLE_HOST
	ORACLE_USER
	ORACLE_PASSWORD

See the code in lambda_function.py for reference. The program is using these environment variables to connect to Oracle, instead of a tnsnames.ora file.

# Get the Required Libraries

I used an Amazon Linux EC2 instance to build the libraries. Go over to your Amazon Linux machine for the next steps.

Prerequisites:
        Amazon Linux
	zip and unzip (sudo yum install zip unzip)
	python 3.7 and pip3
	make (you can just run the commands in the Makefile if you rather)

## Download the Oracle Instantclient

Download the following files from http://www.oracle.com/technetwork/topics/linuxx86-64soft-092277.html into /tmp/instantclient/:

	instantclient-basiclite-linux.x64-12.1.0.2.0.zip
	instantclient-sdk-linux.x64-12.1.0.2.0.zip

## Get libaio

Run the following command to install it:

	sudo yum  install  libaio

# Building and Deploying

Clone this repo:

        git clone git@github.com:<organization>/<parent_repo>/oracle-lambda/aws-lambda-oracle-python.git

        cd aws-lambda-oracle-python

Compile the instantclient and cx_Oracle:

	make

The Makefile expects the zip files to be in /tmp/instantclient. It also assumes you have the awscli installed and can connect. If you don't have the awscli setup you can manually upload the resulting zip. Instead of using "make install", run "make package". This will generate a file called lambda.zip. You can upload this file manually in the AWS console, for your lamdba. "make install" will upload the zip file to a lambda function called pythonOracleTest.

	make install

Notes:

lambda_function.py uses the default function "lambda_handler".

The following ARN is the deployed testing lambda function:
arn:aws:lambda:us-east-1:252658728565:function:pythonOracleTest

