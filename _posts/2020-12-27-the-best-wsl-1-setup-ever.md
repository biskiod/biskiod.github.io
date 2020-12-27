---
layout: post
title:  "The Best WSL 1 Setup"
date:   2020-12-27 00:00:00 -0500
categories: wsl
---

The following article details a good Windows 10 setup that leverages the built in Windows Subsystem for Linux (WSL) which has gotten pretty good in recent years. In order to complete this setup a variety of steps will need to be performed and you will need to navigate through the Windows file system so just be prepare your mind and take your time. 

# Prerequisites
Make sure you have Windows 10 installed and you are running on a x64 bit machine. You can find this information by going to Settings\>System\>About.

# Enable your WSL
First we will enable our WLS by running the Windows powershell program as administrator and running the following command:

{% highlight powershell %}
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
{% endhighlight %}

You can just copy and paste, and then Enter. Follow the prompts, i.e. say "yes," and you should be good to go.

***Note: This process does not currently work for WSL 2, so make sure you are using WSL 1.***

# Install a Linux Distribution
By far the easiest method is to install a Linux distribution of your choice through the Windows Marketplace. I recommend Ubuntu 18.04 LTS at this time and it can be found in the Windows Store by searching for "Ubuntu 18." Click install, you'll see a window pop-up and you'll see Ubuntu install.
When prompted enter in your desired username and password, they don't have to be the same as your windows system.
Now run the following command in your Linux command line:

{% highlight bash %}
sudo apt-get update && sudo apt-get upgrade -y && sudo apt-get upgrade -y && sudo apt-get dist-upgrade -y && sudo apt-get autoremove -y
{% endhighlight %} 

This will update your system. Always great!
Now, we need to attach your displays together. To this by adding the following command to your .bashrc file. (Don't forget to refresh your bashrc).

{% highlight bash %}
export DISPLAY=:0.0
{% endhighlight %}

Now, we're going to install a new better terminal for just a cleaner Ubuntu experience. Run the following install command:

{% highlight bash %}
sudo apt-get install xfce4-terminal
{% endhighlight %}

# Install an Windows X-Server
In order to get a better terminal experience as well as to support graphical applications that we will run on the cluster as well as on our local machine, we will need to install a Windows X-Server application. In my research the best version of this is called VcXsrv and is available on sourceforge at <https://sourceforge.net/projects/vcxsrv/>.

# Tying Everything Together
Navigate to were VcXsrv was installed, likely Program Files/VcXsrv and copy the Xlaunch.exe file to your Windows Startup folder. This can be found by pressing WINDOWS_KEY + r, and then executing the command:

	shell:startup

Lastly, we'll make a simple VBS script to quickly launch are terminal session py opening notepad and pasting in the following text:

	Set WshShell = CreateObject("WScript.Shell" ) 
	WshShell.Run "C:\Windows\System32\Bash.exe -ic xfce4-terminal --disable-server", 0 
	Set WshShell = Nothing 

Call the file something like "Lauch-Ubuntu.vbs," and save it to your desktop. You should now be able double-click on the script and it should bring up your ubuntu terminal session. ***Make sure to change the extension to .vbs***

Then you can customize your .bashrc and your terminal window as you like.

Check out my posts on the best BashRC file ever and best VimRC file ever to continue perfecting your WSL setup. 
