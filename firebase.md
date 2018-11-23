# Firebase

Firebase provides a set of services for mobile applications. The services include Performance Tracking, TestLab, Storage, Authentication etc.

One good thing is that each of these services are published as sub-specs so you can pick and choose the capabilities that you want.eg: `Firebase/Auth`, `Firebase/Core`, `Firebase/PerformanceMonitoringetc.`

### Remote Config

Allows the configuration of the app to change based on users / segments etc. Equivalent to LaunchDarkly

### Performance Tracking

* Provides automatic performance tracking for network calls
  * You can also track specific actions using `Performance.startTrace`, `Performance.incrementCounter`and `Performance.stop`

#### Test Lab <a id="test-lab"></a>

[https://firebase.google.com/docs/test-lab/](https://firebase.google.com/docs/test-lab/)

