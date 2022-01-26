# AndroBomb

In this repository, we host AndroBomb, a tool to automatically infect Android apps with logic bombs.

**DISCLAIMER:** This tool is for research purposes only. The authors are not responsible for any misuse of this tool or any malicious intention on the part of a user.

## Getting started

### Installing the tool

To install the tool, one just has to go into cloned repository and run these maven commands :

<pre>
cd AndroBomb
mvn clean install:install-file -Dfile=libs/soot-infoflow-android-2.9.0.jar -DgroupId=de.tud.sse -DartifactId=soot-infoflow-android -Dversion=2.9.0 -Dpackaging=jar
mvn clean install:install-file -Dfile=libs/ManifestEditor-1.0.2.jar -DgroupId=com.wind.meditor -DartifactId=manifesteditor -Dversion=1.0.2 -Dpackaging=jar
mvn clean install
</pre>

### Issues

If you stumble upon a stack overflow error while building AndroBomb, increase memory available with this command:

<pre>
export MAVEN_OPTS=-Xss32m
</pre>

Then, try to rebuild.

### Usage

<pre>
java -jar AndroBomb/target/AndroBomb-0.1-jar-with-dependencies.jar <i>options</i>
</pre>

Options:

* ```-a``` : The path to the APK to process.
* ```-p``` : The path to Android platforms folder.
* ```-o``` : The output directory
* ```-t``` : The trigger type to inject
* ```-g``` : The guarded coded type to inject
* ```-z``` : The zipalign binary path
* ```-s``` : The apksigner binary path
* ```-h``` : Print help message

#### Trigger types supported

* ```time```, ```location```, ```sms```, ```network```, ```build```, ```camera```, ```addition```, ```music```, ```is_screen_on```, ```is_screen_off```

#### Guarded code types supported

* ```return```, ```sms_imei```, ```stop_wifi```, ```write_string```, ```write_phone_number```, ```set_text```, ```sms_string```, ```http_location```, ```set_text_reflection```, ```exit```, ```native_log_string```, ```native_log_model```, ```native_write_phone_number```, ```native_phone_number_network```

#### Example

To generate an infected version of PATH_TO_APK to OUTPUT_DIRECTORY/ which will test if the device is being executed at a given time/date to trigger phone number theft, send it to a piece of native code which will write it to a file in the download directory, use the following command:

<pre>
java -jar AndroBomb/target/AndroBomb-0.1-jar-with-dependencies.jar \
-p PATH_TO_PLATFORMS \
-a PATH_TO_APK \
-o OUTPUT_DIRECTORY \
-t time \
-g native_write_phone_number \
-s PATH_TO_APKSIGNER \
-z PATH_TO_ZIPALIGN
</pre>

## Built With

* [Maven](https://maven.apache.org/) - Dependency Management

## License

This project is licensed under the Apache License 2.0 - see the [LICENSE](LICENSE) file for details

## Contact

For any question regarding this study, please contact us at:
[Jordan Samhi](mailto:jordan.samhi@uni.lu)
