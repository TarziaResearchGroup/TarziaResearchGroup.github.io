---
permalink: /research/
title: "What we do"
author_profile: true
---

See blog posts on [Andrew's personal website](https://andrewtarzia.github.io/year-archive/).

Code snippets and recipes are also available on [GitHub Gists](https://gist.github.com/andrewtarzia).


## Low-cost computational tools and robust software for decision-making

We are working toward bridging the gap between how computational tools are used in chemical and materials design processes.
A significant part of this is the development of new software ecosystems that are FAIR and easy-to-use by researchers of various expertises.

![Components in molecular materials design](/assets/research_schematic_aprofuob_1.png)


<> <details>
<>   <summary>
<>      <p style="font-size:20px; display:inline">Structure generation of (supra)molecular materials</p>
<>   </summary>
<>   <p>
<>      We continue to develop an ecosystem built around the work done by Andrew in <a href="https://github.com/lukasturcani/stk"><> <i>stk</i></a> for generating molecular and periodic structures. Find tutorials: <a href="https://www.youtube.com/watch?v=mPr9D7nCQ84&list=PLIWYdPQ9hLzVngMF8NOkiApMtgc_ZwZgO"><i>stk</i> tutorial videos</a> and <a href="https://github.com/andrewtarzia/stk-examples">code</a>.
<>   </p>
<> </details>

## Structure generation of (supra)molecular materials

We continue to develop an ecosystem built around the work done by Andrew in [<i>stk</i>](https://github.com/lukasturcani/stk) for generating molecular and periodic structures. Find tutorials: [<i>stk</i> tutorial videos](https://www.youtube.com/watch?v=mPr9D7nCQ84&list=PLIWYdPQ9hLzVngMF8NOkiApMtgc_ZwZgO) and [code](https://github.com/andrewtarzia/stk-examples).

### Using coarse-grained and minimal models

[_cgx_](https://github.com/andrewtarzia/CGExplore) is a library for using _stk_ with coarse-grained molecules to afford more efficient high-throughput screening and rational design. This library is under-development but it's first usage is written up [here](https://chemrxiv.org/engage/chemrxiv/article-details/64c7aed1658ec5f7e57cf4d8).

### Preparing building blocks for structure generation

[bbprepared](https://github.com/andrewtarzia/bbprepared) contains algorithms and tests for preparing building blocks for <i>stk</i> usage. [Here](https://youtu.be/dbQwhlpf5Jc) is a video on its usage. The [documentation](https://bbprepared.readthedocs.io/en/latest/) contains useful recipes and examples, such as finding the lowest energy conformer:

```python
import stk
import stko
import bbprep

building_block = stk.BuildingBlock(smiles="C1=CC=NC(=C1)C=NBr")

# This uses the rdkit conformer generation.
ensemble = bbprep.generators.ETKDG(num_confs=100).generate_conformers(
    building_block
)

# Iterate over ensemble.
minimum_score = 1e24
minimum_conformer = bbprep.Conformer(
    molecule=ensemble.get_base_molecule().clone(),
    conformer_id=-1,
    source=None,
    permutation=None,
)
for conformer in ensemble.yield_conformers():
    # Something here to calculate energy.
    score = stko.MMFFEnergy().get_energy(conformer.molecule)
    if score < minimum_score:
        minimum_score = score
        minimum_conformer = bbprep.Conformer(
            molecule=conformer.molecule.clone(),
            conformer_id=conformer.conformer_id,
            source=conformer.source,
            permutation=conformer.permutation,
        )
```


### Optimising structures

[<i>stko</i>](https://github.com/JelfsMaterialsGroup/stko) contains wrappers for optimisation and property calcualtion of <i>stk</i> molecules.
The [documentation](https://stko-docs.readthedocs.io/) contains recipes and tutorials.

I have also developed some low-cost Monte Carlo-based algorithms for optimisation _stk_ molecule optimisation ([_MCHammer_](https://github.com/andrewtarzia/MCHammer)) and host-guest conformer generation/optimisation ([_SpinDry_](https://github.com/andrewtarzia/SpinDry)).

### Visualising molecular pores

[_PoreMapper_](https://github.com/andrewtarzia/PoreMapper) is a very efficient way to map the inside of a molecular pore for visualisation and analysis. See a blog post [here](https://andrewtarzia.github.io/posts/2021/11/poremapper-post/).


### Databases of toy-model material space

While the [_cgx_](https://cgexplore.readthedocs.io/en/latest/) documentation holds examples and tutorials for usage, we also publish our toy-model landscapes on [_cgmodels_](https://cgmodels.readthedocs.io/en/latest/), which are explorable using [_chemiscope_](https://chemiscope.org).

## Exploring host-guest system design at low-cost


## Calculating molecular size

[_mol-ellipsize_](https://github.com/andrewtarzia/mol-ellipsize) is an efficient method for calculating molecular size based on fitting an ellipsoid to the vdw cloud of a molecule. Examples are provided within the github repository. See a blog post [here](https://andrewtarzia.github.io/posts/2022/01/molellipsize-post/).

## Interpreting and analysing dynamic trajectories

[_dynsight_](https://github.com/GMPavanLab/dynsight) is a software package Andrew manages the development of in collaboration with the Pavan Lab.
This software is working toward streamlining the analysis of trajectories of particles.
