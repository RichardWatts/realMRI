=================================
The Hitchhiker's Guide to k-Space
=================================

*(with apologies to Douglas Adams)*

k-space is the key to understanding the difference between different types of acquisition. If you want to understand such things as conventional gradient and spin echoes, echo-planar imaging (EPI) or fast (turbo) spin echoes, not to mention radial sampling and spirals, you need to know a little about about k-space.

If you skipped the last section, or glanced at the math and turned away in horror, don’t worry. You don’t have to understand all that stuff to find your way around in k-space and the different types of acquisitions. (Almost) All MRI measurements are made in k-space. Here is a summary of the rules of the road for k-space.

  For 2D sequences we acquire data to fill a two-dimensional grid of k-space for each slice

  Once we’ve filled this grid, our k-space data can be converted to an image using a 2D Fourier transform. This is just a mathematical transformation

  We can ride around (sample) k-space by changing the magnetic field gradients. We always start off in the middle of k-space, where all the protons are in phase (ignoring T2 and T2* effects)

  The magnetic field gradient direction and strength determine the direction and speed (the velocity) with which we traverse k-space

  A 180 degree RF pulse magically teleports us to the opposite location in k-space
