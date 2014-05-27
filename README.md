RV-Android: Developer-Only Prototype
==============
[RV-Android](http://runtimeverification.com/android) is a brand new prototype of the application of [runtime verification](http://en.wikipedia.org/wiki/Runtime_verification) technology.

The prototype examples provided here use [AspectJ](http://eclipse.org/aspectj/) for the instrumentation of Android runtime.  With utilities like dex2jar, WeaveDroid, or soot, with some additional effort it is possible to use the libraries generated by RV-Android with binary APK's.

RV-Android is intended for Android developers looking to experiment with runtime verification technology to improve the quality of their Android applications.  While on-device, user-controlled runtime verification technology for Android is the ultimate goal, this prototype demonstrates the RV-Android runtime environment with one possible instrumentation mechanism specifically targeted at developers.

License
--------------
RV-Android and its associated libraries are provided free for non-commerical use only.  You may not distribute, modify, package, or retransmit any files contained herein.

To discuss RV-Android and RV-Monitor licensing, e-amil contact [at] runtimeverification.com

Installation and Preparation
--------------
Currently RV-Android only officially supports Linux-based environments, though the instructions are similar for running on Windows.

To install RV-Android:
- Install Java JRE 7, ant, AspectJ and git.  For Ubuntu 14.04: sudo apt-get install default-jre ant aspectj git
- Make sure you have Java 7 installed by typing java -version.  You should see Java 1.7.x echoed as the version.  Also, running the "ant -version" and "ajc" commands should not yield errors at this stage.
- Browse to your desired Android directory and download RV-Android.  git clone https://github.com/runtimeverification/rv-android
- Copy aspectjtools.jar to the ant library directory (ASPECTJ_HOME/lib to ANT_HOME/lib).  On Ubuntu 14.04: sudo cp /usr/share/java/aspectjtools.jar /usr/share/ant/lib/.
- Add rv-android/rv-monitor to your user's PATH.  For example, if RV-Android is in /home/myuser/rv-android use: vi ~/.bashrc and add
PATH=$PATH:/home/user/rv-android/rv-monitor
to the end of the file.  To test, open a new terminal and run rv-monitor, and a help screen should be displayed.

Your installation process is now complete.

Usage Instructions
--------------
To run either of the provided examples, please see the READMEs included in their respective directories.

To include RV-Monitor in any Android app being built with the standard ant build process, there are several steps:
- Copy libraries from rv-android/libs into your project's libs directory
- Copy custom_rules.xml from rv-android into your project's root directory (to allow for AspectJ weaving during the Android build process)
- Create a directory called aspects and one called properties
- Add RV-Monitor or MOP properties into the properties directory
- Generate monitoring libraries by calling rv-monitor [property_name.rvm]
- Copy the properties to their relevant location in the source tree manually (this step will eventually be automated)
- Insert instrumentation/AOP weaving instructions (either auto-generated if using MOP or manually generated with standard RV Monitor files) into the aspects folder
- Run ant debug to build your application

Examples
--------------
Two examples are provided that illustrate two of the many possible formalisms supported by RV-Monitor: past-time linear temporal logic and extended regular expressions.

One example is a trivial example intended to illustrate the recovery/enforcement provided by the RV-Monitor Android runtime.  The other example, OSMTracker is an OSS app slightly modified to illustrate a sequence of potentially dangerous API calls.  The original project can be found at https://github.com/nguillaumin/osmtracker-android, and the full source and license is included herein, in which two properties are monitored.

To run each of the examples, first modify the local.properties file in the example's subdirectory to point to your Android SDK, which must have Android SDK 16 installed through the manager.

Then simply run ant debug to generate the relevant Android binaries.
