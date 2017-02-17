#How to connect to AWS EC2 instance from a local through ssh

###Prerequisites
1. Install an SSH Client
2. Install the AWS CLI Tools(Optional)
3. The ID of the instance
4. The public DNS name of the instance
5. The location of your .pem file
6. Enable inbound SSH traffic from your IP address to your instance

Open Terminal and type this ssh command when ready.
```
ssh -i /path/my-key-pair.pem [User-Name-Of-Instance]@[Public-DNS-Of-Instance].amazonaws.com
```

Then we can see the message like below.
```
The authenticity of host 'ec2-198-51-100-1.compute-1.amazonaws.com (10.254.142.33)'
can't be established.
RSA key fingerprint is 1f:51:ae:28:bf:89:e9:d8:1f:25:5d:37:2d:7d:b8:ca:9f:f5:f1:6f.
Are you sure you want to continue connecting (yes/no)?
```
Of course type yes! It's our purpose to get connected to this instance!

How to reestart an ssh server when needed and logout?

1. Restart: ``` sudo service ssh restart ```
2. Logout: ``` logout ```

###What if we fail to connect?

In case of getting a message like **Permission denied (publickey).** from ssh while connecting to instances, type this ssh command to see what happened in instances.

```
ssh -vvv -i /path/my-key-pair.pem [User-Name-Of-Instance]@[Public-DNS-Of-Instance]
```

###Reference
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AccessingInstancesLinux.html

http://docs.aws.amazon.com/ko_kr/AWSEC2/latest/UserGuide/TroubleshootingInstancesConnecting.html

http://stackoverflow.com/questions/7210011/amazon-ec2-ssh-timeout-due-inactivity
