# 🔌 Adapter Pattern — Overview

## 🎯 Goal
Convert the interface of a class into another interface **clients expect**.  
Allows incompatible interfaces to work together.

---

## 🔹 Why Use Adapter
- When you want to **reuse existing classes** with a different interface.  
- Provides **compatibility** between systems without changing existing code.

---

## 🧱 Example
```java
// Target interface
interface MediaPlayer {
    void play(String audioType, String fileName);
}

// Adaptee (existing class)
class AdvancedMediaPlayer {
    void playVlc(String fileName) { System.out.println("Playing VLC: " + fileName); }
    void playMp4(String fileName) { System.out.println("Playing MP4: " + fileName); }
}

// Adapter
class MediaAdapter implements MediaPlayer {
    AdvancedMediaPlayer advancedMusic;

    public MediaAdapter(String audioType) {
        advancedMusic = new AdvancedMediaPlayer();
    }

    public void play(String audioType, String fileName) {
        if(audioType.equalsIgnoreCase("vlc")) advancedMusic.playVlc(fileName);
        else if(audioType.equalsIgnoreCase("mp4")) advancedMusic.playMp4(fileName);
    }
}

// Client
class AudioPlayer implements MediaPlayer {
    MediaAdapter adapter;

    public void play(String audioType, String fileName) {
        if(audioType.equalsIgnoreCase("mp3")) {
            System.out.println("Playing MP3: " + fileName);
        } else if(audioType.equalsIgnoreCase("vlc") || audioType.equalsIgnoreCase("mp4")) {
            adapter = new MediaAdapter(audioType);
            adapter.play(audioType, fileName);
        } else {
            System.out.println("Invalid media type: " + audioType);
        }
    }
}

// Usage
public class Main {
    public static void main(String[] args) {
        AudioPlayer player = new AudioPlayer();
        player.play("mp3", "song.mp3");
        player.play("vlc", "video.vlc");
        player.play("mp4", "movie.mp4");
    }
}
```

---

## ⚙️ Summary
| Feature | Adapter Pattern |
|---------|----------------|
| Purpose | Make incompatible interfaces compatible |
| Client code | Uses target interface, unaware of adaptee |
| Use cases | Legacy code integration, API adapters |