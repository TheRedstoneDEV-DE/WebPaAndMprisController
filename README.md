
<p align="center">
 <img width="140px" src="https://github.com/TheRedstoneDEV-DE/WebPaAndMprisController/blob/main/PinguControll.png" align="center" alt="GitHub Readme Stats" />
 <h2 align="center">PinguControll</h2>
 <p align="center">A simple webui to control PulseAudio (or Pipewire) and any mediaplayer with MPRIS on linux.
This project was just created since all software I found in this direction was deprecated or not working, so I created my own.
</p>
</p>
  <p align="center">
    <a href="https://github.com/TheRedstoneDEV-DE/VoiceAssistant/releases">
      <img alt="GitHub Release" src="https://img.shields.io/github/release/theredstonedev-de/voiceassistant" />
    </a>
    <a href="https://github.com/TheRedstoneDEV-DE/VoiceAssistant/issues">
      <img alt="Issues" src="https://img.shields.io/github/issues/theredstonedev-de/voiceassistant?color=0088ff" />
    </a>
    <a href="https://github.com/TheRedstoneDEV-DE/VoiceAssistant/pulls">
      <img alt="GitHub pull requests" src="https://img.shields.io/github/issues-pr/theredstonedev-de/voiceassistant?color=0088ff" />
    </a>
    <br />
  </p>
  

<p align="center">
⚠️ This is still Work-In-Progress Software!
</p>
  <br />
<hr>


## Requirements 
- A PC running linux
- A recent JRE / JDK version, minimum is Java 18
- An audio server compatible with pactl (tested on Pipewire)
- Maven for building the project

<br />
<hr>

## Configuring
1. Change the allowed hosts like you need them in `src/main/java/me/theredstonedevde/pawebctl/WebServer.java` (line 18-23)
```java
...
public class WebServer {
    private static final String[] APPROVED_IP_ADDRESSES = {
        "192.168.21.117", //host pc
        "192.168.21.118", //controlpanel or client for the web interface
        "127.0.0.1" //localhost
    };
...
```
2. Configure the MPRIS interface (optional if you use the plasma-browser-extension) in `src/main/java/me/theredstonedevde/mprisctl/MPRISctl.java` (line 13-18)
```java
...
	PlasmaBrowserExtension pbe;
	DBusConnection dbusconnection;
	String MPRIS_BUSNAME = "org.mpris.MediaPlayer2.plasma-browser-integration"; // <--- change busname
	String MPRIS_OBJECTPATH = "/org/mpris/MediaPlayer2"; // <--- change objectpath (only required in some cases)
	public void init() {
		try {
...
```
You can get these values by using the program d-feet.
  You just open the program switch to "Session Bus", filter for mpris and grab the player you want to control.

Now you are ready to compile the code!

<br />
<hr>

## Compiling
1. Go to the repository root and execute 
   `mvn install dependency:copy-dependencies`.
   The process should complete with "BUILD SUCCSESSFUL" if not you're always welcome to create an issue!

2. Run the program!
   Run the program with
   `java -cp target/dependency/*:target/PaMprisController-1.0-SNAPSHOT.jar me.theredstonedevde.pawebctl.WebServer`

3. Open the webui!
   The webui runs under http://127.0.0.1:8193/ or http://<your pc's IP here>:8193/
