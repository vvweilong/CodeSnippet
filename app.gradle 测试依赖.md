    // Testing-only dependencies
        // Force usage of support annotations in the test app, since it is internally used by the runner module.
        androidTestCompile 'com.android.support:support-annotations:' + rootProject.supportLibVersion;
        androidTestCompile 'com.android.support.test:runner:' + rootProject.runnerVersion;
        androidTestCompile 'com.android.support.test:rules:' + rootProject.rulesVersion;
        androidTestCompile 'com.android.support.test.espresso:espresso-core:' + rootProject.espressoVersion;