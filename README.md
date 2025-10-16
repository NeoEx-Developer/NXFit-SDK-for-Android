# NXFit-SDK-for-Android

This SDK is intended to be used to connect to NXFit services.

## Getting Started
The NXFit SDK is currently hosted on GitHub Packages. Follow these steps to add the SDK to your build:

### Create GitHub Access Token
GitHub provides maven packages only through authenticated connections.
- Login to GitHub (create an account if needed).
- Go to **Settings** &#8594; **Developer Settings** &#8594; **Personal access tokens** &#8594; **Tokens (Classic)**
- Click on **Generate new token (Classic)**
- Give the new token a meaningful name and the only scope required is **read:packages**.
- Since this token only requires **read:packages** set the expiration to whatever you feel comfortable with, however for this token scope *No Expiration* should be fine.
- Once the required scope is checked, click **Generate token**.
- Copy the generated access token and record it somewhere safe. You'll need it when updating the *build.gradle* files.

### Add the NXFit SDK GitHub Packages repository to your gradle build files
- Using the access token generated in the prior step, add the following maven repository to *settings.gradle* file:

        dependencyResolutionManagement {
            // ...
            repositories {
                // other repositories....
        
                // For nxfit-sdk from GitHub Packages
                maven {
                    name = "GitHubPackages"
                    url = uri("https://maven.pkg.github.com/NeoEx-Developer/NXFit-SDK-for-Android")
        
                    credentials {
                        username = YOUR_GITHUB_USERNAME
                        password = YOUR_GITHUB_ACCESS_TOKEN
                    }
                }
            }
        }

- Add the following dependency to your app's *build.gradle.kts* file:
  
        dependencies {
            implementation("com.neoex:nxfit-sdk:9.1.0")
        }
  
- Sync the project with Gradle files 

-  The [NXFit](com.neoex.nxfit.NXFit) interface is the main starting point. The NXFit class must be instantiated using the [NXFit.build](com.neoex.nxfit.NXFit.build) function. The [NXFit.build](com.neoex.nxfit.NXFit.build) function requires the following:  A reference to the [Application](android.app.Application) [Context](android.content.Context), an instance of [ConfigurationProvider](com.neoex.nxfit.ConfigurationProvider), the current user ID and an access token flow. Note that all these values are expected to remain valid for the entire lifecycle of the NXFit instance, with only the access token being refreshed as needed through the access token flow.
