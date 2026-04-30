TryHackMe: Missing Person (Writeup)  


This room is about tracking a person's trip to Indonesia using just two photos: MotoGP.jpg and food.jpg. Here is how I solved it:


Part 1: The Race Track

First, I looked at MotoGP.jpg. I saw a big "PERTAMINA" sign.

Circuit Name: By searching for Pertamina MotoGP tracks, I found it's the Pertamina Mandalika International Street Circuit.

Event Date: Since the prompt mentions 2025, I checked the 2025 MotoGP schedule for Indonesia. The race is from 03-05/10/2025.


Part 2: The Dinner

Then I checked food.jpg.

Restaurant Name: Inside the photo, on the napkins/menus, the name Cantina Mexicana is visible.

Photo Time: I used an online EXIF viewer to check the image metadata. The "Date/Time Original" was 19:55:30.


Part 3: The After Party & The Cave

The user mentioned an after-party and a local DJ.

Bar Address: I searched for "MotoGP Mandalika after party." This led me to Surfers Bar in Kuta, Lombok. 
The full address is: Jl. Raya Kuta, Kuta, Kec. Pujut, Kabupaten Lombok Tengah, Nusa Tenggara Bar.

DJ Name: Checking the bar's social media or event tags, I found the DJ’s name is Bong Leleh.

The Cave: I looked up Bong Leleh’s Instagram/Facebook. He promotes a local tour to a cave called Gua Sumur.

Phone Number: I found his business contact on the Gua Sumur Facebook page. The number is 085333137345.


What I Learned from this Challenge:

Image Metadata is Key: I learned how to use EXIF data to find the exact time and date a photo was taken, which is a powerful tool in digital forensics.

Contextual Clues: Even a small logo (like Pertamina) or a restaurant name on a napkin can reveal a person's exact location.

Social Media Investigation: By finding one person (the DJ), I could trace their business and other locations (the cave) through their social media footprint.

Connecting the Dots: OSINT is not just about one fact; it's about combining metadata, Google searches, and social media to build a complete story.
