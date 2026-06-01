Before we start: If you haven't downloaded the Example Assets from Session 2 (with the Audio file) [Download the Example Assets](https://juliannetzer.de/downloads/AssetsSRH2.zip)


# <a name="spatialaudio"></a>Spatial Audio

Spatial audio in Unity simulates how sounds change based on their position relative to the listener, creating a more immersive experience. It takes into account distance, direction, and environmental effects to make sounds feel like they are coming from specific locations in 3D space.

## Audio Listener & Audio Sources

### Audio Listener 
The Audio Listener component, usually attached to the Main Camera, represents the player's "ears" and determines how sound is perceived in the scene. Only one Audio Listener should be active at a time.

### Audio Source
Audio Sources are attached to GameObjects that produce sound. They determine volume, pitch, spatial blend, and 3D positioning of the audio.
![](images/Audio1.jpg)

With "Min Distance" and "Max Distance" you can set the minimum and maximum distance of audibility. 
![](images/Audio2.jpg)

With the "Volume Rolloff" you can select different Rolloff algorithms. Select "Linear Rolloff" if you want to hear a strong difference based on the positioning, "Logarithmic Rolloff" for a more realistic effect. 
![](images/Audio3.jpg)