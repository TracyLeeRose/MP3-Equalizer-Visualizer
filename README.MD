# Amplitude Depth 3D Audio Visualizer

A web-based audio player that visualizes music in a dynamic 3D point cloud. It maps audio frequency, amplitude, and perceived loudness (depth) onto a 3D space, offering interactive controls for both the audio output and the visual representation.

![Placeholder GIF/Screenshot](placeholder.gif)
*(Replace `placeholder.gif` with an actual screenshot or GIF of the visualizer)*

## Features ✨

*   **3D Audio Visualization:** Renders audio frequency data in real-time using Three.js.
    *   **X-axis:** Frequency (Logarithmic scale: 20Hz - 20kHz)
    *   **Y-axis:** Amplitude (Normalized signal strength)
    *   **Z-axis:** Depth (Mapped to amplitude, creating a sense of forward/back movement for louder sounds)
*   **Audio Playback:** Supports loading and playing local MP3, WAV, and OGG files.
*   **Interactive 3D Controls:**
    *   Use mouse/touch to rotate, pan, and zoom the visualization (via OrbitControls).
    *   Toggle automatic rotation of the scene.
*   **Frequency Band Control:**
    *   **Mute Ranges:** Selectively apply notch filters to the *audio output* for specific frequency bands (e.g., mute human voice range).
    *   **Highlight Ranges:** Visually highlight specific frequency bands in the *3D plot* with distinct colors (e.g., highlight bass frequencies).
    *   **Targeted Ranges:** Includes controls for common ranges like human voice, presence, sibilance, and higher harmonics.
    *   **Unselect All:** Quickly disable all active filters and highlights.
*   **Responsive Design:** The layout adjusts to different screen sizes.
*   **Dark Theme:** Easy-on-the-eyes interface.

## How to Use 🚀

1.  **Get the Code:**
    *   Clone the repository: `git clone https://github.com/your-username/your-repo-name.git`
    *   *OR* Download the `index.html` file directly.
2.  **Open the File:** Open the `index.html` file in a modern web browser (like Chrome, Firefox, Edge, Safari) that supports the Web Audio API and WebGL.
3.  **Load Audio:** Click the "Choose File" button and select an MP3, WAV, or OGG audio file from your computer.
4.  **Play:** Use the standard HTML5 audio player controls (play/pause, seek, volume).
5.  **Explore:**
    *   Click and drag on the visualization to rotate the view.
    *   Scroll (or use pinch-zoom) to zoom in and out.
    *   Right-click and drag (or two-finger drag) to pan the view.
    *   Click the "Stop/Start Rotation" button to toggle the automatic rotation.
6.  **Control Frequencies:** Use the checkboxes in the left sidebar to:
    *   Mute specific frequency ranges in the audio playback.
    *   Highlight corresponding ranges in the 3D visualization.
    *   Click "Unselect All" to clear all selections.

## Technical Details 🛠️

*   **Frontend:** Plain HTML, CSS, and JavaScript. No build process required.
*   **Audio Processing:** Uses the [Web Audio API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Audio_API):
    *   `AudioContext` for managing audio operations.
    *   `MediaElementAudioSourceNode` to link the `<audio>` element.
    *   `AnalyserNode` to get real-time frequency and amplitude data (`getByteFrequencyData`).
    *   `BiquadFilterNode` (configured as `notch` or `allpass`) to selectively filter audio frequencies based on user selections. Filters are chained sequentially.
*   **3D Rendering:** Uses [Three.js](https://threejs.org/):
    *   `WebGLRenderer` for drawing onto the `<canvas>`.
    *   `PerspectiveCamera` for the 3D view.
    *   `Scene` to hold all objects.
    *   `Points` with `BufferGeometry` to represent the frequency data. Point positions and colors are updated dynamically in the animation loop based on `AnalyserNode` data.
    *   `OrbitControls` for user interaction with the 3D scene.
    *   Axes and labels are created using `Line` segments and `Sprite`s with canvas textures.

## Dependencies

*   [Three.js](https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js) (r128) - via CDN
*   [THREE.OrbitControls](https://cdn.jsdelivr.net/npm/three@0.128.0/examples/js/controls/OrbitControls.js) - via CDN

## Known Issues / Limitations

*   Requires a modern browser with WebGL and Web Audio API support.
*   Performance may vary depending on the user's hardware and the complexity of the audio.
*   Due to browser security policies, the `AudioContext` may start in a 'suspended' state and require user interaction (like clicking the page or the play button) to resume and enable audio processing/playback.
*   The accuracy of frequency-to-X-axis mapping depends on the logarithmic scale approximation.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request or open an Issue.

## License

This project is licensed under the [MIT License](LICENSE). (You would need to add a LICENSE file, typically containing standard MIT license text).
