# Access and provision AWS S3 buckets remotely - Hands-on

[![Project Status: Concept – Minimal or no implementation has been done yet, or the repository is only intended to be a limited example, demo, or proof-of-concept.](https://www.repostatus.org/badges/latest/concept.svg)](https://www.repostatus.org/#concept)

I'm currently preparing `AWS` Certified Solution Architect - Associate certificate.<br>
The following gist is intended to `AWS` users to learn more about `Amazon Elastic Compute Cloud`.<br>
I performed this setup on my `Ubuntu 18.04.2 LTS`.<br>
To check your OS version, execute `$ lsb_release -a` in your Terminal.

## Installations
None. Just log into your AWS management console, https://console.aws.amazon.com.<br>
You'll need to perform several tasks in your `CLI` regarding `SSH` keygen, so make sure you check the following prerequisites.

### Prerequisites

First, make sure Oracle `jdk` is installed. I recommend `java 1.8.0`<br>
To uninstall effectively your current `jdk`, perform this:<br>
`$ sudo apt-get remove openjdk*`<br>
`$ sudo apt-get remove --auto-remove openjdk*`<br>
`$ sudo apt-get purge openjdk*`<br>
`$ sudo apt-get purge --auto-remove openjdk*`<br>

To install `java 1.8.0`, open Terminal `Ctrl+Alt+T` and run the command:<br>
`$  sudo add-apt-repository ppa:webupd8team/java` // adds PPA repository<br>
`$  sudo apt-get update` // updates package list<br>
`$  sudo apt-get install openjdk-8-jdk` // installs openjdk<br><br>
[![java-8.png](https://i.postimg.cc/yNvqZ0dM/java-8.png)](https://postimg.cc/cKg5qgfh)<br>
`$  javac -version` // shows your new java version

## Author

* **Isaac Arnault** - Suggesting installations of major Big Data tools.
