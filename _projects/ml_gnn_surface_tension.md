---
layout: page
title: Graph neural networks for surface tension
description: Why surface tension matters, why it is hard to measure, and how a graph neural network that also learns from liquids predicts it for polymers.
description_html: 'Why surface tension matters, why it is hard to measure, and how a graph neural network that also learns from liquids predicts it for polymers. Try it in the <a href="/predictor/">surface tension predictor</a>.'
img: assets/img/gnn_st/card_light.gif
img_dark: assets/img/gnn_st/card_dark.gif
category: machine learning
importance: 2
---

{% include gnn_st/styles.html %}

<figure class="gst-hero">
  <img src="{{ '/assets/img/gnn_st/hero_dew.jpg' | relative_url }}" alt="Water drops sitting as round, glassy beads on a green blade of grass">
  <figcaption>Water's surface tension, together with the waxy grass blade it sits on, pulls these drops into round beads. Photo: <a href="https://commons.wikimedia.org/wiki/File:Dew_on_grass_Luc_Viatour.jpg" target="_blank" rel="noopener">Luc Viatour</a> (<a href="https://lucnix.be" target="_blank" rel="noopener">lucnix.be</a>), <a href="https://creativecommons.org/licenses/by-sa/2.5/" target="_blank" rel="noopener">CC BY-SA 2.5</a>, via Wikimedia Commons, cropped.</figcaption>
</figure>

Every liquid has a surface tension, and every solid has a closely related surface energy. Together with the surface it touches, it decides whether water beads up or spreads out, whether a paint sticks, and whether a coating stays clean. In this project I ask a simple question: can we predict the surface tension of a polymer from its chemical structure alone, before anyone makes it?

## What surface tension is

A molecule inside a material is pulled equally from every side by its neighbors. A molecule at the surface has no neighbors above it, so it is pulled inward. Making more surface therefore costs energy, and that cost for each bit of new surface is the surface tension.

<figure class="gst-fig">
{% include gnn_st/surface.svg %}
  <figcaption>Inside, each molecule is pulled equally in every direction. At the surface, the neighbors above are missing, so the molecule is pulled inward (red arrow).</figcaption>
</figure>

Molecules that hold on to each other strongly, like water, give a high surface tension. Molecules that barely stick, like those in Teflon, give a low one.

## Why it matters

Surface tension shapes how paints, coatings, and glues work, how easily a non-stick pan releases food, and even how the body responds to a medical implant. Non-stick and water-repellent coatings need a low surface tension, while surfaces that must be painted or glued need a high one.

The lowest values come from polymers with fluorine-rich side chains, relatives of Teflon, but many fluorinated chemicals stay in the environment for a very long time. Chemists are looking for fluorine-free alternatives, and a model that predicts surface tension from structure helps them pick promising candidates before making them.

<figure class="gst-fig">
  <div class="gst-legend"><span><i class="gst-key dot k-poly"></i>polymers</span><span><i class="gst-key dot k-liq"></i>liquids</span></div>
{% include gnn_st/scale_wide.svg %}
{% include gnn_st/scale_narrow.svg %}
  <figcaption>Familiar materials on one surface tension scale, in millinewtons per meter (mN/m). The shaded shapes show the roughly 300 polymers and 600 liquids our models learned from.</figcaption>
</figure>

## Why it is hard to measure

For a liquid like water, measuring surface tension is routine. Polymers are much harder. Most are solid or extremely thick at room temperature, so they are often measured hot and the values corrected afterward, and the result depends on how clean the surface is. Carefully checked values exist for only a few hundred polymers. Computer simulations can help, but a single polymer can take days to weeks of computer time.

## Our first model

