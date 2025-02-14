# AgoraVideoSwiftUI

AgoraVideoSwiftUI is a package for building video call apps using the Agora RTC SDK and SwiftUI. It provides a set of SwiftUI views and classes that simplify setting up and managing Agora RTC sessions for video calls.

## Installation

AgoraVideoSwiftUI can be installed using Swift Package Manager in Xcode. Simply add the package to your project by navigating to File > Swift Packages > Add Package Dependency and entering the repository URL:

```
https://github.com/AgoraIO-Community/AgoraVideoSwiftUI.git
```


## Usage

To use AgoraVideoSwiftUI in your SwiftUI project, simply import the package and use the provided views and classes. For example, you can use `AgoraVideoCanvasView` and `AgoraManager` view to render all the video streams in an Agora RTC session:

```swift
import AgoraVideoSwiftUI
import AgoraRtcKit

struct AgoraGettingStartedView: View {
    @ObservedObject var agoraManager = AgoraManager(appId: <#AppId#>, role: .broadcaster)
    var channelId: String = "test"
    var body: some View {
        ScrollView {
            VStack {
                ForEach(Array(agoraManager.allUsers), id: \.self) { uid in
                    AgoraVideoCanvasView(agoraKit: agoraManager.engine, uid: uid)
                        .aspectRatio(contentMode: .fit).cornerRadius(10)
                }
            }.padding(20)
        }.onAppear {
            agoraManager.engine.joinChannel(
                byToken: <#Agora Temp Token#>, channelId: channelId, info: nil, uid: 0
            )
        }.onDisappear {
            agoraManager.engine.leaveChannel()
        }
    }
}
```

## Contributing

Contributions to AgoraVideoSwiftUI are welcome! If you encounter any issues or have feature requests, please submit an issue on the GitHub repository. Pull requests are also welcome.

## License

AgoraVideoSwiftUI is available under the MIT license. See the [LICENSE](LICENSE) file for more information.
