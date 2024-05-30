# IDEA9103_Final_Xingyue_Wan
## Inspiration
In [week 10 tutorial](https://canvas.sydney.edu.au/courses/56592/pages/week-10-tutorial-2?module_item_id=2309124) we learnt to create a jumping long bar like effect using Perlin noise. I chose to add audio to the group code - [Summer (from 'Kikujiro')](https://music.youtube.com/playlist?list=OLAK5uy_nsUhfGr157YzQhmdZbjE8FFHH5AgrhYnI) to use the frequency of the music and animate the jumps based on the group base code. The expected code rendering is similar to the base code where the squares jump to the frequency of the music.
## Animation Methods
Firstly I added audio to the group code and loaded the audio file and created an FFT to analyse the frequency of the audio. Then I added a button to start or pause the music. Finally I implemented the effect of using the dynamics of the audio spectrum to adjust the height of the image segments to achieve a throbbing animation.
## Code Analysis
I modified the visuals based on the group code to achieve a bouncing animation through the audio of the music.
- Firstly I added audio loading and FFT object declaration
```
let audio;
let fft;
let isPlaying = false;
```
- Add the audio of my choice to the function Audio preloaded into the function.
```
function preload() {
  audio = loadSound('asset/summer.mp3'); 
}

```
- I added the initialisation of the FFT object and the connection to the audio.
```
fft = new p5.FFT();
audio.connect(fft);
```
- I created a button named ‘Play Audio’ using the createButton() function and set its position to (20, 20). I used the mousePressed() function to associate the toggleAudio() function with the button's click event as a toggle for the audio playback state.
```
let button = createButton('Play Audio');
button.position(20, 20);
button.mousePressed(toggleAudio);
```
- I added the `toggleAudio()` function to toggle the play state of the audio when the user clicks the play/pause button.
```
function toggleAudio() {
  if (audio.isPlaying()) {
    audio.pause();
    isPlaying = false;
  } else {
    audio.play();
    isPlaying = true;
  }
}
```
- Finally, I added animateSegments() to animate the squares to the rhythm of the music. More the rhythm and volume of the music changes, the squares in the base code dynamically adjust the height of each block.
```
  function animateSegments(spectrum) {
  let segmentIndex = 0;
  for (let y = 0; y < numSegments; y++) {
    for (let x = 0; x < numSegments; x++) {
      let segment = segments[segmentIndex];
      let segmentSize = map(spectrum[segmentIndex], 0, 255, 10,50);
      segment.drawHeight = segmentSize;
      segmentIndex++;
    }
  }
}
```
##Final Outcome
<img width="887" alt="final effect" src="https://github.com/xwan0374/IDEA9103_Final_Xingyue_Wan/assets/168156727/28dc4678-0607-4a00-9d92-a027594f9790">