In our first study [[1]](#ref-1), we gathered the measured surface tension of about 300 polymers from the PoLyInfo database [[3]](#ref-3) and trained several machine learning models on them. Simpler models work from features calculated beforehand, such as how many fluorine atoms a polymer has. A graph neural network (GNN) learns straight from the atoms and bonds of the polymer's repeat unit. The GNN was the most accurate.

## Does the model get the trend right?

A good model should also get trends right. For simple hydrocarbon polymers such as polyethylene and polypropylene, we know that the surface tension drops as the side chain gets longer and then levels off, because it cannot keep dropping forever. What we did not know was how quickly it levels off, since experiments only go up to two carbons in the side chain. So we first ran molecular dynamics simulations, building a thin film of each polymer atom by atom on the computer.

<figure class="gst-fig gst-stepper" data-gap="2000">
  <div class="gst-steps" role="group" aria-label="Steps of the trend figure">
    <button type="button" class="gst-step" aria-pressed="false"><span>1</span> Measurements</button>
    <button type="button" class="gst-step" aria-pressed="false"><span>2</span> Simulations</button>
    <button type="button" class="gst-play" hidden>Play again</button>
  </div>
  <div class="gst-legend"><span><i class="gst-key dia"></i>measured</span><span><i class="gst-key line k-md"></i>MD simulation</span></div>
{% include gnn_st/trend_md_wide.svg %}
{% include gnn_st/trend_md_narrow.svg %}
  <figcaption>Surface tension of six hydrocarbon polymers as the side chain grows, from polyethylene to poly(1-heptene). The sketches show each repeat unit.</figcaption>
</figure>

The simulations show that the surface tension levels off fairly quickly, after about three carbons in the side chain. Their values sit a few mN/m away from the three measurements, but they capture the shape of the trend.

We then asked the models from our first study to predict the same six polymers, added one at a time below. Only the GNN followed the trend. The linear model keeps falling, and the random forest wanders with no clear direction.

<figure class="gst-fig gst-stepper" data-gap="2200">
  <div class="gst-steps" role="group" aria-label="Models added one at a time">
    <button type="button" class="gst-step" aria-pressed="false"><span>1</span> Linear regression</button>
    <button type="button" class="gst-step" aria-pressed="false"><span>2</span> Random forest</button>
    <button type="button" class="gst-step" aria-pressed="false"><span>3</span> GNN</button>
    <button type="button" class="gst-play" hidden>Play again</button>
  </div>
  <div class="gst-legend"><span><i class="gst-key dia"></i>measured</span><span><i class="gst-key line k-md"></i>MD simulation</span><span><i class="gst-key ring-muted"></i>linear regression</span><span><i class="gst-key sq"></i>random forest</span><span><i class="gst-key dot k-poly"></i>GNN</span></div>
{% include gnn_st/trend_models_wide.svg %}
{% include gnn_st/trend_models_narrow.svg %}
  <figcaption>Predictions of the models from our first study for the same six polymers, shown against the measurements and the simulations.</figcaption>
</figure>

## The idea: learn from liquids too

About 300 polymers is not much data for machine learning. Liquids are much easier to measure, their surface tension comes from the same forces, and they are built from the same small pieces. Polyethylene glycol and ethanol, for example, are both built from a carbon, carbon, oxygen chain, although in ethanol the oxygen also carries a hydrogen. So in our new work [[2]](#ref-2), we added about 600 liquids and trained our models on polymers and liquids together.

<div class="gst-stats">
  <div class="gst-stat"><b>~300</b><span><i style="background: var(--g-poly)"></i>polymers with a measured surface tension</span></div>
  <div class="gst-stat"><b>~600</b><span><i style="background: var(--g-liq)"></i>small-molecule liquids</span></div>
  <div class="gst-stat"><b>Most</b><span>of the small building blocks in the polymers also appear in the liquids</span></div>
</div>

## The result: a much better polymer model

Learning from the liquids, together with a better way of drawing each polymer for the model (described below), made the new GNN clearly more accurate for polymers.

<figure class="gst-fig">
  <picture class="only-light">
    <source media="(max-width: 575.98px)" srcset="{{ '/assets/img/gnn_st/parity_narrow_light.png' | relative_url }}">
    <img src="{{ '/assets/img/gnn_st/parity_wide_light.png' | relative_url }}" alt="Predicted against measured surface tension for the polymers. The new model's points sit closer to the diagonal than those of the 2025 model" loading="lazy" style="width: 100%">
  </picture>
  <picture class="only-dark">
    <source media="(max-width: 575.98px)" srcset="{{ '/assets/img/gnn_st/parity_narrow_dark.png' | relative_url }}">
    <img src="{{ '/assets/img/gnn_st/parity_wide_dark.png' | relative_url }}" alt="Predicted against measured surface tension for the polymers. The new model's points sit closer to the diagonal than those of the 2025 model" loading="lazy" style="width: 100%">
  </picture>
  <figcaption>Predicted against measured surface tension. Each point is a polymer the model had not seen during training, and points on the line are perfect predictions.</figcaption>
</figure>

For polymers, only the GNN clearly gained from the liquids. The simpler models, given the same liquids, did not reliably improve.

<figure class="gst-fig">
  <div class="gst-legend"><span><i class="gst-key ring"></i>trained on one class alone</span><span><i class="gst-key dot k-both"></i>polymers and liquids together</span></div>
{% include gnn_st/methods_wide.svg %}
{% include gnn_st/methods_narrow.svg %}
  <figcaption>Average error of four kinds of model, trained on one class alone or on polymers and liquids together. Where a model barely changed, the open circle sits on top of the filled dot. For polymers, the filled GNN point also includes the better way of drawing each polymer.</figcaption>
</figure>

Why only the GNN? We think it is because it builds its picture of a molecule from small local pieces, and polymers and liquids share most of those pieces. The extra liquids may also simply keep the network from memorizing the small set of polymers. The simpler models see each molecule as one fixed list of numbers, and the liquids taught them little.

## What is a graph neural network?

A molecule can be seen as a graph: atoms are dots and bonds are lines between them. A graph neural network works directly on that network of atoms and bonds. Step through it below with the repeat unit of PET, the plastic in water bottles.

<div class="gst-gnn" id="gst-gnn" data-step="0">
  <div class="gst-steps" role="group" aria-label="Steps of a graph neural network">
    <button type="button" class="gst-step" aria-pressed="true"><span>1</span> Molecule to graph</button>
    <button type="button" class="gst-step" aria-pressed="false"><span>2</span> Passing messages</button>
    <button type="button" class="gst-step" aria-pressed="false"><span>3</span> A wider view</button>
    <button type="button" class="gst-step" aria-pressed="false"><span>4</span> One number</button>
    <button type="button" class="gst-play" hidden>Play all</button>
  </div>
{% include gnn_st/gnn_animation_wide.svg %}
{% include gnn_st/gnn_animation_narrow.svg %}
  <p class="gst-step-text"><strong>Molecule to graph.</strong> Atoms become nodes and bonds become edges. The two star nodes (*) mark the polymerization sites, where the chain continues.</p>
  <p class="gst-step-text" hidden><strong>Passing messages.</strong> In each round, every atom shares what it knows with the atoms it is bonded to.</p>
  <p class="gst-step-text" hidden><strong>A wider view.</strong> After three rounds, each atom knows its surroundings three bonds out, not just its own element.</p>
  <p class="gst-step-text" hidden><strong>One number.</strong> The atoms are combined into one summary of the whole molecule, and a small neural network turns it into the surface tension.</p>
</div>

The network learns all of this on its own, by comparing its predictions with measured values.

## How polymers and liquids go in

A liquid goes in as its whole molecule. A polymer is a very long chain, so the model gets just one repeat unit. In the text format we use, an asterisk (*) marks each polymerization site, the point where the unit links to the next one, and the model keeps the two asterisks as extra nodes in its graph. This gave the lowest error of the options we tried, and it also tells the model whether it is looking at a polymer or a liquid.

<div class="gst-inputs">
  <div class="gst-incard">
    <h3>A polymer: polyethylene glycol</h3>
{% include gnn_st/input_polymer.svg %}
    <p>The repeat unit in brackets, repeated n times along the chain. For the model it is written as <code>*CCO*</code>, and each * becomes an extra node at a polymerization site.</p>
  </div>
  <div class="gst-incard">
    <h3>A liquid: ethanol</h3>
{% include gnn_st/input_liquid.svg %}
    <p>The whole molecule, written as <code>CCO</code>.</p>
  </div>
</div>

## Try the predictor

Both models are online. Type a polymer repeat unit, with a * at each polymerization site, or a liquid, and get its surface tension in a few seconds. Try `*CCO*` for polyethylene glycol or `CCO` for ethanol.

<a class="gst-cta" href="{{ '/predictor/' | relative_url }}">Open the predictor</a>

It predicts room-temperature values for single-type polymers (homopolymers) and pure liquids. For unusual structures, treat the result as a rough estimate.

## Papers

<ol class="refs">
  <li id="ref-1">J. Tamnanloo et al. Graph neural networks for surface tension prediction of polymers: a comparative analysis with descriptor-based models. <em>Macromolecules</em> <strong>58</strong>, 3764–3773 (2025). <a href="https://doi.org/10.1021/acs.macromol.4c03265" target="_blank" rel="noopener">doi:10.1021/acs.macromol.4c03265</a></li>
  <li id="ref-2">J. Tamnanloo et al. Cross-domain training for surface tension prediction of polymers and liquids. Manuscript in preparation.</li>
  <li id="ref-3">S. Otsuka, I. Kuwajima, J. Hosoya, Y. Xu, M. Yamazaki. PoLyInfo: polymer database for polymeric materials design. <em>2011 International Conference on Emerging Intelligent Data and Web Technologies</em>, 22–29 (2011). <a href="https://doi.org/10.1109/EIDWT.2011.13" target="_blank" rel="noopener">doi:10.1109/EIDWT.2011.13</a></li>
</ol>

{% include gnn_st/script.html %}
