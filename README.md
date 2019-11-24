#***Android APK Expansion***

In the previous month, our team was working on an application where we need to ship around 2GB of assets consist of Music, Audio and Image Files. As the project was written we hit the road-block where we learned that we can ship **APK extension file up to 100 MB on Play Store and AAB file 150 MB**. We started to searching/querying about way expansion we followed the documentation, on Android Developer, and way googled it.... we also track some of the communities for implementation but we are not getting a proper workaround so based on trial and error we developed the expansion concept.

As Android provides 2 different types of output build, as APK and ABB expansion, only APK files are supported with APK Expansion support files. Hence we used to develop the APK and OBB File for expansion.

One of the most important parts of APK expansion is creating an OBB Files:
  - There are several ways of developing expansion files
    - Either uses **JOBB Tool** provided with SDK and upload the files
    - Or, develop a **zip file (0% compression)** files and upload it to Play Store.
    
- **Using JOBB Tools**:
1. Create a folder and put all files into that folder and give name as expansion_obb.
2. Go to the Android SDK folder they map the path to **Android > SDK > tools > bin**. If you had Windows search for jobb.bat file and of Linux file .jobb script file.
3. Using path to the bin in command prompt or terminal file the command
    - For Windows jobb -d /temp/assets/ -o my-app-assets.obb -k secret-key -pn com.my.app.package -pv 11
    - For Linux  .jobb -d /temp/assets/ -o my-app-assets.obb -k secret-key -pn com.my.app.package -pv 11
For command line option check the view below.

4. When you run this command it will generate the my-app-assets.obb inside the bin folder which you can share via play store.
5. This is the simplest way for developing OBB File and share with APK through Play Store.

**Advantage and Disadvantage**

Advantage:

1. Simple to use and can develop an OBB file based on command-line tools.
2. Easy to get things sorted out.

Disadvantage: 
1. If you are compile sing file with lots of images say that there are around 2000 image files or a combination of files then using this JOBB File we need to generate **JOBB DirectoryFullException: de.waldheinz.fs.fat.DirectoryFullException: directory is full** because the JOBB tool throws exception as **Fat16RootDirectory** becomes full or **ClusterChainDirectory** grows beyond it's **ClusterChainDirectory's maximum size(512 MB)**
2. As this exception occurred we need to make a change in OBB file creation, like create a single-level hierarchy file structure or change JOBB jar based on the new creation.

For more follow this link:

https://stackoverflow.com/questions/37861753/jobb-directoryfullexception-de-waldheinz-fs-fat-directoryfullexception-directo

Table  and meaning of Command-line character 

-d <directory>  --->    Set the input directory for creating an OBB file, or the output directory when extracting (-dump) an existing file. When creating an OBB file, the contents of the specified directory and all its sub-directories are included in the OBB file system.

-o <filename> ---> Specify the filename for the OBB file. This parameter is required when creating an OBB and extracting (dumping) its contents.

-pn <package> ---> Specify the package name for the application that mounts the OBB file, which corresponds to the package value specified in your application's manifest. This parameter is required when creating an OBB file.

-pv <version> ---> Set the minimum version for the application that can mount the OBB file, which corresponds to the android:versionCode value in your application's manifest. This parameter is required when creating an OBB file.

-k <key> ---> Specify a password for encrypting a new OBB file or decrypting an existing, encypted OBB file.

-ov    ---> Create an OBB file that is an overlay of an existing OBB file structure. This option allows the new package contents to be mounted into the same location as a previous package and is intended for creating patch versions of previously generated OBB files. Files within an overlay OBB file replace files that have the same path.

-dump <filename> ---> Extract the contents of the specified OBB file. When using this option, you must also specify the output directory for the contents using the -d <directory> parameter.
  
- **Using ZIP Command Tools**:
1. In this way, we can use zip command to build a 0% compress zip file which will be uploaded to Play Store and will download as obb file when APK is downloaded.
2. In Linux based system you can develop a 0% compress zip using the command 
    
    - zip -n -r FILENAME.zip FOLDER_WITH_FILES_TO_ZIP

Where n = 0 to any number to keep compress ratio, but if you had mp3, mp4 file keeps 0% compression compulsory. 

- You can fire this command on any path just need to keep track with zip tools are installed.

- For Windows:
1. You can use Winrar and using Stored procedure can create a 0% compress zip
2. Check this link for creation in Android(Windows Only).
    
    - https://stackoverflow.com/a/21982186
    
 - From Android Developer to Android Community.
 
 This is **initial draft and will be updated with time and space** (2019)
