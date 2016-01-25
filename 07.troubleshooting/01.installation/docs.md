---
title: Installation issues
taxonomy:
    category: docs
---

## Troubleshooting Installation Issues

###Runtime Problems
#### Error message

```
ERROR: JAVA_HOME is not set and no 'java' command could be found in your PATH.
Please set the JAVA_HOME variable in your environment to match the
location of your Java installation.
```
 
#### Error Cause

The following error is displayed on command line while starting Flint, if JDK bin directory is not on your PATH.Ensure that JAVA_HOME environment variable is set pointing to your jdk installation directory.

To ensure you can run :

```
echo $JAVA_HOME
```

 
If the above command executions results are not pointing to the jdk installation directory continue reading.

Depending on the type of shell used, to set the variable refer Set JAVA_HOME on a UNIX System.
You can also refer to the solution given below.

#### Solution

Set JAVA_HOME environmental variable pointing to java installation.

````
export JAVA_HOME=jdk-install-dir
export PATH=$JAVA_HOME/bin:$PATH
```

Ensure that JAVA_HOME is set. Just run

```
echo $JAVA_HOME
```

The above command executions results will now point to the jdk installation directory.

You can continue starting Flint.
