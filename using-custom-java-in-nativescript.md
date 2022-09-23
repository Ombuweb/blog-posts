## How to use Java code in NativeScript

In this post, I will show you how to use the Java code you write in Android Studio in a Nativescript app. This solution resulted from me implementing the [Room Persistence](https://developer.android.com/jetpack/androidx/releases/room) library for Nativescript.

To use the Java code in Nativescript, you have two places to put it into, as illustrated in the following image from the [Nativescript](https://docs.nativescript.org/app-resources.html#adding-native-code-to-an-application) docs: 
[native-code-location.png](/assets/how-to-use-java-in-nativescript/native-code-location.png)
You either use the individual Java classes or package them into a library and use that library. In both cases, you should add the necessary dependencies to the ```app.gradle```. In the case of the Room library, you need to add the following dependencies:

[app-gradle.png](/assets/how-to-use-java-in-nativescript/app-gradle.png)
Even if you decide to use the Java classes directly and not via the ```.aar```, if you're using Typescript you'll still need to generate the ```.aar``` file, if you want to generate types for IntelliSense.

What I usually do is write and test the code I need in Android Studio, and when I'm satisfied:
1. I convert the project(app module) to a library module by following steps 1-4 at [Convert an app module to a library module](https://developer.android.com/studio/projects/android-library#Convert).
2. Package the library module, containing all the classes, into a ```.aar``` file. The image below shows the steps to take in order to produce the ```.aar``` file:
[create-aar-file.png](/assets/how-to-use-java-in-nativescript/create-aar-file.png) You can find the generated file at the location shown below:
[aar-file-location.png](/assets/how-to-use-java-in-nativescript/aar-file-location.png)

3. Drag and drop the ```app-release.aar``` onto ```The Archiver``` or a similar tool to get the ```classes.jar``` file that you use to generate the types for IntelliSense.
4. To generate the types, run ```ns typings android –jar <path to the .jar >``` file from step 4.
5. Reference the generated ```android.d.ts```(you can rename it appropriately) file in the ```reference.d.ts```. 

[reference-types.png](/assets/how-to-use-java-in-nativescript/reference-types.png).

Now when you type the full package name(```com.ombuweb.testroomdb```) the Java classes get suggested in VS Code: 
![IntelliSense-in-action.png](/assets/how-to-use-java-in-nativescript/IntelliSense-in-action.png").

See this Nativescript app [demo](https://github.com/Ombuweb/testApp.git) using the Java code . You can find the Java code [here](https://github.com/Ombuweb/test-roomdatabase.git)

I hope you find this post useful.

### Environment
* The Android Studio in the images: **4.1.1**
