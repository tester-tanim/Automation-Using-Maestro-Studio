# Web, Android, IOS Automation Using Maestro Studio

appId: com.yourcompany.yourapp   # Change to your Android package / iOS Bundle ID
# For web testing:
# tags:
#   - web

---
# 1. Launch App (or open website)
- launchApp
# - openLink: https://example.com            # Web only

# 2. Wait for animations & optional permissions
- waitForAnimationToEnd
- tapOn:
    text: "Allow"
    optional: true
- tapOn:
    text: "While using the app"
    optional: true

# 3. Input Text
- tapOn: "Email or username"
- inputText: "testuser@example.com"
- hideKeyboard

- tapOn: "Password"
- inputText: "SuperSecret123!"
- hideKeyboard

# 4. Tap / Click
- tapOn: "Log In"
# - tapOn: { id: "login_btn" }               # by resource-id / accessibilityIdentifier

# 5. Double Tap
- doubleTapOn: "Profile Picture"

# 6. Scroll / Swipe
- scroll                                     # Auto-scroll down
- swipe:
    direction: DOWN
    duration: 1000
- swipe:
    direction: UP
    duration: 800
- swipe:                                      # Pull-to-refresh
    start: "50%,80%"
    end: "50%,20%"
    duration: 600

# 7. Long Press
- longPressOn:
    text: "Post Options"
    duration: 1500
- tapOn: "Delete"

# 8. Assertions (will fail the test if not met)
- assertVisible: "Home"
- assertVisible:
    text: "Welcome back"
    timeout: 15000
- assertNotVisible: "Login"

# 9. Take Screenshot
- takeScreenshot: screenshots/home_screen.png

# 10. Take Video Recording
- startRecording
- tapOn: "Search"
- inputRandomText
- tapOn: "First Result"
- scroll
- stopRecording: videos/search_demo.mp4

# 11. Back & Key Press
- back
- pressKey: Enter

# 12. Repeat Actions (e.g., infinite scroll test)
- repeat:
    times: 6
    commands:
      - scroll
      - delay: 1000

# 13. Conditional Flow (Maestro ≥1.33)
- extendedWaitUntil:
    visible: "Skip Tutorial"
    timeout: 5000
- tapOn:
    text: "Skip Tutorial"
    optional: true

# 14. Clean app state (optional, for fresh runs)
# - eraseAppData
# - launchApp
