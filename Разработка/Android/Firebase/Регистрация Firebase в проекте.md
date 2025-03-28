#Firebase #server #Gradle 
### Добавление файла google-services.json

![[Pasted image 20250328101815.png]]
### Подключение Firebase в проект:

*build.gradle.kts (:app) Подключение на уровне модуля*
```kotlin
plugins {  
    alias(libs.plugins.android.application)  
    id("com.google.gms.google-services")  
}

dependencies {  
    implementation(libs.appcompat)  
    implementation(libs.material)  
    implementation(libs.activity)  
    implementation(libs.constraintlayout)  
    testImplementation(libs.junit)  
    androidTestImplementation(libs.ext.junit)  
    androidTestImplementation(libs.espresso.core)  
  
    implementation ("androidx.tracing:tracing:1.2.0")  
    implementation(platform("com.google.firebase:firebase-bom:33.11.0"))  
    implementation("com.google.firebase:firebase-auth")  
}
```

*build.gradle.kts (:app) Подключение на уровне проекта*
```kotlin
plugins {  
    alias(libs.plugins.android.application) apply false  
    id("com.google.gms.google-services") version "4.4.2" apply false  
}
```


