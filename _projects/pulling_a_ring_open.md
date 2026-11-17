---
layout: page
title: Pulling a molecular ring open
description: Quantum-chemistry simulations of a strained carbon ring torn open by force, and of what it does when the force lets go.
img: assets/img/gdfc/card_light.gif
img_dark: assets/img/gdfc/card_dark.gif
category: quantum chemistry
venue: Multireference ab initio dynamics
importance: 1
_styles: >
  .clip { margin: 1.6rem 0 1.8rem; }
  .clip video { display: block; width: 100%; aspect-ratio: 16 / 9; border-radius: 6px; background: #ffffff; }
  html[data-theme="dark"] .clip video { background: #1c1c1d; }
  .clip figcaption { margin-top: 0.5rem; font-size: 0.9rem; color: var(--global-text-color-light); }
  .clip figcaption strong { color: var(--global-text-color); font-weight: 500; }
  .story img { width: 100%; border-radius: 6px; }
  .refs li { margin-bottom: 0.4rem; }
---

Most chemical reactions are started with heat or light. Mechanochemistry uses force instead. When a long polymer chain is stretched hard, for example by the collapsing bubbles of ultrasound in a polymer solution, the pull concentrates on the bonds along its backbone, and a small, strained ring built into that backbone can be torn open.

The ring studied here is gem-difluorocyclopropane (gDFC): a triangle of three carbon atoms with two fluorine atoms on one corner. In 2010, Lenhardt and coworkers built these rings into polybutadiene and showed that pulling on the polymer opens them into a 1,3-diradical, a molecule with two unpaired electrons. Normally this structure is the transition state of the ring's isomerization and lasts for a single molecular vibration, but the pull holds it open: the transition state is trapped by tension [[1]](#ref-1). In 2015, Wang and coworkers asked what the ring does once the force is released [[2]](#ref-2). The simulations below follow both steps atom by atom, with the electrons treated by quantum mechanics.

<figure class="story">
  <img class="only-light" data-zoomable src="{{ '/assets/img/gdfc/story_light.jpg' | relative_url }}" alt="A gem-difluorocyclopropane ring is pulled open into a diradical. When the force is released, it almost always closes with both handles on the same side, and rarely with them on opposite sides">
  <img class="only-dark" data-zoomable src="{{ '/assets/img/gdfc/story_dark.jpg' | relative_url }}" alt="A gem-difluorocyclopropane ring is pulled open into a diradical. When the force is released, it almost always closes with both handles on the same side, and rarely with them on opposite sides">
</figure>

## Why the fluorines matter

A three-membered ring is already strained: its bond angles are squeezed to 60°, far from the roughly 109° that carbon prefers. Two fluorine atoms on one corner add more strain and weaken the carbon–carbon bond on the opposite side of the triangle [[1]](#ref-1). That bond, the one that breaks in the movies, gives way much more easily than a bond in plain cyclopropane, so a moderate pull opens the ring without tearing the rest of the molecule apart.

## How the movies are made

Breaking a bond leaves two electrons that no longer pair up, and standard density functional theory describes that poorly. The simulations therefore use a multireference method: CASSCF with second-order perturbation corrections (CASPT2), with two electrons in the two orbitals of the breaking bond and the 6-31G\* basis set, in OpenMolcas. In ab initio molecular dynamics, the atoms move by Newton's laws while the forces on them come from this quantum calculation, repeated every 0.25 to 0.5 femtoseconds. Each run starts from positions and velocities sampled from the molecule's quantum vibrational (Wigner) distribution at 280 K. The polymer chain on either side of the ring is replaced by a constant pulling force on the two hydrogens where the chain would attach, drawn in orange in the movies. For the ring-closing runs, the force is switched off.

In each movie:

- **Left chart:** the length of the breaking bond. An intact carbon–carbon bond is about 1.5 Å long.
- **Right chart:** how that bond's two electrons are shared between its bonding and antibonding orbitals. An intact bond keeps both in the bonding orbital (about 2 and 0). As the bond breaks, the electrons split up, one in each orbital (about 1 and 1): the diradical.
- **The stick for the breaking bond** is drawn from those same numbers, so it thins and disappears as the bond breaks and grows back as it forms. A dashed line keeps showing the distance once the bond is gone.
- **Time:** one second of video is 30 femtoseconds (3 × 10⁻¹⁴ s) of the simulation.

## Pulling the ring open

<figure class="clip">
  <video data-light="{{ '/assets/video/gdfc/open_cis_light.mp4' | relative_url }}" data-dark="{{ '/assets/video/gdfc/open_cis_dark.mp4' | relative_url }}" data-poster-light="{{ '/assets/img/gdfc/open_cis_light.jpg' | relative_url }}" data-poster-dark="{{ '/assets/img/gdfc/open_cis_dark.jpg' | relative_url }}" muted loop playsinline controls preload="none" aria-label="Ab initio dynamics of gem-difluorocyclopropane pulled at 2 nN on two hydrogens on the same side of the ring: the bond breaks and its two ends twist in opposite directions"></video>
  <figcaption><strong>Handles on the same side of the ring, 2 nN each.</strong> The two ends of the breaking bond twist in opposite directions as the ring opens.</figcaption>
</figure>

When the two orange hydrogens sit on the same side of the ring (cis), pulling them apart makes the two ends of the breaking bond, each a carbon carrying two hydrogens, twist in opposite directions, one clockwise and one counterclockwise (a disrotatory opening). That is the path the orbital-symmetry (Woodward–Hoffmann) rules allow when this ring is simply heated, and it is the path these simulations always take.

<figure class="clip">
  <video data-light="{{ '/assets/video/gdfc/open_trans_light.mp4' | relative_url }}" data-dark="{{ '/assets/video/gdfc/open_trans_dark.mp4' | relative_url }}" data-poster-light="{{ '/assets/img/gdfc/open_trans_light.jpg' | relative_url }}" data-poster-dark="{{ '/assets/img/gdfc/open_trans_dark.jpg' | relative_url }}" muted loop playsinline controls preload="none" aria-label="Ab initio dynamics of gem-difluorocyclopropane pulled at 3 nN on two hydrogens on opposite sides of the ring: both ends of the breaking bond twist the same way"></video>
  <figcaption><strong>Handles on opposite sides, 3 nN each.</strong> Both ends of the breaking bond twist the same way as the ring opens.</figcaption>
</figure>

When the orange hydrogens sit on opposite sides (trans), the pull twists both ends the same way, like two wheels turning together (a conrotatory opening), a motion the same rules disfavor for a heated ring. The force overrides that preference, though it takes a harder pull: 3 nN here instead of 2 nN. With the force on, the open diradical stays open: the pull has turned a fleeting transition state into a stable structure.

## Letting go

In the experiment the force lasts only as long as a bubble collapse. Once it is gone, the diradical is a transition state again, and the ring snaps shut, usually within about 100 femtoseconds.

<figure class="clip">
  <video data-light="{{ '/assets/video/gdfc/close_dis_light.mp4' | relative_url }}" data-dark="{{ '/assets/video/gdfc/close_dis_dark.mp4' | relative_url }}" data-poster-light="{{ '/assets/img/gdfc/close_dis_light.jpg' | relative_url }}" data-poster-dark="{{ '/assets/img/gdfc/close_dis_dark.jpg' | relative_url }}" muted loop playsinline controls preload="none" aria-label="Ab initio dynamics after the force is released: the two ends twist in opposite directions as the ring closes, and both orange hydrogens end up on the same side"></video>
  <figcaption><strong>Force released: the usual closing.</strong> The two ends twist in opposite directions and both handles end up on the same side.</figcaption>
</figure>

By far the more likely outcome is that the two ends twist in opposite directions as the ring closes (disrotatory), leaving both handles on the same side: the cis ring. That is why pulling on a polymer full of trans rings converts many of them into the less stable cis form, and why the polymer ends up slightly shorter after it has been stretched [[1]](#ref-1).

<figure class="clip">
  <video data-light="{{ '/assets/video/gdfc/close_con_light.mp4' | relative_url }}" data-dark="{{ '/assets/video/gdfc/close_con_dark.mp4' | relative_url }}" data-poster-light="{{ '/assets/img/gdfc/close_con_light.jpg' | relative_url }}" data-poster-dark="{{ '/assets/img/gdfc/close_con_dark.jpg' | relative_url }}" muted loop playsinline controls preload="none" aria-label="Ab initio dynamics after the force is released: the diradical lingers, then both ends twist the same way as the ring closes, leaving the orange hydrogens on opposite sides"></video>
  <figcaption><strong>Force released: the rare closing.</strong> Both ends twist the same way and the handles end up on opposite sides.</figcaption>
</figure>

Much less often, both ends twist the same way and the ring closes conrotatory, giving the trans ring. In this run the diradical lingers for about 200 femtoseconds before it finds that exit.

<figure class="clip">
  <video data-light="{{ '/assets/video/gdfc/close_reopen_light.mp4' | relative_url }}" data-dark="{{ '/assets/video/gdfc/close_reopen_dark.mp4' | relative_url }}" data-poster-light="{{ '/assets/img/gdfc/close_reopen_light.jpg' | relative_url }}" data-poster-dark="{{ '/assets/img/gdfc/close_reopen_dark.jpg' | relative_url }}" muted loop playsinline controls preload="none" aria-label="Ab initio dynamics after the force is released: the ring closes, opens again, and closes a second time with the orange hydrogens on opposite sides"></video>
  <figcaption><strong>A ring that changes its mind.</strong> It closes with the handles on the same side, breaks open again, then closes the other way.</figcaption>
</figure>

The energy released as the ring closes stays in the molecule as vibration, because nothing in these simulations carries it away. In this run the ring closes with both handles on the same side, breaks open again about 140 femtoseconds later, and then closes the other way, with the handles on opposite sides. In a polymer in solution, the chain and the solvent would carry some of that energy away.

## Why it matters

Transition states decide how fast a reaction runs and which products it makes, but they normally last about 10⁻¹³ s, far too short to study directly. Tension trapping holds one in place, and these simulations show, femtosecond by femtosecond, how a held transition state falls apart once it is let go.

## References

<ol class="refs">
  <li id="ref-1">J. M. Lenhardt, M. T. Ong, R. Choe, C. R. Evenhuis, T. J. Martinez, S. L. Craig. Trapping a diradical transition state by mechanochemical polymer extension. <em>Science</em> <strong>329</strong>, 1057–1060 (2010). <a href="https://doi.org/10.1126/science.1193412" target="_blank" rel="noopener">doi:10.1126/science.1193412</a></li>
  <li id="ref-2">J. Wang, M. T. Ong, T. B. Kouznetsova, J. M. Lenhardt, T. J. Martínez, S. L. Craig. Catch and release: orbital symmetry guided reaction dynamics from a freed "tension trapped transition state". <em>J. Org. Chem.</em> <strong>80</strong>, 11773–11778 (2015). <a href="https://doi.org/10.1021/acs.joc.5b01493" target="_blank" rel="noopener">doi:10.1021/acs.joc.5b01493</a></li>
</ol>

{% include themed_videos.liquid %}
