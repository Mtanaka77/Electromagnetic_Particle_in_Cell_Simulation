## Largescale Electromagnetic Particle-in-Cell Simulation for High-Temperature Plasmas ## 

### Magnetic Reconnection and Solar-Magnetospheric Coupling ###

Why is a current sheet of the distant magnetotail of the earth to be thinned and why is a large energy to be released, which is typically observed as magnetic reconnection ? There were many theories for the reconnection including from classical Dungey's theory to nuclear-fusion oriented anomalous resistivity. It is noted that Dr. Speicer in the mean time paid attention to inertia resistivity of thinning the neutral sheet. Some time later in 1995 (Ref.3), a particle simulation was executed to show the reconnection mechanism of different inertia of ions and electrons resulting in large energy release of earth's magnetotail.

An electromagnetic particle simulation code is utilized for solar and magnetospheric space physics. Both electric and magnetic fields at low frequencies are solved by a slightly backward time decentering technique. Magnetic reconnection and the solar wind-earth magnetic field coupling are quite suitable for applying this simulation code.


### Implicit Decentered Particle Code and a Large Time Step ###

One utilizes the time decentered scheme in aimpl=0.6, while the time centered scheme in the explicit code (aimpl=0.5) is used in other directory of molecular dynamics simulations. It is noted, however, that finite errors in the divergence term accumulate which must be corrected if the finite difference coordinate space are utilized. Four physical units are, i) time: 1/wpe (c/wpe: electron inertia length), ii) length: c/wpe, iii) mass: electron mass, and iv) charge: electron charge. The program is written in Fortran 2003 and is coded for parallelization by MPI ver.3.

By the implicit scheme it is free from the Courant condition, that is, Dx(length)/Dt(time step) >< c, the speed of light. For the backward differential scheme in aimpl > 0.5, a time step may be dt~1.2/wpe in order to dump out plasma oscillations at plasma frequency omega_e= wpe - small noises. But, 2 \pi/(dt wce) >> 1 is necessary for electron tracking.

A large time step for ions, 2 \pi /(dt*wci) >> 1, is a good target of the drift-kinetic simulation of electrons. The time step is still bound by electron hopping, and typical time step may be dt= 10/wpe.

The title, major references, and remarks of this simulation code are written in the top of the @mrg37_013A.f03 file.
Important blocks of the code are explained as comments.
Two additional files are necessary, the paramer file param_A13A.h and the configure file rec_3d13A.


### Execution Scripts ###

Linux (PGI): Compilation by mpif90

 > mpich-4.0.2: ./configure --prefix=/opt/pgi/mpich-4.0.2 2>&1 | tee conf.txt

 > fftw3-3.3.10: ./configure --disable-shared --enable-maintainer-mode --enable-threads --prefix=/opt/pgi/fftw3

mpif90 @mrg37-013A.f03 needs the files param_A13A.h and rec_3d13A

 > $ mpif90 -mcmodel=medium -fast @mrg37-013A.f03 -I/opt/pgi/fftw3/include -L/opt/pgi/fftw3/lib -lfftw3

Execution by mpiexec (may need some tens of processors)

 > Execution: $ mpiexec -n 6 a.out &


### Simulation of Two Flux Bundles

One can enjoy simulations by changing system sizes and boundary conditions. For the present case, an equilibration of the pair of flux bundles is first tested in three dimensions. Fully kinetic ions and electrons are used in the igc=1 case, for example, in the rec_3d13A file. Then, let's start looking at a merging of two flux bundles. On the other case, the drift-kenetic electrons and kinetic ions are simulated at a large time step in the igc=2 case. But, one should note that heavy ions move kinetically while light electrons lose some of their particle freedom in the coordinate space.

In-house graphic subroutines are incorporated in "@mrg37-013A.f03" in order to check the current run in the simulation. Figure 1 in the "EMfield.pdf" PDF plot of the igc=1 case shows the electric and magnetic fields in the YZ (left) and X (right) components at the early and final times. Two flux bundles at t=5000/wpe are seen touched and sqeezed at the Y= Ly/2 plane. Reading papers of this implicit particle simulation code (Ref. 1-2) and applications to magnetospheric space plasmas (Ref. 3-5) are highly recommended.


### References: ###

1. M. Tanaka, A simulation of low-frequency electromagnetic phenomena in kinetic plasmas of three dimensions, J.Comput. Phys., 107, 124-145 (1993).

2. M. Tanaka, Macro-EM particle simulation method and a study of collisionless magnetic reconnection, Comput.Phys.Commun., 87, 117-138 (1995).

3. M. Tanaka, Macro-particle simulations of collisionless magnetic reconnection, Phys.Plasmas, 2, 2920-2930 (1995).

4. M. Tanaka, Asymmetry and thermal effects due to parallel motion of electrons in collisionless magnetic reconnection, Phys.Plasmas, 3, 4010-4017 (1996). 

5. H. Shimazu, M. Tanaka, and S. Machida, The behavior of heavy ions in collisionless parallel shocks generated by the solar wind and planetary plasma interactions, J.Geophys.Res., 101, 27565-27571 (1996).


