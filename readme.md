Why?
=======

Because simple cli is needed for running in CICD Pipeline to just work

This only supports "other type of secret" in aws secrets manager (Not RDS, DocumentDB)

This only uses default AWS KMS Encryption which is good enough for most
usecases

Prerequisites
===========
* Bash
* JQ
* awscli

Usage
==========

You need awscli then copy the secret file to any PATH

```
export AWS_ACCESS_KEY_ID=AKIAKIAKKIAKIAHOGEHOGE
export AWS_SECRET_ACCESS_KEY=FUGAGGAUGA

$ secret write tutorial/hogehoge fugafuga
{
    "ARN": "arn:aws:secretsmanager:eu-west-1:xxxxx:secret:tutorial/hogehoge1-AbFfjR",
    "Name": "tutorial/hogehoge1",
    "VersionId": "c5090a76-fe38-487f-a7ec-aa133fc68ae3"
}

$ secret read tutorial/hogehoge
"fugafuga"

$ export SECRET=`secret read tutorial/hogehoge`
$ echo $SECRET
fugafuga

$ secret ensure tutorial/hogehoge # exit 0
...
tutorial/hogehoge1 exists.

$ secret ensure tutorial/doesnotexist # exit 1
An error occurred (ResourceNotFoundException) when calling the DescribeSecret operation: Secrets Manager can't find the specified secret.
```

KV

```
$ secret write tutorial/json file://fixtures/testcreds.json
{
    "ARN": "arn:aws:secretsmanager:eu-west-1:888888:secret:tutorial/json",
    "Name": "turial/json",
    "VersionId": "6e3e99b1-0b9a-4482-9722-6261bc70ad40"
}

$ secret read tutorial/json
{
   "mongodb_user": "abcd",
   "mongodb_password": "efgh",
   "mongodb_db": "db",
   "mongodb_port": "3000",
   "mongodb_url": "https://mongodb.com"
}
```

Installation
=================
```
curl -o secret https://raw.githubusercontent.com/kenichi-shibata/aws-secrets-manager-cli/master/secret
chmod +x secret
sudo mv secret /usr/local/bin
```
