## What?
This is a data analysis program with which you can take a sound of a container filled with multiple objects, and ideally it gives you the number of that object that is in the container. Currently, it doesn't work -until now I had very little training data, and it was so noisy it was practically useless-, but I am working on this project in my spare time and intend to get good results out of it soon.

Other than the actual software, I have a setup to slowly rotate a matchbox with a set number of matches/ other objects so that I can collect hours of data without being there. I haven't yet trained on this dataset, and my old data was literally 5 minutes of me just shaking the box. Now that I have this little device I'm sure I'll get enough good data to actually get correct predictions.

You might notice the program doesn't have a license, and that's because I'm a bit scared of messing that part up, if anyone would like to use this software we can talk about it!
## Why?
I thought it would be an interesting way to learn more complex types of neural networks (kind of a big project for a first, but i think taking on a challenge is the best way to learn), also problem 1 of IYPT seemed pretty fun (I was a participant). I also think it could have a lot of interesting applications, imagine if you had some container with grains (maybe even a liquid) in it, and you wanted an estimate of how full it was without even peeking at the inside, this could be a very useful sensor for the agricultural industry (which is very large here in Brazil) and I'm sure more creative people could find even better uses for this kind of sensor.
## How?
Currently, the program works in a few steps: 

 1. It takes all of the data and labels it. Then it splits it
    into a lot of randomly sized slices of audio that are longer than 10
    seconds, basically allowing me to "generate" an infinite amount of
    valid and labeled training data from one very large audio. One
    problem I'm running into is that I was doing something really stupid
    and doing everything on RAM, so changing everything to write and
    load straight to and from disk is being really hard. Since
    everything was on RAM, obviously my neural network was awful, cause
    it was limited to very little low quality data.
 2. Secondly, it takes all those little slices and does FFTs on all of
    them, then finds every single peak on the spectra, resulting in an
    array with all the frequency peaks' amplitude and frequency for each
    audio.
 3. Then all of these arrays are used to train an RNN with cross
    validation so I don't have to spend double the time making a
    validation dataset (Maybe I could just cut the original audio
    randomly again, but I don't think I'll implement that now).
 4. Now I theoretically have a fully trained neural network that can
    find out the number of matches in a matchbox, then I just have to
    run my machine with an unknown number of matches, do some
    pre-processing and it's ready for the RNN to guess!

## Stuff I've yet to do (with some stuff I've done)
 - [x] Extract some data
 - [x] Cut that data into a more sizeable amount
 - [x] Do the Fourier analysis of all of them
 - [x] Find the frequency peaks and their amplitudes
 - [x] Pad and generally prepare the data for the RNN
 - [ ] Do all of the operations directly to and from disk space, making only temporary arrays 
 - [x] Actually feed the data into the RNN
 - [x] Make a device for extracting data
 - [ ] Train it with the better data
 - [ ] Use better training parameters
 - [ ] Train it on a GPU
 - [ ] Try it with objects other than matchsticks (balls, grains and liquids)


