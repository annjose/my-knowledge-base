# AB Testing

Various options are available to do AB Testing - LaunchDarkly, Firebase Remote Config, Optimizely

* LaunchDarkly
* Firebase - [https://firebase.google.com/docs/remote-config/config-analytics](https://firebase.google.com/docs/remote-config/config-analytics)
* Optimizely -

**Firebase Remote Config**

Remote Config allows you to set defaults in your app that can be overridden from the Firebase console. With Analytics, you can segment your users and measure the impact of your A/B tests.

Remote Config is Firebase's equivalent of LaunchDarkly. You can combine Remote Config and Google Analytics for Firebase to implement AB Testing in your app. Analytics allows you to define "user properties"; and then you can create conditions based on these user properties. You can combine these user properties with Remote Config rules \(eg: OS type = iOS, country = Canada etc\)

Details - [https://firebase.google.com/docs/remote-config/parameters](https://firebase.google.com/docs/remote-config/parameters)

#### Good Articles {#good-articles}

* [https://willowtreeapps.com/ideas/how-feature-toggles-can-enable-ab-testing-in-mobile-apps](https://willowtreeapps.com/ideas/how-feature-toggles-can-enable-ab-testing-in-mobile-apps)

