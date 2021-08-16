=================
k-Space with Math
=================

If you don’t like math, turn away now. If, on the other hand, you aren’t frightened by integral signs, and remember a little about complex numbers, you may find this quantitative description satisfying. If you really want to fully understand how different types of imaging acquisitions work, there is no avoiding a trip through k-space. To explain k-space, we need to derive the MRI signal equation.

The signal from a given location has both a magnitude and phase, and can be written as

.. math::

  s = s_0 e^{i \theta}


Where s0 is the magnitude of the signal (which depends on the proton density, T1, T2, and various imaging parameters such as TE and TR), and theta is its phase. While the complex exponential appears, well, complex, it just represents the phase through Euler’s formula,

.. math::

  e^{i \theta} = cos \theta + i sin \theta


The magnitude of the signal is determined by the tissue properties (T1, T2, etc) and the scanner settings (TE, TR, etc). The phase is explicitly controlled by the magnetic field gradients that are applied.

As we have written previously, the magnetic field can be made a function of spatial location by passing currents through the magnetic field gradient coils. We’ll limit ourselves to two dimensions, but the following can easily be extended to three. This is the distinction between 2D and 3D acquisitions. In a 3D acquisition, slice selection is (mainly) replaced by phase encoding along the third dimension.


.. math::

   B(X,Y) = B_0 + G_X X + G_Y Y


Combining this with the Larmor equation, we get a resonant frequency

.. math::

   \omega (X, Y) = \gamma B(X,Y) = \gamma (B_0 + G_X X + G_Y Y)


Using a reference frequency of gamma B0, the relative frequency of a proton at a given location can be written as

.. math::

   \Delta \omega (X, Y) = \gamma (G_X X + G_Y Y)



The phase, theta, that is accumulated over time is just the integral of the angular frequency, omega, (angular velocity) with respect to time. This is the angular frequency (velocity) equivalent of saying that the distance we drive is the integral of our speed with respect to time. We now explicitly acknowledge that the magnetic field gradients Gx and Gy are varied as functions of time, t.


.. math::

  \theta (X,Y,t) = \int {\Delta \omega (X,Y,t)}{dt} = \int {\gamma (G_X (t) X + G_Y (t) Y)}{dt}


Noting that for a given proton, X, and Y are constant (this is usually assumed to be the case, but we can exploit variations to measure velocity and random motion in phase-contrast and diffusion imaging respectively), we make the following definitions. There’s no physics here, these are just arbitrary (but useful) substitutions. As we’ll see shortly, these equations will define our location in ‘k-space’.

.. math::

  k_X = \gamma \int {G_X (t) X}{dt}

.. math::

  k_X = \gamma \int {G_Y (t) Y}{dt}


At a given location (X, Y) and time t, the phase can now be written as a function of kX, kY, X, and Y

.. math::

  \theta(k_X, k_Y, X, Y) = k_X X + k_Y Y


Finally, we can use this phase to write the signal equation as

.. math::

  s(k_X, k_Y, X, Y) = s_0 (X,Y) e^{i(k_X X + k_Y Y)}


This represents the signal from a single point in space. The total signal is just the integration over all space.

.. math::

  S( k_X, k_Y ) = \int{ \int{s_0 (X,Y) e^{i(k_X X + k_Y Y)} }{dX}}{dY}


Phew, that’s it. This is the signal equation for imaging in MRI. Now we just need to understand what it means and how we can use it to generate at reconstruct images.

Mathematicians seeing the above equation may recognize it as the 2D inverse Fourier transform. The signal that we measure at a given value of kX, kY is just the inverse Fourier transform of the object in (image) space. More interesting is that mathematicians figured out the opposite transformation a very long time ago, and so if we can sample the signal as a function of kX, kY, the object in X, Y is just the (forward) Fourier transform.

While the equation above allows us to go from image-space to ‘k-space’, we can also go in the opposite direction, to form an image, given that we have sampled this mysterious k-space.


.. math::

  S(X, Y) = \frac{1}{2 \pi} \int{\int{S_0 (k_X, k_Y) e^{-i (k_X X + k_Y Y)} }} dk_X dk_Y


In reality, we sample k-space at discrete locations, so that instead of integrating over a continuous function, reconstruction becomes the discrete Fourier transform. Essentially, the integration becomes a summation.

.. math::

  S(X, Y) = \frac{1}{2 \pi} \sum_{k_X}{\sum_{k_Y}{S_0 (k_X, k_Y) e^{-i (k_X X + k_Y Y)} }}


