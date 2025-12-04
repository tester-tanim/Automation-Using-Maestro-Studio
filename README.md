# Web, Android, IOS Automation Using Maestro Studio

# Maestro UI Test Flow – Full Example (Copy & Run!)

Copy the entire code block below and save it as `example-flow.yaml` in your `.maestro/flows/` folder.

```yaml
appId: com.yourcompany.yourapp   # Change to your app's package (Android) or Bundle ID (iOS)

---
# Launch app & handle permissions
- launchApp
- waitForAnimationToEnd
- tapOn:
    text: "Allow|While using the app|OK"
    optional: true
    regex: true

# Login
- tapOn: "Email|Username"
- inputText: "testuser@example.com"
- hideKeyboard
- tapOn: "Password"
- inputText: "SuperSecret123!"
- hideKeyboard
- tapOn: "Log In|Sign In|Continue"

# Double tap on profile
- doubleTapOn: "Profile Picture|Avatar"

# Scroll feed
- repeat:
    times: 5
    commands:
      - scroll
      - delay: 800

# Swipe actions
- swipe:
    direction: DOWN
    duration: 1000
- swipe:                                  # Pull to refresh
    start: "50%,80%"
    end: "50%,20%"
    duration: 600

# Long press & delete
- longPressOn:
    text: "Post|Item"
    duration: 1500
- tapOn: "Delete|Remove"
- tapOn: "Confirm"

# Input random data (great for sign-up tests)
- tapOn: "Name"
- inputRandomPersonName
- tapOn: "Email"
- inputRandomEmail

# Assertions – fail fast if wrong screen
- assertVisible:
    text: "Home|Dashboard|Feed"
    timeout: 15000
- assertNotVisible: "Log In"

# Take proof
- takeScreenshot: screenshots/home_after_login.png

# Record a short video
- startRecording
- tapOn: "Search"
- inputRandomText
- tapOn: "First Result"
- scroll
- stopRecording: videos/search_demo.mp4

# Final navigation
- back
- back
- pressKey: Home                            # Android only

```
# How to Run
# On emulator / iOS simulator
maestro test flows/example-flow.yaml

# On real Android device (watch it live with Vysor!)
maestro test --device <your-device-id> flows/example-flow.yaml


