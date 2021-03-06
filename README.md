# Starter kit for react-native app

> This doc is for:

- People wanting to creat a new RN app
- Integrating AppCenter SKD

# Create new App

>

First, run react-native command to create a new project

```sh
react-native init app-name
```

## Get app running

Should get the app running after excuting this command 

```sh
react-native run-ios
react-native run-android

```
## More Scripts

You can check all common used scripts in package.json via [common scripts ](http://example.com/ "Title")  

[This link](http://example.net/) has no title attribute. 

#Integrate Appcenter SDK

First you should create new apps in [AppCenter](https://appcenter.ms/)

## Add crash report
First add dependecies

```sh
yarn add appcenter appcenter-analytics appcenter-crashes

```

Link to project

```sh
react-native link
```

AppCenter [sdk get start](https://docs.microsoft.com/en-us/appcenter/sdk/getting-started/react-native)

#Use App Center CLI

Install App Center CLI in local

```sh
npm install -g appcenter-cli
```
More infomation [App Center CLI](https://docs.microsoft.com/en-us/appcenter/distribution/codepush/)


Checkout more scripts via [Management CLI](link to cli doc)

## App Center Code push

First install code push 

```sh
npm install --save react-native-code-push
```

Then link libs

```sh
react-native link react-native-code-push
```
###Plugin Installation (iOS - CocoaPods)

1. Add the React Native and CodePush plugin dependencies to your Podfile, pointing at the path where NPM has installed modules

	```
	# React Native requirements
	pod 'React', :path => '../node_modules/react-native', :subspecs => [
	   'Core',
	   'CxxBridge', # Include this for RN >= 0.47
	   'DevSupport', # Include this to enable In-App Devmenu if RN >= 0.43
	   'RCTText',
	   'RCTNetwork',
	   'RCTWebSocket', # Needed for debugging
	   'RCTAnimation', # Needed for FlatList and animations running on native UI thread
	   # Add any other subspecs you want to use in your project
	]
	# Explicitly include Yoga if you are using RN >= 0.42.0
	pod 'yoga', :path => '../node_modules/react-native/ReactCommon/yoga'
	pod 'DoubleConversion', :podspec => '../node_modules/react-native/third-party-podspecs/DoubleConversion.podspec'
	pod 'glog', :podspec => '../node_modules/react-native/third-party-podspecs/glog.podspec'
	pod 'Folly', :podspec => '../node_modules/react-native/third-party-podspecs/Folly.podspec'
	
	# CodePush plugin dependency
	pod 'CodePush', :path => '../node_modules/react-native-code-push'
	```

2. Run pod install

#### Manually install

[Plugin Installation (iOS - Manual) ](https://docs.microsoft.com/en-us/appcenter/distribution/codepush/react-native#plugin-installation-ios---manual)

### Plugin Installation(Android)

Basicly you do not need to change anything

[Android Setup](https://docs.microsoft.com/en-us/appcenter/distribution/codepush/react-native#android-setup)



### Windows setup

[Windows Setup](https://docs.microsoft.com/en-us/appcenter/distribution/codepush/react-native#windows-setup)

### Release new deployment to App Center

After code change, can run this to push code to app center 

```appcenter 
appcenter codepush release-react -a <ownerName>/<appName> 

```


Login ->appcenter login

List profile -> appcenter profile list

Logout-> appcenter logout

List tokens ->appcenter tokens list

Create Token -> appcenter tokens create -d "NEW_TOKEN_NAME"

Create Apps -> appcenter apps create -d <appDisplayName> -o <operatingSystem>  -p <platform> 
 
 (ie:appcenter apps create -d MyApp-Android -o Android -p React-Native)
 
Add deployments -> appcenter codepush deployment add -a <ownerName>/<appName> Staging
 
 
appcenter codepush deployment add -a <ownerName>/<appName> Production
                
With the original CodePush, apps automatically had two deployments (Staging and Production). 
  
Rename app names -> appcenter apps update -n <newName> -a <ownerName>/<appName>
 
Delete Apps -> appcenter apps delete -a <ownerName>/<appName>
 
List Apps -> appcenter apps list

Remove deployment -> appcenter codepush deployment remove -a <ownerName>/<appName> <deploymentName>
 
Rename deployment -> appcenter codepush deployment rename -a <ownerName>/<appName> <deploymentName> <newDeploymentName>
 
List deployments -> appcenter codepush deployment list -a <ownerName>/<appName>
 
Release update -> appcenter codepush release-react -a <ownerName>/<appName> -d <deploymentName> -t <targetBinaryVersion> 

They do have a rollback command, but tired and seems does not work, and the good solution is release a new development.

List codepush history -> appcenter codepush deployment history -a <ownerName>/<appName> <deploymentName>



Android set-up

Add lib 

npm install --save react-native-code-push

Link lib

react-native link react-native-code-push

recommond to use pod file

```
# React Native requirements
pod 'React', :path => '../node_modules/react-native', :subspecs => [
   'Core',
   'CxxBridge', # Include this for RN >= 0.47
   'DevSupport', # Include this to enable In-App Devmenu if RN >= 0.43
   'RCTText',
   'RCTNetwork',
   'RCTWebSocket', # Needed for debugging
   'RCTAnimation', # Needed for FlatList and animations running on native UI thread
   # Add any other subspecs you want to use in your project
]
# Explicitly include Yoga if you are using RN >= 0.42.0
pod 'yoga', :path => '../node_modules/react-native/ReactCommon/yoga'
pod 'DoubleConversion', :podspec => '../node_modules/react-native/third-party-podspecs/DoubleConversion.podspec'
pod 'glog', :podspec => '../node_modules/react-native/third-party-podspecs/glog.podspec'
pod 'Folly', :podspec => '../node_modules/react-native/third-party-podspecs/Folly.podspec'

# CodePush plugin dependency
pod 'CodePush', :path => '../node_modules/react-native-code-push'
```
After add above script , run ## pod install
 more info https://docs.microsoft.com/en-us/appcenter/distribution/codepush/react-native
 
 Run delpoyment list to retrieve the deployment key
  ## appcenter codepush deployment list -a <ownerName>/<appName>  
 
 App Center can only upload new versions to existing apps that are already published on the App Store or TestFlight.
