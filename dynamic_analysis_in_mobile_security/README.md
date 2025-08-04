# Resources

## Read or watch

- CodeShare
- JNI Overview
- Android Developer Guide
- Android NDK Documentation
- Android Reverse Engineering (ARE)
- Android Security Documentation
- Reverse Engineering Guides
- Frida Documentation
- OWASP Mobile Application Security Testing Guide (MASTG)

# Tools

## Dynamic Analysis Tools

- ObjectionObjection
- Frida Official Site
- ADB Documentation
- GDB
- Ghidra
- IDA Pro

## Android Studio

- Android Studio

## Network Interception Tools

- Burp Suite
- mitmproxy
- Wireshark

## APK Analysis Tools

- APKTool
- jadx

## Programming and Scripting

- Python

# Learning Objectives

At the end of this project, you are expected to be able to explain to anyone, without the help of Google:

- What is dynamic analysis, and how does it differ from static analysis in mobile security?
- How can dynamic analysis be effectively applied to mobile applications to monitor real-time behavior?
- How can Frida be used to inject scripts, hook functions, and interact with applications at runtime?
- In what ways does Objection simplify Frida’s capabilities, and how can it assist in tasks like bypassing security features and extracting data?
- What techniques allow us to observe hidden functions and sensitive data handling in real-time?
- How can mobile applications’ interactions with system resources and their internal data flows be analyzed dynamically?
- How can we intercept and analyze an app’s network traffic to identify vulnerabilities in data transmission?
- What are effective methods for bypassing SSL pinning to gain deeper insight into network communications?
- What are common anti-debugging and anti-tampering techniques used in mobile apps?
- How can we bypass protections like root detection, code obfuscation, and method protection to facilitate a smoother dynamic analysis?
- What are best practices for documenting the dynamic analysis process, tool usage, and observed behaviors?
- How can identified vulnerabilities and sensitive findings be reported in a way that highlights risks and suggests improvements?

# Requirements

## General

- **Allowed Tools:** Frida, Objection, GDB, APKTool, JADX, Wireshark, mitmproxy, Android Debug Bridge (ADB), Burp Suite.
- **Environment:** All analyses should be conducted on an Android emulator or a physical device within a secure, controlled environment.
- **Backup:** Regularly back up APK files, scripts, and key data before and during the analysis process.
- **Execution Compatibility:** Ensure all scripts and tools can be executed and run on Kali Linux or a compatible analysis environment.
- **Path Management:** Use relative paths for all file references to avoid dependency on hardcoded paths.
- **Integrity Checks:** Validate APK and binary integrity before analysis to prevent issues due to corrupted or tampered files.
- **Tool Configuration:** Configure all monitoring and network tools correctly, including proxy and certificate settings, before beginning the analysis.
- **Documentation:** Maintain organized, clear, and detailed documentation for each step of the analysis, including findings and tool usage.
- **Focus:** Concentrate your analysis on the designated APK provided for the project.
- **Local Execution:** All work must be completed within the secure environment on the local machine or emulator; use of online tools or cloud services is not permitted for this project.

## Tasks

### 0. Android App Security (mandatory)

**Welcome to the Android Dynamic Analysis Challenge**

In this challenge, you’ll be provided with an APK that contains a hidden flag. Your objective is to perform dynamic analysis on the app, utilizing various tools and techniques to uncover the flag and complete the exercise.

This challenge is designed to help you practice reverse engineering and dynamic analysis techniques commonly used in mobile security assessments. You’ll need to run the app on a device or emulator and use dynamic analysis tools to intercept and manipulate the app’s runtime behavior.

For this challenge, you will analyze the APK by running it and using dynamic analysis tools to modify its behavior and extract the hidden flag.

**Tools:**

- Frida
- ADB (Android Debug Bridge)
- Objection
- Android Studio

**Instructions:**

1. **Set Up Your Environment**  
   - Device/Emulator: Use an Android device or emulator with debugging enabled.  
   - ADB Connection: Ensure you can connect to your device/emulator via ADB.

2. **Install the APK**  
   - Use `adb install <path_to_apk>` to install the provided APK on your device or emulator.

