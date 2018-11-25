# Xcode Concepts

## xcodebuild commands

* `xcodebuild build`- builds the project to run on simulators \(add scheme/workspace/project\)
* `xcodebuild analyze` - static analysis of the project 
* `xcodebuild test` - builds the project and runs the tests 
* `xcodebuild build-for-testing` - builds the project for testing \(use with `test-without-building`\)
* `xcodebuild test-without-building` - run the tests on multiple simulators without building
* `xcodebuild archive` - creates an xcarchive for the project
* `xcodebuild -exportArchive` - exports a given archive as an IPA file

Tool to upload the IPA to iTunes connect - ALTool \(Application Loader Tool\)

Location of the tool: _/Applications/Xcode.app/Contents/Applications/Application Loader.app/Contents/Frameworks/ITunesSoftwareService.framework/Support/altool_

