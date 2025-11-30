Total Time: 8.8Hrs<br>
11/29/2025 to 11/30/2025<br>

# Finished PCB Layout
Here is what I came up with, I mainly just placed things randomly until I got it to a good size. Its quite a small board at only 60x40mm. Itll be sure to fit in the enclosure I plan on using, which is a very small cigar box. I will mount the PCB using 3 M3 screws and nuts. The potentiometers, switches, and jacks will be panel mounted, too.
Here is the final PCB layout:
![Screenshot 2025-11-30 004540](https://blueprint.hackclub.com/user-attachments/blobs/proxy/eyJfcmFpbHMiOnsiZGF0YSI6MTYyMDgsInB1ciI6ImJsb2JfaWQifX0=--1fee78b1f711be13dd452285126ca7c7c81c4b28/Screenshot%202025-11-30%20004540.png)
And the 3D render:
![Screenshot 2025-11-30 004531](https://blueprint.hackclub.com/user-attachments/blobs/proxy/eyJfcmFpbHMiOnsiZGF0YSI6MTYyMDksInB1ciI6ImJsb2JfaWQifX0=--f55c8afd08bfc194e5b994e37cea3c6a10668eae/Screenshot%202025-11-30%20004531.png)
And my final schematic:
![Screenshot 2025-11-30 004708](https://blueprint.hackclub.com/user-attachments/blobs/proxy/eyJfcmFpbHMiOnsiZGF0YSI6MTYyMTAsInB1ciI6ImJsb2JfaWQifX0=--bd519451572a5fabf569259c2a0c6253387b75b4/Screenshot%202025-11-30%20004708.png)

# Component Selection and Footprints
This part always takes the longest. For the LM386, I used the standard DIP-8 package. For the caps, I always use TDK, Panasonic, or Nichicon. I chose the cheapest THT values and simply selected their footprints based off their datasheet or what Digikey told me. I look here:
![Screenshot 2025-11-29 222713](https://blueprint.hackclub.com/user-attachments/blobs/proxy/eyJfcmFpbHMiOnsiZGF0YSI6MTYxOTYsInB1ciI6ImJsb2JfaWQifX0=--4315f7bdbccc0c2ec5dde0b1d43723f930f5ee69/Screenshot%202025-11-29%20222713.png)
For the potentiometers, jacks, and switches, I will buy those off of amazon because it is much cheaper than Digikey for these generic parts, in my experience. They will be case mounted, so I need to simplify my schematic to reflect that these will be connectors: 
![image](https://blueprint.hackclub.com/user-attachments/blobs/proxy/eyJfcmFpbHMiOnsiZGF0YSI6MTYxOTcsInB1ciI6ImJsb2JfaWQifX0=--9d137677bd50a42b7f97b6ff2b48a4a74c22f8e0/image.png)
and all of my footprints:
![image](https://blueprint.hackclub.com/user-attachments/blobs/proxy/eyJfcmFpbHMiOnsiZGF0YSI6MTYxOTksInB1ciI6ImJsb2JfaWQifX0=--f0d40b1de44b906d51a38775fc755d0e22a62e73/image.png)
Now I will lay out the PCB.

# Designed Circuit
For my amp, I chose the LM386 because I've learned about them already and they seem to be ubiquitous in their use in low-power guitar amps. I chose the N-1 variant because it operates about my 9V voltage level ranging 5-12V. First, I made the 1/4" input stage which consists of a logarithmic 10k potentiometer going straight to the non-inverting input. The 10k was chosen to be logarithmic because this is to control the volume.
![Screenshot 2025-11-29 211049](https://blueprint.hackclub.com/user-attachments/blobs/proxy/eyJfcmFpbHMiOnsiZGF0YSI6MTYxMTAsInB1ciI6ImJsb2JfaWQifX0=--0aa5b4a435ec14cc34daeba9d07f948623932f76/Screenshot%202025-11-29%20211049.png)

Next, I need to design the gain control. This is simply a 10k log. pot in series with a 10uF capacitor and a SPST switch across pins 1 and 8 of the amp. The capacitor value was taken from the datasheet.
![Screenshot 2025-11-29 213351](https://blueprint.hackclub.com/user-attachments/blobs/proxy/eyJfcmFpbHMiOnsiZGF0YSI6MTYxMTIsInB1ciI6ImJsb2JfaWQifX0=--7f3b2b5c4c53e088deb69e6f489cc26e3360e826/Screenshot%202025-11-29%20213351.png)
This allows the amp to vary its gain from a ratio of 20 up to 200, which is cool! The switch is there to toggle between clean and dirty, naturally.

Next was bass control. By placing a capacitor between pins 5 and 1, high frequencies are attenuated since Xc is inversely proportional to f. As f increases, C shunts that high frequency, leaving more perceivable bass. The R is for shaping, i think.

Lastly was the 1000uF capacitor in series with the 8 Ohm speaker. This coupling capacitor charges up to effectively remove DC offset bias which could harm the speaker. It only allows AC through. The higher the value, the lower the frequencies will be able to pass through. For example, if f=100Hz, Xc=1/2pi(100Hz)(1000x10^-6)=1.6Ohms of resistance. The higher C, the lower Xc will be for a given f. By having our coupling cap at sucha high value, I hope I will get a nice bass throughput.
![image](https://blueprint.hackclub.com/user-attachments/blobs/proxy/eyJfcmFpbHMiOnsiZGF0YSI6MTYxMTgsInB1ciI6ImJsb2JfaWQifX0=--6e23a7d02dba5c72848e899280dd5bd106345509/image.png)
I have not placed any LEDs to let you know its on to save power.