3. **Run the App**  
   - Launch the app to understand its basic functionality.  
   - Observe any user interface elements or interactions.

4. **Identify Target Methods**  
   - Static Analysis: Perform initial static analysis to identify interesting methods or classes to target with dynamic analysis tools.  
   - Hint: Look for methods related to generating or revealing the flag, such as `generateString`, `revealFlag`, or any methods that take a seed or key as a parameter.

5. **Use Frida to Hook Methods**  
   - Write a Frida Script: Create a script to hook into the target method(s) and modify parameters or observe return values.  
   - Modify Runtime Behavior: Change the seed value or intercept method calls to manipulate how the app generates the flag.  
     - **Example:** Intercept the `generateString(seed)` method and try different seed values to find the one that reveals the flag.

6. **Automate Testing**  
   - Loop Through Seed Values: Automate the process of testing multiple seed values by looping through a range (e.g., 0 to 1000).  
   - Check for the Flag: After modifying the seed, observe the output to see if the generated string matches the expected flag format.

7. **Extract the Flag**  
   - Once you’ve found the correct seed that generates the flag, record the flag.  
   - Ensure the flag matches the format specified in the challenge (e.g., starts with `Holberton{` and ends with `}`).

**General Hints for Success**

- Understand the App’s Logic: Before hooking methods, try to understand how the app works and what methods are likely involved in flag generation.
- Start Simple: Begin by hooking methods that are easy to intercept, then move on to more complex interactions.
- Use Logging: In your Frida scripts, use `console.log()` to output information that can help you understand what’s happening.
- Handle Errors: Ensure your scripts handle exceptions or errors to avoid crashes.
- Automate Carefully: When automating tests (e.g., looping through seeds), ensure you manage resources and avoid overloading the app or device.

**Target APK:** `Apk_task0`  
**Repo:**  
- GitHub repository: `holbertonschool-mobile_Security`  
- Directory: `dynamic_analysis_in_mobile_security`  
- File: `0-flag.txt`

### 1. Hooking Native Functions in Android (mandatory)

In this challenge, you will explore the dynamic analysis of an Android application that utilizes native code through the Java Native Interface (JNI).

Your goal is to analyze and manipulate native functions using Frida to intercept, modify, and extract the decrypted flag from the application’s native code.

**Objective:**

- Perform dynamic analysis to hook into a native function within the Android application and retrieve the decrypted flag that is processed in the native code but not displayed in the app interface.

**Tools:**

- Frida
- ADB (Android Debug Bridge)
- Objection
- Android Studio

**Instructions:**

1. Analyze App Behavior: Launch the app and familiarize yourself with its functionality and user interface.
2. Identify the Native Library: Locate the native library (e.g., `libnative-lib.so`).
3. Intercept Native Functions with Frida: Attach Frida to the running app and hook into the native function `getSecretMessage`.
4. Extract the Flag from Native Code: Observe and manipulate the data processed by the hooked function to retrieve the hidden flag.

**Hints**

- Utilize Frida’s scripting capabilities to hook and modify the behavior of the native functions.
- Use Frida’s `Interceptor.attach()` method to hook the function dynamically.
- Use `adb logcat` to monitor the app’s logs, which may provide useful information during your analysis.
- Explore Objection for additional convenience in hooking and inspecting the app.
- Check JNI function exports using `frida -U -n <package_name> -ito list loaded symbols`.

**Deliverables**

- A report detailing the process of hooking the native function and the methods used to extract the hidden flag.
- The decrypted flag obtained from the native function.
- A step-by-step report detailing how you identified, hooked, and extracted the flag.

**Target APK:** `Apk_task1`  
**Repo:**  
- GitHub repository: `holbertonschool-mobile_Security`  
- Directory: `dynamic_analysis_in_mobile_security`  
- File: `1-flag.txt`, `1-report.md`

### 2. Android Cryptography Challenge: Intercepting and Decrypting Data (mandatory)

In this challenge, you will analyze an Android application that communicates with a remote server using encrypted data. Your objective is to intercept the communication, analyze the cryptographic mechanisms, manipulate the data, and ultimately decrypt the hidden flag.

