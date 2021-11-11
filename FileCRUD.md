#### What is Bundle

On Apple’s platforms, apps are distributed as bundles, which means that in order to access internal files that we’ve included (or bundled) within our own app, we’ll first need to resolve their actual URLs by searching for them within our app’s main bundle.
That main bundle can be accessed using Bundle.main, which lets us retrieve any resource file that was included within our main app target
