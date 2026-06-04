# I Just Wanted to Play Tetris

04/06/2026

---

I watched the Tetris movie a few months ago and as soon as the credits rolled, I started playing the game obsessively. Pretty soon, as would be expected, the grid was burned into my retinas. I couldn’t stop seeing falling blocks when I closed my eyes. Naturally, the only reasonable solution was to start taking the game apart. This decision triggered a chain reaction that ended several months later in combinatorial geometry.

<p align="center">
<img src="https://upload.wikimedia.org/wikipedia/commons/9/9c/Typical_Tetris_Game.svg" width="300"></p>

### The Hardware Illusion

I decided the only way to purge the game from my head was to engineer it from scratch. I opened Tinkercad and mapped a simplified version of the logic onto an 8x8 LED matrix.

Mechanically, an LED matrix is a fascinating puzzle. You cannot just command all the necessary lights to turn on simultaneously. You have to rely on multiplexing. The system activates one row of lights, sets the correct pattern for the falling shape and the locked blocks, turns them off, and immediately snaps to the next row. It scans through the grid so incredibly fast that the human eye is tricked into seeing a solid, continuous picture. Getting the system running on real hardware was deeply satisfying. Unfortunately, my brain interpreted this as encouragement.

<p align="center">
<img src="https://github.com/pragyaangaur/Electronics/blob/main/Assets/Tetris.jpeg" width="350"></p>

### Breaking the Rules of the Grid

Once the hardware was stable, I started questioning the shapes themselves. Classic Tetris runs on "tetrominoes" which are shapes constructed of exactly four squares that are strictly connected by flat edges. I started wondering why the game relied entirely on edge adjacency. Why are they never allowed to connect just at the corners?

This is the mathematical difference between a *polyomino* (edge-connected) and a *polyplet* (edge or vertex-connected). I suspected that allowing corner connections would make the game significantly stranger, which is usually a good sign.

I spent the next month building a web-based puzzle game designed around these pseudo-triominos. I called it TriKing. I built a dynamic difficulty curve, tracked combo chains, and coded an algorithm to detect complex rotational maneuvers. I compiled the whole thing, wrote an input handler for touch and keyboard, launched it on itch.io, and watched it get played over 200 times.

<p align="center">
<img src="https://github.com/pragyaangaur/TriKing/blob/main/Assets/TriKing1.jpeg" width="300"></p>

### The Hyperbolic Boundary

My brain, however, was not going to stop at playing games. It wanted to know how deep the rabbit hole went. I started wondering about the total combinatorial space of these shapes. If I have a set number of squares, exactly how many unique polyplets can exist in the universe?

I fell straight into the On-Line Encyclopedia of Integer Sequences (OEIS) - the battleground for math nerds. I quickly realized that counting standard shapes on a normal, flat Euclidean grid is heavily researched and nothing I could do on my humble laptop could beat the polyplet enumeration sequences that ran up to the billions. I needed to find a frontier that hadn’t already been conquered by people with supercomputers and more free time than me.

So, I abandoned flat space entirely and looked at non-Euclidean hyperbolic geometry.

This is basically a grid that curves away from you exponentially. I focused on a specific geometric structure called the {4,5} tessellation of the hyperbolic plane. In this space, every square has 4 edge-neighbors and 8 vertex-neighbors. The OEIS sequence tracking the number of unique shapes in this exact space was A390200.

<p align="center">
<img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSqGp9XAdQ70cLsk_gAtmIcO-2oceoV3Uk5Ow&s" width="200"></p>

I pulled the sequence and noticed it stopped at 7 squares, where the count reached 98,353 unique shapes. The next value simply wasn’t there. As far as I could tell, nobody had computed it yet. I possessed exactly two relevant qualifications: a laptop and an unhealthy amount of stubbornness.

### The Final Computation

I spent weeks understanding the domain and building the model. Standard floating-point arithmetic was useless here because rounding errors would eventually corrupt the count. I had to build an exact algebraic engine to keep the math perfectly pure. 

To make sure my result was accurate, I developed two mathematically different programs that counted the shapes in completely different ways. If the logic was correct, both programs had to eventually corroborate each other. 

When I finally ran the scripts, both independent engines mathematically converged on the exact same integer.

[For an 8-square polyplet in a hyperbolic {4,5} tessellation, there are exactly **1,261,889** unique shapes.](https://oeis.org/A390200)

I packaged my computational statistics and methodologies, and submitted the disclosure to the mathematicians at OEIS. On June 3, 2026, my calculation was officially verified, approved, and appended to the permanent sequence. 

This is the part that worries me. You watch a movie about a retro video game. You build a tiny hardware version because it seems fun. Then you design your own puzzle game. Then you start reading papers about combinatorics. And some time later, you are computing undiscovered integers in a hyperbolic universe and joining the math nerds online.

---
> *Disclaimer: The enumeration has been reviewed and approved under OEIS A390200. I am currently drafting a paper detailing the methodology used by me to reach the result.*
