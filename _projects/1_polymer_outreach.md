---
layout: page
title: Polymer outreach
description: Showing students how polymer chains stretch, tangle, and snap, with simulations and hands-on experiments.
img: assets/img/outreach/card_light.gif
img_dark: assets/img/outreach/card_dark.gif
category: molecular dynamics
venue: Third Frontier outreach
importance: 3
_styles: >
  .clip { margin: 1.4rem 0 1.6rem; }
  .clip video { display: block; width: 100%; aspect-ratio: 16 / 9; border-radius: 6px; background: #ffffff; }
  html[data-theme="dark"] .clip video { background: #1c1c1d; }
  .clip figcaption { margin-top: 0.5rem; font-size: 0.9rem; color: var(--global-text-color-light); }
---

Akron, the [Rubber Capital of the World](https://en.wikipedia.org/wiki/Akron,_Ohio), sits at the heart of Ohio's Polymer Valley, and the [University of Akron](https://www.uakron.edu/)'s [School of Polymer Science and Polymer Engineering](https://www.uakron.edu/polymer/) is **ranked first in the United States** for polymer science by [EduRank](https://edurank.org/chemistry/polymers/us). As part of the School's Third Frontier outreach group, I help introduce students to polymers, using the same kind of simulations I run in my research alongside hands-on experiments.

## What is a polymer?

A polymer is a very long molecule made by linking many small units, called monomers, into a chain, like beads on a string. Plastics, rubber, and nylon are polymers, and so are the DNA and proteins in our bodies. Because the chains are so long, they coil up and tangle with each other like a bowl of cooked spaghetti, and this tangling gives polymers much of their strength and stretch.

## Longer chains hold together longer

<figure class="clip">
  <video data-light="{{ '/assets/video/outreach/chain_length_light.mp4' | relative_url }}" data-dark="{{ '/assets/video/outreach/chain_length_dark.mp4' | relative_url }}" data-poster-light="{{ '/assets/img/outreach/chain_length_light.jpg' | relative_url }}" data-poster-dark="{{ '/assets/img/outreach/chain_length_dark.jpg' | relative_url }}" muted loop playsinline controls preload="none" aria-label="Simulations of four pieces of polymer with 20, 50, 100, and 200-unit chains pulled at the same speed"></video>
  <figcaption>Four pieces of polymer pulled from both ends at the same speed. Each colour is one chain.</figcaption>
</figure>

Each strip is a computer simulation of a small piece of polymer melt, built from bead-and-spring chains, a soft material with no crosslinks between its chains, much like Silly Putty. All four are pulled at the same speed, and the only difference is the length of the chains, from 20 to 200 units. Short chains barely tangle, so they slide past each other and the sample tears apart early. Longer chains are more entangled: they have to slide and straighten out before the sample can come apart, so it draws out into long fibers first. The piece with 20-unit chains holds together only until it is about 4 times its starting length, while the piece with 200-unit chains lasts until about 11 times. This is one reason longer chains make tougher plastics.

## Pull slowly and it stretches, pull fast and it snaps

<figure class="clip">
  <video data-light="{{ '/assets/video/outreach/pulling_speed_light.mp4' | relative_url }}" data-dark="{{ '/assets/video/outreach/pulling_speed_dark.mp4' | relative_url }}" data-poster-light="{{ '/assets/img/outreach/pulling_speed_light.jpg' | relative_url }}" data-poster-dark="{{ '/assets/img/outreach/pulling_speed_dark.jpg' | relative_url }}" muted loop playsinline controls preload="none" aria-label="Simulations of a piece of polymer with 200-unit chains pulled slowly, five times faster, and ten times faster, with the two faster pulls shown at half speed"></video>
  <figcaption>The same 200-unit chains pulled at three speeds. The two faster pulls are shown at half speed so you can watch them snap: on screen they move 2.5 and 5 times faster than the slow one.</figcaption>
</figure>

All three pieces start together. Pulled five or ten times faster, the chains have no time to adapt: the sample narrows and snaps after stretching to only about 4 to 5 times its starting length, and some chains break, all while the slowly pulled piece has barely started to stretch. Pulled slowly, the chains have time to slide past each other and line up along the pulling direction, so the sample keeps stretching into a long fiber and holds together until about 11 times its starting length. You can feel the same thing with Silly Putty: pull it slowly and it stretches, yank it and it breaks.

## Polymer Explorers at the library

In June 2026, with the School's outreach team, I helped run Polymer Explorers, a hands-on workshop for high-school students at the [Akron-Summit County Public Library](https://www.akronlibrary.org/)'s Main Library. Students moved through four stations, including Stretch or Snap?, which paired the simulations above with Silly Putty, and my Slimy Worms station, where sodium alginate squeezed into a calcium chloride bath instantly forms rubbery hydrogel worms as calcium ions crosslink the chains.

<div class="row">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid loading="lazy" path="assets/img/outreach/workshop_station.jpg" title="Slimy Worms station" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid loading="lazy" path="assets/img/outreach/alginate_worm.jpg" title="An alginate hydrogel worm" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">The Slimy Worms station, and an alginate hydrogel worm made in a calcium chloride bath.</div>

{% include themed_videos.liquid %}
