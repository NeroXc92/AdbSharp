# Media
Control Android playback system
``` csharp
Media pb = handle.Media;
```
## Methods
Play/Pause:
``` csharp
// Emulate android keycode KEYCODE_MEDIA_PLAY_PAUSE
pb.PlayPause();
```
Play:
``` csharp
// Emulate android keycode KEYCODE_MEDIA_PLAY
pb.Play();
```
Pause:
``` csharp
// Emulate android keycode KEYCODE_MEDIA_PAUSE
pb.Pause();
```
Stop:
``` csharp
// Emulate android keycode KEYCODE_MEDIA_STOP
pb.Stop();
```
Previous:
``` csharp
// Emulate android keycode KEYCODE_MEDIA_PREVIOUS
pb.Previous();
```
Next:
``` csharp
// Emulate android keycode KEYCODE_MEDIA_NEXT
pb.Next();
```