**Objective:**

- Capture and manipulate HTTP requests between the Android application and the server.
- Analyze the application’s cryptographic implementation (e.g., AES, RSA).
- Decrypt the encrypted data and extract the hidden flag.

**Tools:**

- Burp Suite
- mitmproxy
- Wireshark
- APKTool
- jadx

**Instructions:**

1. Set Up Your Environment  
   - Ensure your Android device/emulator is running with debugging enabled.  
   - Configure your interception tool (Burp Suite or mitmproxy) to capture network traffic.

2. Intercept HTTP Traffic  
   - Use Burp Suite or mitmproxy to capture requests between the app and the server.  
   - Log the encrypted responses received from the server.

3. Analyze the APK  
   - Decompile the APK using APKTool or jadx.  
   - Identify cryptographic functions (e.g., AES decryption, RSA key usage).  
   - Locate where encryption keys are stored or derived.

4. Modify and Decrypt Data  
   - Intercept and alter HTTP responses to manipulate how the app processes encrypted data.  
   - Apply cryptographic techniques to decrypt and retrieve the hidden flag.

**Hints**

- Use Burp Suite’s request/response modification features to analyze encrypted data.
- Focus on cryptographic functions in the decompiled code (AES, RSA, Base64 encoding).
- Check how the app manages encryption keys—weak key storage can lead to vulnerabilities.
- Ensure your network interception is working correctly by verifying captured traffic.

**Deliverables**

- A report detailing the process of intercepting, manipulating, and decrypting the communication, including any challenges faced.
- The hidden flag extracted from the decrypted data.

**Target APK:** `Apk_task2`  
**Repo:**  
- GitHub repository: `holbertonschool-mobile_Security`  
- Directory: `dynamic_analysis_in_mobile_security`  
- File: `2-flag.txt`, `2-report.md`

### 3. Android Security Challenge: Revealing Hidden Functions (mandatory)

Welcome to the Revealing Hidden Functions challenge! This task is designed to enhance your skills in reverse engineering, dynamic analysis, and application security. You will work with a custom Android application that contains hidden functions responsible for retrieving a secret message (the flag). Your objective is to locate and invoke these hidden functions using advanced analysis tools.

**Objectives:**

- Enhance Reverse Engineering Skills: Learn to dissect and understand application binaries without source code access.
- Master Dynamic Analysis Tools: Gain hands-on experience with tools like Frida, Objection, and GDB to manipulate and analyze running applications.
- Understand Application Security: Appreciate the importance of secure coding practices to protect sensitive functions and data within applications.

**Tools:**  
- Android Studio (latest version recommended)  
- Android Device or Emulator (API level 24 or higher)  
- Frida  
- Objection  
- GDB  
- APKTool  
- jadx  
- Python (for running helper scripts)

**Instructions:**  
1. Decompile the Android application using tools like APKTool or jadx to inspect its code and understand its structure.  
2. Identify any obfuscated or hidden methods that could potentially reveal the secret.  
3. Use dynamic analysis tools such as Frida or Objection to hook into the application’s runtime.  
4. Locate the hidden functions responsible for decrypting and displaying the secret.  
5. Invoke these functions to retrieve the secret message.  
6. Understand the encoding mechanism used within the hidden functions.  
7. Reverse the encoding to reveal the original secret message.

**Hints**  
- Utilize Frida scripts to dynamically hook into method calls and alter application behavior.  
- Use Objection to make it easier to explore the app’s runtime and bypass security features.  
- Monitor log outputs during execution to identify any relevant information about hidden functions.  
- Pay attention to how data is passed between functions; understanding parameters will aid in successfully invoking them.

**Deliverables**  
- A report detailing the process of locating, invoking, and retrieving the hidden functions, including any challenges faced.  
- The decrypted flag obtained from the hidden functions.

**Target APK:** `Apk_task3`  
**Repo:**  
- GitHub repository: `holbertonschool-mobile_Security`  
- Directory: `dynamic_analysis_in_mobile_security`  
- File: `3-flag.txt`, `3-report.md`  

