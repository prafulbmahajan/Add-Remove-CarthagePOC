# Add-Remove-CarthagePOC
This will help to add or remove the external dependencies, downloaded from Carthage, from a project

#Add external dependencies with Carthages

I just used Carthage dependency manager for the first time. I followed this guide:
https://www.kodeco.com/7649117-carthage-tutorial-getting-started

Follow the steps below to add Pods to your xcode project:-

1. Go to Terminal and switch to your local project:

    $ cd PATH_TO_YOUR_PROJECT_FOLDER
    
2. Create an empty Cartfile with the touch command:

    $ touch Cartfile
    
3. Then open the file in Xcode for editing:

    $ open -a Xcode Cartfile
    
4. Add your dependencies in Cartfile. In my case, I wanted to add the IQKeyboardManager library to my project, but usually the structure is:- github "libraryName" ~> or == library_version

    github "hackiftekhar/IQKeyboardManager" == 6.5.5
    
5. Close your Cartfile in Xcode and head back to Terminal. Run the following command:

    $ carthage update --platform iOS
    
"--platform iOS" ensures that Carthage only builds frameworks for iOS. If you don’t specify a 
platform, Carthage will build frameworks for all platforms — often both Mac and iOS — supported by
the library.

6. Back to Xcode, we want to add the above file IQKeyboardManager.framework to the Linked 
Frameworks and Libraries of the project. Do so by dropping the IQKeyboardManager.framework file 
from a Finder window into the drop target (where it says “Add Files here”).

7. Switch to Build Phases tab.
7.1 - Click on + icon and select New run script phase
7.2 - Expand the Run Script section. Once expanded, in the Shell text field, type
    
    /usr/local/bin/carthage copy-frameworks
    
7.3 - Click on the + button under Input Files and type

    $(SRCROOT)/Carthage/Build/iOS/IQKeyboardManager.framework
    
7.4 - Check both checkboxes:
    1. Run script
    2. Show environment variables in build log
    
8. Double click on the Xcode project to open.

9. You can clean/re-build your project and run it.

#Remove external dependencies

For Removal we need to follow some steps-
1) Remove the Carthage Folder, Cartfile.resolved and Cartfile from Project Folder.
2) Go to Project Target in General tab, remove the Framework added in Framework, Embedded Section.
3) in Build Phase, Remove the Framework from Run Script Section.
4) If you added the Copy File Phase then remove that also.
5) Remove the import Code from the files where you using the Framework.
5) Clean and Build the target.

#Thanks
